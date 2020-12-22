## Introduction

_Last modified: January 30th, 2020_

To my knowledge, this will be the first open-source system for private federated learning on server, web, and mobile anywhere on the planet. Our target platforms will include worker libraries written for servers (Python), web browsers (Javascript), Android devices (Kotlin), and iOS devices (Swift). We will do this by allowing for PySyft "plans" to be executed by a remote worker other than PySyft itself.

For the web, we must run TensorFlow.js as our deep learning framework. However, in order to run PyTorch plans in TensorFlow.js, we must first serialize the operations as a list, and then convert each operation into the appropriate commands available in TensorFlow.js. This translation layer will be described in more detail below.

Conversely, for Android and iOS, we have chosen to utilize PyTorch Mobile. PyTorch Mobile allows us to run plans for both training and inference of PyTorch models via a wrapper library (written in Java) for Android and using LibTorch (PyTorch’s internal C++ library) for iOS. There is not currently a finished Objective-C or Swift wrapper that has been released by the PyTorch team. It’s worth noting that for the mobile workers, plans will need to be converted into TorchScript in order to be executed - the Javascript worker does not have this concern.

In addition to "plans" that represent a batch of operations to be executed on a single worker, PySyft introduces the concept of a "protocol" that represents a distributed computation graph with defined worker roles. A "protocol" deployed to workers should allow executing SMPC algorithms such as those necessary for secure aggregation. Secure aggregation will require workers, or a subset of workers, to communicate directly - this can be accomplished by using WebRTC to establish a peer-to-peer data channel between workers. This allows for an added layer of protection to the workers that is separate from differential privacy which is applied as part of the eventual model update process on PyGrid.

**Patrick Cason<br />**
_Web and Mobile Team Lead_

## Terminology

Let’s start off by defining a few terms that will be regularly used throughout this document:

- **Model** - a standard machine learning model
- **Operation/Command** - a single function in PyTorch, TensorFlow, or TensorFlow.js
- **Plan** - a serialized list of operations that can be executed by a worker
- **Protocol** - a graph of operations on a list of workers, executed over WebRTC
- **Worker** - any server, device, or browser that is capable of running a PySyft model for training and inference
- **VirtualWorker** - a virtualized Python worker that’s capable of pretending to be a separate server-based worker
- **PyTorch** - a deep learning library written in Python
- **LibTorch** - the tensor-based mathematical library written in C++ that is called by PyTorch
- **TorchScript** - a generated language that allows for a PyTorch method to be simplified into an object representing PyTorch operations. In the context of our system, we will serialize PySyft plans into TorchScript so that they may be executed by mobile worker libraries.
- **Wrapper library** - a library written in one language that allows for execution in another language. For instance, there is a Java wrapper for LibTorch which is written in C++.
- **Averaging plan** - the plan run by the central server (PyGrid) that determines how the models should be aggregated to eventually update the global model
- **Cycle** - a single run of the federated learning process from workers pulling down the model and training it until the global model update process is finished
- **Secure aggregation** - given a state where multiple parties each have one or more numbers, these techniques allow them to average their numbers without any party seeing any other party’s raw input to the average.
- **Secure multi-party computation (SMPC)** - a class of algorithms allowing for multiple parties to collaboratively compute a function without revealing their inputs to the function to each other.

We will also use this section for defining each of the components of the OpenMined federated learning system:

- **PySyft** - a framework for privacy-preserving machine learning that hooks both PyTorch and TensorFlow
- **PyGrid** - a library consisting of multiple services that allows for PySyft workers to be deployed across a network. It’s also responsible to manage the FL process and host models, plans, configurations, and tensors.
- **syft-proto** - a Protocol Buffer interface used between PySyft and the various worker libraries that allows for class definitions to be shared across platforms
- **syft.js** - the official Javascript worker library for PySyft, running in the web browser
- **KotlinSyft** - the official Kotlin worker library for PySyft, running on Android devices
- **SwiftSyft** - the official Swift worker library for PySyft, running on iOS devices
- **Threepio** - a small command translation library that allows for PyTorch or TensorFlow commands to be translated to and from TensorFlow.js

## Overview

