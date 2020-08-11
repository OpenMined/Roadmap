<table>
  <tr>
    <td align="center">
      <a href="https://github.com/LaRiffle">
        <img src="https://avatars3.githubusercontent.com/u/12446521?s=240" width="170px;" alt="Théo Ryffel">
        <br /><sub><b>Théo Ryffel</b></sub></a><br />
        <sub>Team Lead</sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/youben11">
        <img src="https://avatars0.githubusercontent.com/u/21220087?s=240" width="170px;" alt="">
        <br /><sub><b>Ayoub Benaissa</b></sub></a><br />
        <sub>CrypTen integration</sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/ajnovice">
        <img src="https://avatars3.githubusercontent.com/u/3927652?s=240" width="170px;" alt="">
        <br /><sub><b>Ajay Singh</b></sub></a><br />
        <sub>CrypTen integration</sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/gmuraru">
        <img src="https://avatars1.githubusercontent.com/u/7805588?s=240" width="170px;" alt="">
        <br /><sub><b>George Muraru</b></sub></a><br />
        <sub>CrypTen integration</sub>
      </a>
    </td>
  </tr>
</table>

## TL;DR

The current goal is to be able to start a crypten computation from a syft worker. Crypten parties would be run inside syft workers, those workers can be holding their own private data, which should be encrypted during computation. The way this should be used can be illustrated in the following code snippet.

```python
# alice and bob are syft workers

@run_multiworkers([alice, bob,], master_addr="127.0.0.1")
def crypten_computation():
	# load data from syft worker using its tag
	# “crypten_data” is a tag that reference two different private tensors at alice and bob
	alice_tensor = syft_crypt.load("crypten_data", src=1)
	bob_tensor = syft_crypt.load("crypten_data", src=2)
	res = alice_tensor * bob_tensor
	return res.get_plain_text()
```

To be able to provide such API, we need to be able to start a crypten party at each worker, be able to load data from the worker using a tag, send the function in a secure manner and get back the result. We details each milestone below:

- [x] 1. Launch Crypten parties from Pysyft to run a fixed function with fixed data
- [x] 2. Get a return value from a CrypTen execution
- [ ] 3. Send common argument tensors to all parties (~plan.state)
- [ ] 4. Allow CrypTen parties to load private data from Syft workers using tags (not files)
- [ ] 5. Send a function to CrypTen parties to be executed (using Plans)
- [ ] 6. Remote model evaluation by CrypTen parties on private data (using Plans with a state)
- [ ] 7. Choose between imposing the backward pass from Plans or use CrypTen Autograd
- [ ] 8. Remote model training using Plans on private data

## 1. Launch Crypten parties from Pysyft to run a fixed function with fixed data

> https://github.com/OpenMined/PySyft/pull/2963

We build a new context of computation which can run parties that are distributed across syft workers. The communication of crypten parties remains the same, however, syft workers handle initialization and the serialization of return values.

The crypten computation done for the moment is a toy function defined at worker level. The exchange of function isn't yet supported for security reasons.

This PR introduces:

- A new message type CryptenInit that lets workers exchange information such as rank of crypten party to run, number of parties involved, and ip and port of the master party.
- A new router for the CryptenInit message type that runs crypten party according to the information received.

