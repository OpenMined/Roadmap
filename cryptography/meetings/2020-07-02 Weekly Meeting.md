### General Announcements
- A lot of thoughts around syft 0.3
- What's the crypto strat for 0.3?

### Recap

TIM TITCOMBE
- Welcome!
- worked on SplitNN
- Now on PryVote using SSI -> need some crypto stuff

AYOUB
- Benchmark against Crypten: ResNet we are some overhead. Waiting for feedback from the crypten team
- TenSEAL: Reviewing some PRs, but next week: roadmap scheduling!

GEORGE
- Crypten: PR regarding POC plans got approved and I think it is ready for merge:  https://github.com/OpenMined/PySyft/pull/3531
- Crypten: PR with OnnxModels (the model is at different parties and the local party that starts the computation does not know how the architecture looks - only the parties that really do the computation knows about the model - we can only run the inference) : https://github.com/gmuraru/PySyft/pull/9 (and the syft-proto PR that adds the OnnxModels: https://github.com/OpenMined/syft-proto/pull/129) -- this might not be needed since from what I know currently we do not use protobuf, but the implementation is "protobuf" ready
- CrypTen: TODO for me -- work on the blogpost draft initiated by Ayoub
- Crypten Demo: Reworking the demo - nearly finished it (PlaceHolders are giving me some hard times when trying to unwrap them when running the real crypten computation -- currently I have a bug with max_recursion_reached)
- Syft Core 3.0: Add some stubs for the tests  + coverage setup (currently is 0 percent because we need to write the worker/client classes that should do the job: https://github.com/OpenMined/PySyft/pull/3803) + python3.8 adds some pretty nice annotations like: @finale (specify that this class should not be subclassed anymore), @overload, and also has some type checking. Here is my PR that waits for approves
- Falcon: did not had time to progress here :(
- Get copy: still waiting for review: https://github.com/OpenMined/PySyft/pull/3670 and here the syft-proto PR for the RequestCopyMessage: https://github.com/OpenMined/syft-proto/pull/130 -- the same, this is only to make the RequestCopyMessage ready for protobuf serialization)

SUKHAD
- PyFE: reading research papers. But final projects this week

RAVIKANT
- BFV scheme: 1 multiplication working!!
- Next step: needs relinearisation to do more.
- Exams coming.

ALAN
- Loading a deployed language model is working on virtual workers.
- Prepared some slides to explain illustrate the idea. Will find a way to communicate this

THEO
- Merging AriaNN piece by piece: remote exec merged
- Shaloop packaging: works for linux & macos!
- Private imaging: encrypted resnet18 output wrong results
