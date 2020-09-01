### General announcement
- New federated learning dev team!
- New milestone: FALCON

### Recap

AYOUB
- 100 stars in TenSEAL
- matmul in TenSEAL optimization (1 minute -> 15s) using multi-threading
- <1s on eval on small neural networks

BILAL
- Working on convolution: our method allow multiple layer of convolution but requires one interaction (you send back the tensor blinded). Reshape can't be done on ciphertext.
- Convolution time: <0.4s !!
- CNN experiment coming

BOGDAN
- TenSEAL context serialization with protobuf merged!
- working on tensor serialization

MICHAEL
- PSI: working with a app partner for contact tracing still going on
- Working for java bindings!
- Writing rust bindings for integration in syft core 
- Set up a discussion about PSI in the next meeting

RAVIKANT
- Working on multiplication op, because relinearisation doesn't work as such
- using multiple coefficient modulus instead
- Multiplication almost done!

ALAN
- Incremental dev phase to reach the milestone
- PySyft issue: about serialization of some workers
- Setup a meeting for better explain the global stack

THEO
- batchnorm: working!
- resnet18 working in 120s 
- FSS final PRs coming
- Rust experiments for FSS

> What is bigger than GPT-3 ? Encrypted GPT-3
