### Recap


### Updates

ADAM
- Implement tutorial intrusion system detection in the network (applied to Docker) 
- Working on the roadmap of my team

AJAY
- Will add tests to SyftCryptTensor in the PR
- Will dd more functionality

ALAN
- Working on pipelines in SyferText: pipe of remote transformations on the data (token, tag, etc). Need to break in 2 pipelines: one to be send entirely to the remote worker (should use Plan !) for pre-processing and one to be used like classic SMPC.
- Interested about SplitNN

GEORGE
- [PySyft] Got the tanh sigmoid merged into master (thanks Theo for the review -- also added test for it and the possibility to choose between sigmoid and tanh)
- [PySyft] Will start looking into: https://github.com/OpenMined/PySyft/issues/3131 (I assigned the issue to em)
- [CrypTen] Got the plans working with a simple "CrypTen function" where there are 2 workers and they add the tensors and call "get_plain_text"
- [CrypTen] Working on integration Ajay MPCTensor (for CrypTen) with what I have -- I got an idea on how will work, but need to continue writing code to make sure that some parts of the PySyft code is doing what I think it is doing

AYOUB
- CrypTen: working on conversion from Syft models to Crypten models. At stake: keeping an equivalence to update back parameters after training happened
- TenSEAL: still reading on Gazelle paper. 
- Working on the master thesis

JASON
- Working with the syft-core team to refactor messages & serialization
- Started to look at the gsoc project: a ZK proof from scratch in PySyft

YUGANDHAR
- Good progress of dtype & field in FPT & AST. SecureNN requires custom dtype, that will only be available for AST internally
- Working with overflow & Protobuf serialization

THEO
- FSS - x8 faster than SecureNN using @tracer & Plans in a new way
- Having added a Crypto Store (forgot to mention it!!) to workers
