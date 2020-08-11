### Recap

- PMs onboarding
- all 3 frameworks (syft.js, swift, kotlin) using PyGrid can execute plans
- pyDP -> release cross platform
- DP & Crypto cooperations

### Updates

ALAN
- Sentiment analysis tutorial ready!! Thanks to GC issues solving
- Pygrid integration to host models and pipelines 
- can we add a mechanism to register objects automatically for serde?

GEORGE
- Crypten: hook load_from_party 
- Crypten; playing with ONNX and hoe to mix plan and model evaluation in crypten
- Rm the wrapper
- code cleaning: ex: dosctring formatting & more 

AYOUB
- Crypten: try to train a model with crypten and jails but it is slow and diverging for the moment
- TenSEAL: fixing a bug about multiplying a vector of value with plaintext zeros 
- TenSEAL: bogdan cebere merged porting the cpp api to python -> will be in the next release

RAVIKANT
- Working on the decrypted part for FV homomorphic Enc.: I have completed the main code but still some problems to fix 
- Working also on kotlin-syft

BILAL
- TenSEAL: working on GitHub actions workflow for Windows but still some problems (maybe make issues)

SHARAN
- Remove support custom dtype in AST
- Fix move to same location 
- flatten and 1D ops weird bug
- More GC leaks tracking 
- Starting FE project

MUHAMMED
- Reimplemented max function but pbs: GC & flatten
- work avg & max pooling, working on padding ; GC issues

YUGANDHAR
- mul and div issue: shape mismatch issue 
- secureNN with n workers merged -> more tests so slower
- work on truncation issue 
- interested by FALCON

THEO
- grid & web sockets discovery & PR
- many message for forcedelete -> can we optimize or batch?

