### General announcement

Cryptography team grows!! It now contains 3 crypto groups:
- SMPC group led by @George Muraru 
- Homomorphic Encryption group led by @Ayoub Benaissa 
- Functional Encryption group led by @Syzygianinfern0 
This will help us to scale in the coming months! :slightly_smiling_face: 


### Recap

ALAN
- Working on the release: creating pygrid nodes, need to host workers on AWS
- Tests: new tests added in the CI but they need to download language models -> this is being optimized
- Alan working on plans to add models in the pipelines
- Gave a talk at MLH about syfertext
- Creating an NLP research group
- OpenMined conference: Tutorial about SyferText 0.1

BOGDAN
- Merged serialization for TenSEAL context & tensor
- Worked on bazel build
- Improve matmul with multi-threading 

AYOUB
- Ciphertext with the 0 value bug from SEAL: other bug corrected on this
- Serialization and remote evaluation! Using Fast API. What about a permanent connection using grpc?

BILAL
- Working on convolution: done! Matrix need to be reshaped. With >1 kernel we currently need 2 multiplications, otherwise 1.
- Results in 5s on a CNN!
- Clean tutorials maybe next week

RAVIKANT
- Mul with the variant of the FV scheme: PR ready!
- Relinearisation op: need to do some change in param validation
- Then the encryption part will be completed!

SHARAN
- Exams are done!
- Scheduling what still need to be done on the FE scheme (the decryption part) 

GEORGE
- Crypten merged in master! included in v0.2.8
- Support for python 3.6 dropped
- working on using Crypten tutorials with pygrid

FALCON: made new issues | working with Muhammed 
- Working on correlated randomness

THEO
- Finally packaged my lib using Rust!
- Big PR about FSS merged
- PR opened to optimize max/argmax
- PR opened to refactor SPDZ

Two guys stole a calendar. They got six months each.