[View a diagram of this process](https://drive.google.com/file/d/1xWKA9YEJCdUq-y49Sx1vSlR5n-48v7dH/view?usp=sharing)

The OpenMined federated learning workflow is [loosely inspired Google’s federated learning workflow](https://arxiv.org/pdf/1902.01046.pdf), but we provide a bit more generalization since we don’t also control the operating system itself. Our workflow consists of the following steps:

### 1. Design

A developer designs their FL model using PyTorch in PySyft. This process involves the creation of a model, an averaging plan, and various plans and protocols a developer desires to run on the workers.

The averaging plan will instruct PyGrid on how to average model diffs that are returned from the workers. This is also known as the "model update" plan whereby PyGrid receives trained model diffs from workers, averages them, and then updates the global model before beginning another cycle.

The developer may also define as many plans and protocols they desire for the worker to run on their device. For simplification purposes, you can think of a plan as code the worker runs by itself, and a protocol as code that's run by the worker in conjunction with one or more other workers. Plans are generally going to include the core training logic, while a protocol may allow multiple workers to perform secure aggregation or other forms of encrypted computation together over WebRTC.

Below is a proposed sample code block of how this might work:

```py
import syft as sy
import torch
import requests

hook = sy.TorchHook(torch)
hook.local_worker.is_client_worker = False

class Net(sy.Plan):
    def __init__(self):
        super(Net, self).__init__()
        self.linear1 = torch.nn.Linear(10, 5)
        self.linear2 = torch.nn.Linear(5, 1)

    def forward(self, x):
        x = self.linear1(x)
        x = torch.nn.functional.relu(x)
        x = self.linear2(x)
        return x

# Model
model = Net()

x = torch.zeros(1, 10)
y = torch.zeros(1, 1)

# Averaging plan - run by PyGrid
@func2plan
def averaging_plan(model_params):
    sum = model_params[0]
    for params in model_params[1:]:
        sum += params
    avg = sum / len(model_params)
    return avg

# Training plan - run by worker
@func2plan(model=model, data=x, target=y, optimizer=nn.SGD(model.parameters(), lr=0.01))
def training_plan(model, data, target, optimizer):
    data, target = data, target
    optimizer.zero_grad()
    output = model(data)
    loss = F.nll_loss(output, target)
    loss.backward()
    optimizer.step()

# Secure aggregation protocol - run by worker
worker1 = sy.VirtualWorker(hook=hook, id="worker1")
worker2 = sy.VirtualWorker(hook=hook, id="worker2")
worker3 = sy.VirtualWorker(hook=hook, id="worker3")

worker1_model = worker1.Promise.Model()
worker2_model = worker2.Promise.Model()
worker3_model = worker3.Promise.Model()

worker1_shares = worker1_model.share(worker1, worker2, worker3)
worker2_shares = worker2_model.share(worker1, worker2, worker3)
worker3_shares = worker3_model.share(worker1, worker2, worker3)

new_model_shares = (worker1_shares + worker2_shares + worker3_shares) / 3

new_model_shares["worker1"].declare_output()
new_model_shares["worker2"].declare_output()
new_model_shares["worker3"].declare_output()
secure_aggregation_protocol = sy.Protocol(worker1, worker2, worker3)
```

### 2. Test

At this point, a developer will test their code against VirtualWorkers in PySyft, allowing them to locally simulate the process of deploying their model to the edge. The developer will also want to define their initial model parameters (e.g. model name, version, hyperparameters, etc.) and server configuration (e.g. the number of cycles, maximum number of workers, etc.).

This process will create a network of VirtualWorkers in PySyft, send the various worker plans and protocols to each of them, execute the model on each of the VirtualWorkers, push the results back to PySyft, run the averaging plan to update the global model, and finally return the model back to the developer for inspection.

```py
# These attributes should correspond to inputs in the plans
# You can include custom attributes in here to your liking, the only ones required by PyGrid are "name" and "version"
client_config = {
  name: "my-federated-model",
  version: "0.1.0",
  batch_size: 32,
  lr: 0.01,
  optimizer: "SGD"
}

server_config = {
  max_workers: 100,
  pool_selection: "random",  # or "iterate"
  num_cycles: 5,
  do_not_reuse_workers_until_cycle: 4,
  cycle_length: 8 * 60 * 60,  # 8 hours
  minimum_upload_speed: 2000,  # 2 mbps
  minimum_download_speed: 4000,  # 4 mbps
  authentication: {  # optional (but highly suggested) authentication
    type: 'jwt',
    method: 'POST',
    endpoint: 'https://api.example.com/verify-token',
    secret: 'your-256-bit-secret',  # https://jwt.io/#debugger-io
    is_secret_encoded: true
  }
}

sy.test_federated_training(
  model=model,
  client_plans={ "training_plan": training_plan },
  client_protocols={ "secure_agg_protocol": secure_aggregation_protocol },
  client_config=client_config,
  server_averaging_plan=averaging_plan,
  server_config=server_config
)
```

**A note about authentication:**<br />
If you don't have some authentication logic, you make yourself open to [Sybil attacks](https://en.wikipedia.org/wiki/Sybil_attack). **We highly suggest** that anyone hosting a PyGrid instance for federated learning should also create two endpoints on their user authentication API: one for creating tokens (called by the worker) and one for verifying those tokens (called by PyGrid). Before PyGrid verifies the token with the given user authentication API, it must first ensure that the 256-bit secret that signs the token is identical to the one provided. If it is, then the token is sent to the `endpoint` described above to be verified by the user authentication API. The full authentication flow will be described further in subsequent documentation with examples provided for how this could be done.

### 3. Host

Now that the model has been tested locally, it’s time to host the model on PyGrid. This will allow for training cycles to begin on end-user devices. The developer needs to connect to an existing PyGrid Node and send the model, various worker plans and protocols, averaging plan, and various configurations to be stored in PyGrid properly.

```py
import grid as gr

pygrid = gr.WebsocketGridClient(
  hook,
  id="my-name",
  address="https://localhost:3000"
)

pygrid.connect()

pygrid.host_federated_training(
  model=model,
  client_plans={ "training_plan": training_plan },
  client_protocols={ "secure_agg_protocol": secure_aggregation_protocol },
  client_config=client_config,
  server_averaging_plan=averaging_plan,
  server_config=server_config
)
```

### 4. Execute

Each worker is a library that may be integrated within the context of a web or mobile app. This integration will be relatively straight-forward, requiring no more than a few lines of code. The following is an example of how the syft.js Javascript worker might integrate into an application:

```js
import syft from 'syft.js';
import tf from '@tensorflow/tfjs';

const run = async () => {
  // 0. If you're using authentication, and we suggest you do, make a request to your API for a JSON Web Token
  const jwtTokenRequest = await fetch('https://api.example.com/request-token', {
    method: 'POST',
    body: JSON.stringify(user.id) // The user.id may come from some other auth flow done earlier
  });
  const token = jwtTokenRequest.json();

  const worker = new syft({
    url: 'https://localhost:3000',
    auth_token: token  // An optional authentication token that can validate the identity of a worker
  });

  // You may set up multiple jobs.
  const job = worker.newJob({
    model: 'my-federated-model',
    version: '0.1.0'  // If omitted, PyGrid will assume it's the latest version
  });

  // 1. Determine if there is a cycle that the worker can join. If there is a cycle available, it will automatically download the model, plan, and config from PyGrid. If there isn't a cycle available, this code block will automatically retry at the requested timestamp.

  // NOTE FOR MOBILE WORKERS: This is the place to check for a wifi connection, whether or not the device is charging, and whether or not the user is likely asleep.
  job.start();

  // 2. Once the worker has been approved to participate in a cycle and the model, plan(s), protocol(s), and config have been downloaded...
  job.on('accepted', async ({ model, client_config }) => {
    const { batch_size, optimizer } = client_config;

    // Load your data and targets
    const rawData = [image1, image2, image3, image4, image5, ...];
    const rawTargets = ['dog', 'cat', 'cat', 'neither', 'dog', ...];

    // Batch your data and targets
    const data = [];
    const targets = [];

    while(rawData.length) {
      data.push(rawData.splice(0, batch_size));
    }

    while(rawTargets.length) {
      targets.push(rawTargets.splice(0, batch_size));
    }

    // 3. Execute the plan by name in batches.
    for(let i = 0; i < data.length; i++) {
      await job.plans['training_plan'].execute(model, data[i], target[i], optimizer);
    }

    // 4. Once the plan has been executed, execute the protocol. This will spawn WebRTC and send this job's model diff to other workers to be securely aggregated.
    await job.protocols['secure_agg_protocol'].execute();

    // 5. Afterwards, the job reports the resulting diff (or share of the securely aggregated diff) back to PyGrid.
    job.report();
  });

  job.on('rejected', ({ timeout }) => {
    // Handle the job rejection
    console.log('We have been rejected by PyGrid to participate in the job.')

    const msUntilTry = timeout * 1000;

    // Try to join the job again in "msUntilRetry" milliseconds
    setTimeout(() => {
      job.start();
    }, msUntilRetry)
  });

  job.on('error', error => {
    // Handle the job error
    console.log('There was an error with executing one of the plans or protocols', error);
  });
}
```

One initial detail worth noting is that it’s assumed a worker could be running multiple jobs at the same time. A syft worker will need to intelligently observe each job as unique, handling the current training state and other various resources and tasks independent of other jobs. It’s worth noting that mobile phones will not likely have the compute resources necessary for running multiple jobs simultaneously. Because of this, we should allow for multiple concurrent jobs to be executed, but warn the developer at compile time that this is very bad practice for mobile.

Upon first glance, the example above is performing a lot of "magic" behind the scenes. Once calling the `start()` method, the worker will first authenticate with PyGrid by optionally passing an `auth_token`. If PyGrid has JWT authentication configured in the `server_config`, it will use the `auth_token` variable to check for a positive identity of a worker. In the event that no `auth_token` is passed when one is required, or if the `auth_token` that was passed is an invalid token, the worker will be notified by PyGrid that authentication has failed. In the event that no `auth_token` is passed and no authentication configuration exists in PyGrid itself, then this step will be skipped. This token should be relative to the user who is requesting to participate in the federated learning cycle.

After this, the worker will perform a network connection test with PyGrid to ensure that it has a viable connection for model training and inference. This will include the worker reporting the following information to PyGrid: ping, average download speed, average upload speed, and the format that the worker likes to receive a plan (list of operations or TorchScript). It’s worth noting that we want to send as little information to PyGrid as possible, only what is strictly required to ensure a reasonably paced training cycle. **Workers will not send information related to wifi connectivity, charging state, or asleep/awakeness of the user. It will be the responsibility of the client-side mobile developer to determine what criteria is appropriate for when model training should take place.**

It’s entirely possible that after calling `start()` that PyGrid requests for the worker to keep waiting and check back in at a later time. PyGrid will need to serve a timestamp to the worker notifying it of when to check back in. It should be noted that the worker will not need to call `start()` again at this later point; instead, the worker will simply go into "sleep mode" until that time. This will disable the socket connection and start a timer.

When the `on('accepted')` event listener is triggered, this means that the worker has been chosen to participate by PyGrid and the model, plan(s), protocol(s), and client configuration have been downloaded. Again, this magically happens in the background. At this point, the developer will likely batch their input and label data sets, and the worker may begin to run `execute()` against one of their plans.

We also have two other event listeners: one for handling rejection of an FL cycle request by PyGrid (`on('rejected')`) and another one for handling error during the execution of a plan or protocol (`on('error')`). You may write whatever logic you desire in these event handler callbacks, but it's suggested that you automatically try to re-join an FL cycle after a provided `timeout`. The code example above shows how this will be done.

Once the plan is fully trained, the developer may opt to run a protocol with a group of other workers. We can do this by calling `execute()` against one of their protocols. The trained model will automatically be passed into the `execute()` function in the background.

You can expect the code sample above to change slightly between the various worker libraries. It’s worth considering that the mobile workers are also plagued by different concerns like detecting when the user is awake or asleep, determining charge status, and being limited to execution time limits for background tasks to name a few. It will be up to the mobile libraries themselves to do the detection of this criteria (battery level, charging/not-charging, internet connection speed, and asleep/awake), and we will provide reasonable default levels. However, any of these criteria should be allowed to be overridden by the developer as per their specific use-case.

### 5. Aggregate

At this point, a model has either been trained and the diff has been reported back to PyGrid. Alternatively, if a protocol exists, then shares of a securely aggregated (and trained) model diff have been reported back to PyGrid. If PyGrid receives multiple shares of a model diff, then it will need to combine the shares and then decrypt the result. If the report is sent within the time limit of the cycle (set in the server configuration above), it will be accepted. Otherwise, it will be discarded. The worker will not be notified in either situation.

At this point, PyGrid needs to update the global model with the new weights. Google does this by using an algorithm they appropriately call "Federated Averaging". While it’s perfectly appropriate to use their averaging algorithm, we opted to allow the developer to define their own in the form of a PySyft plan, aptly called the "averaging plan". This function will go through each of the reported model diffs and average them against the global model, which then persists as the new global model for future cycles.

It’s important to note that this will actually create a new "checkpoint" of the model. If the developer originally uploaded a model to PyGrid of name "my-federated-model" with a version of "0.1.0", then it would automatically create a checkpoint of "1". For each checkpoint after that, the value will increment. It would be beneficial for PyGrid to also allow a developer to name their checkpoints something more memorable like "latest" or "stable" or "best-version-yet".

### 6. Inspect

Depending on the server configuration, the developer may opt to have multiple training cycles. In this case, a new cycle will begin at the determined interval. However, assuming we’ve finished all the cycles, the model will now be ready for inspection by the developer and may be used for inference, retrained, or whatever they desire. The developer may decide to pull a specific version of a model, or may optionally decide to even pull a specific checkpoint instead. The process of federated learning is now considered complete.

```py
import grid as gr

pygrid = gr.WebsocketGridClient(
  hook,
  id="my-name",
  address="https://localhost:3000"
)

pygrid.connect()

trained_fl_model = pygrid.get_model(name="my-federated-model", version="0.1.0", checkpoint="latest")
```

## Projects

There are many projects that we consider vital to achieving our MVP. [You may also view our current progress on Github](https://github.com/orgs/openmined/projects/13). The high-level projects we must complete are as follows:

### PySyft

- [Refactor Plans](https://github.com/OpenMined/PySyft/issues/2912)
- [Refactor Protocols](https://github.com/OpenMined/PySyft/issues/2903)
- [Refactor PyTorch tensor hooking](https://github.com/OpenMined/PySyft/issues/2991)
- [Allow PySyft to package plan operations either as a list of individual commands or as TorchScript](https://github.com/OpenMined/PySyft/issues/2994)
- [Add test federated training method to PySyft](https://github.com/OpenMined/PySyft/issues/2995)
- [Build a federated learning worker for PySyft](https://github.com/OpenMined/PySyft/issues/2996)
- _Optional_ - [Implement the command translation layer inside of PySyft which will allow for PySyft Tensorflow plans to be converted to PyTorch](https://github.com/OpenMined/PySyft/issues/2997)

### PyGrid

- [Add WebRTC socket signaling support to PyGrid](https://github.com/OpenMined/PyGrid/issues/412)
- [Add host federated training method to PyGrid](https://github.com/OpenMined/PyGrid/issues/435)
- [Add API worker websocket and HTTP endpoints for FL to PyGrid](https://github.com/OpenMined/PyGrid/issues/445)
- [Add oAuth support for FL workflow](https://github.com/OpenMined/PyGrid/issues/496)
- [Add get model method to PyGrid](https://github.com/OpenMined/PyGrid/issues/436)
- [Allow PyGrid to serve plan operations as either a list of individual commands (syft.js) or as TorchScript (Android and iOS) depending on the requesting environment](https://github.com/OpenMined/PyGrid/issues/437)
- [Implement federated learning cycles in PyGrid](https://github.com/OpenMined/PyGrid/issues/438)
- [Add averaging plan and global model updating functionality to PyGrid](https://github.com/OpenMined/PyGrid/issues/439)
- _Optional_ - [Add a few predefined averaging plans (like “Federated Average”) to PyGrid](https://github.com/OpenMined/PyGrid/issues/440)
- _Optional_ - [Allow for periodic status updates of current FL cycles on PyGrid](https://github.com/OpenMined/PyGrid/issues/441)

### syft-proto

- [Create Protobuf schemas from PySyft classes](https://github.com/OpenMined/syft-proto/issues/35)
- [Set up a CI pipeline and version release system in syft-proto with Github Actions](https://github.com/OpenMined/syft-proto/issues/36)

### syft.js

- [Migrate syft.js to use Protobuf classes](https://github.com/OpenMined/syft.js/issues/83)
- [Implement the command translation layer inside of syft.js](https://github.com/OpenMined/syft.js/issues/86)
- [Implement split and stitch algorithm for data channels in syft.js](https://github.com/OpenMined/syft.js/issues/78)
- [Add bandwidth and Internet connectivity test in syft.js](https://github.com/OpenMined/syft.js/issues/88)
- [Scaffold basic proposed worker API in syft.js](https://github.com/OpenMined/syft.js/issues/87)
- [Execute plans in syft.js](https://github.com/OpenMined/syft.js/issues/89)
- [Execute protocols in syft.js](https://github.com/OpenMined/syft.js/issues/90)
- [Allow for training state to be persisted to temporary storage in the event of a failure in syft.js](https://github.com/OpenMined/syft.js/issues/91)
- _Optional_ - [Add a stopping method that stops the training process](https://github.com/OpenMined/syft.js/issues/93)

### KotlinSyft

- [Create the basic structure of KotlinSyft](https://github.com/OpenMined/KotlinSyft/issues/29)
- [Implement WebRTC flow in Android](https://github.com/OpenMined/KotlinSyft/issues/11)
- [Implement Protobuf in Android](https://github.com/OpenMined/KotlinSyft/issues/30)
- [Set up deployment to Maven](https://github.com/OpenMined/KotlinSyft/issues/3)
- [Implement split and stitch algorithm for data channels in Android](https://github.com/OpenMined/KotlinSyft/issues/31)
- [Add support for background task scheduling in Android](https://github.com/OpenMined/KotlinSyft/issues/35)
- [Implement sleep/wake detection in Android](https://github.com/OpenMined/KotlinSyft/issues/36)
- [Add support for charge detection and wifi detection in Android](https://github.com/OpenMined/KotlinSyft/issues/37)
- [Add bandwidth and Internet connectivity test in Android](https://github.com/OpenMined/KotlinSyft/issues/28)
- [Scaffold basic proposed worker API in Android](https://github.com/OpenMined/KotlinSyft/issues/23)
- [Execute plans in Android](https://github.com/OpenMined/KotlinSyft/issues/32)
- [Execute protocols in Android](https://github.com/OpenMined/KotlinSyft/issues/33)
- [Allow for training state to be persisted to temporary storage in the event of a failure in Android](https://github.com/OpenMined/KotlinSyft/issues/34)
- _Optional_ - [Add a stopping method that stops the training process](https://github.com/OpenMined/KotlinSyft/issues/39)

### SwiftSyft

- [Create the basic structure of SwiftSyft](https://github.com/OpenMined/SwiftSyft/issues/30)
- [Implement WebRTC flow in iOS](https://github.com/OpenMined/SwiftSyft/issues/17)
- [Implement Protobuf in iOS](https://github.com/OpenMined/SwiftSyft/issues/31)
- [Set up deployment to Cocoapods](https://github.com/OpenMined/SwiftSyft/issues/27)
- [Implement split and stitch algorithm for data channels in iOS](https://github.com/OpenMined/SwiftSyft/issues/32)
- [Add support for background task scheduling in iOS](https://github.com/OpenMined/SwiftSyft/issues/36)
- [Implement sleep/wake detection in iOS](https://github.com/OpenMined/SwiftSyft/issues/37)
- [Add support for charge detection and wifi detection in iOS](https://github.com/OpenMined/SwiftSyft/issues/38)
- [Add bandwidth and Internet connectivity test in iOS](https://github.com/OpenMined/SwiftSyft/issues/29)
- [Scaffold basic proposed worker API in iOS](https://github.com/OpenMined/SwiftSyft/issues/28)
- [Execute plans in iOS](https://github.com/OpenMined/SwiftSyft/issues/33)
- [Execute protocols in iOS](https://github.com/OpenMined/SwiftSyft/issues/34)
- [Allow for training state to be persisted to temporary storage in the event of a failure in iOS](https://github.com/OpenMined/SwiftSyft/issues/35)
- _Optional_ - [Add a stopping method that stops the training process](https://github.com/OpenMined/SwiftSyft/issues/40)

### Threepio

- [Scaffold the initial version of Threepio](https://github.com/OpenMined/threepio/issues/4)
- [Create translation mappings](https://github.com/OpenMined/threepio/issues/22)
- [Create automatic translation layer in javascript](https://github.com/OpenMined/threepio/issues/5)
- [Create automatic translation layer in python](https://github.com/OpenMined/threepio/issues/23)

### General

- [Work on multiple end-to-end demos utilizing all 3 Syft worker libraries](https://github.com/OpenMined/syft.js/issues/85)
- [Develop end-to-end testing suite for all full system testing](https://github.com/OpenMined/syft-proto/issues/37)