![PySyft-Crypten-context-of-execution](https://user-images.githubusercontent.com/21220087/73119691-cd7d2900-3f65-11ea-91aa-afd70c8f8aee.png)


#### Code samples

Fixed toy function
```python
def toy_func():
    # Toy function to be called by each party
    alice_t = crypten.cryptensor([73, 81], src=0)
    bob_t = crypten.cryptensor([90, 100], src=1)
    out = (alice_t + bob_t).get_plain_text()
```

Run from syft context:
```python
# self, alice and bob
n_workers = 3
alice = workers["alice"]
bob = workers["bob"]

@run_multiworkers([alice, bob], master_addr="127.0.0.1")
def test_three_parties():
    pass  # pragma: no cover

return_values = test_three_parties()
# A toy function is ran at each party, and they should all decrypt
# a tensor with value [90., 100.]
expected_value = [90.0, 100.0]
for rank in range(n_workers):
    assert (
        return_values[rank] == expected_value
    ), "Crypten party with rank {} don't match expected value {} != {}".format(
        rank, return_values[rank], expected_value
        )
```

## 2. Get a return value from a CrypTen execution

TBD: what is the kind of data that we can currently return? Only numbers? tensors?
What's our strategy to return arbitrary objects (list, tuple, dict) containing tensors and/or numbers ?

## 3. Send common argument tensors to all parties (~plan.state)

Because each CrypTen party can refer to a Syft worker, we leverage the syft architecture to send public tensors to all parties. Hence, the Syft serde protocol will be used here, which allows to send close to every type of objects and will be using protobuf in the mid term.

This functionality is important to execute remote plans on CrypTen workers. Basically, this will be equivalent to sending the state of a plan, which only happens at the beginning of the plan execution.

## 4. Allow CrypTen parties to load private data from Syft workers using tags

> https://github.com/OpenMined/PySyft/pull/3003
> https://github.com/OpenMined/PySyft/issues/3043

In practice, this will be done by modifying the `crypten.load` function to provide a search function which actually calls the associated syft worker for a search on its object store based on tags (we have in syft: `worker.search('#tag1', '#tag2')`). We will have the reverse operation as well to save back tensors in the syft worker.

![PySyft-Crypten-context-of-execution-v2](https://user-images.githubusercontent.com/21220087/74042481-e820ba80-49c7-11ea-9c72-99bd0f2f0b8d.png)


## 5. Send a function to CrypTen parties to be executed (using Plans)

> https://github.com/OpenMined/PySyft/issues/3025
> https://github.com/OpenMined/PySyft/issues/2987

To switch from fixed to arbitrary function execution, we will leverage again the syft workers and their ability to receive and execute Plans. In practice, a crypten worker will ask his syft worker to run a specific plan which will only contain high level operations (like x * y for a MPC multiplication). Crypten will then use his crypto protocol to transcript properly these high level operations into crypto-level sub operations.

The internal implementation of this will not be very different from how Plans currently work: instead of running operations on PlaceHolders instantiated by torch tensors, the PlaceHolders will be instantiated by `crypten.tensors`.

## 6. Remote model evaluation by CrypTen parties on private data (using Plans with a state)

In this step, we combine the two previous steps to combine a model evaluation (which is just a Plan with a state) using private data, accessed through the  modifier `crypten.load`. Note that in this case, we consider the model to be visible to the crypten party: it will be shipped using `plan.state`. Using private models which are not owned by the data owner is still under investigation.

This will be an important milestone to benchmark efficiency of this solution.

## 7. Choose between imposing the backward pass from Plans or use CrypTen Autograd

Moving forward to model training requires to handle backpropagation. We have here several possibilities:
- If we use directly CrypTen AutogradTensor (so now the execution chain from the plan standpoint would be `PlaceHolder>CrypTen.AutogradTensor>CrypTen.Tensor`)

- Plans might handle backward at some point: currently plans only have a `forward` set of operations, but in future they will also have a `backward` one. This one could be used by CrypTen parties to run their gradient computation. This `backward` could actually be computed using syft.AutogradTensors.

## 8. Remote model training using Plans on private data

Next step will be to integrate this in a real use case, which should in particular integrate an optimizer and a loss function. As in step 6, the model will be visible by all parties, until we support loading private models.

Secure aggregation would be a nice feature at this point.

This will be an important milestone to benchmark efficiency of this solution.


### Questions to the CrypTen team:
- Would it be possible to modify `crypten.load` to support custom loader for tensors instead of `torch.load` which is currently used under the hood?
- Would it be possible to load private tensors, ie tensors whose shares are held by different parties?
