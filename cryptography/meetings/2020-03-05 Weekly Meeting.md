### Recap
- OpenMined Research
- Syft Core team
- Syft.js achievements 

### Updates

AJAY
- SyftCryptTensor: PR coming

ANDRE
- Matrix inversion: normalizing wasn't working well -> needs higher precision than 3. 3 doesn't work but 4 is great!
- Investigate the shape of the matrix influence on the scaling factor.
- Will open PR with those changes

YUGANDHAR
- dtype in precision.py (int32 & long64)
- Issues with manipualting & serializing 2**64 field -> overflow error
- SecureNN in int32 
- Thinking about gsoc project!

GEORGE
- Crypten: working on having computations using Plan. Processes are blocking somewhere
- tanh PR updated -> ready
- 2 students will join to work on PySyft

ALAN
- Gsoc project released: create a language model from several remote datasets
- Sentiment analysis using SyferText on imdb 
- Working on sending a Tagger (ex: tag each stopwords remotely in a provide dataset, etc)
- Thinking about integration of PyGrid in SyferText
- Thinking about using SplitNN to train some parts of the net on the worker side and other in the encrypted world
- First sync of the team!

AYOUB
- Crypten: safe env: we can train models using crypten + pysyft!
- But models are still static: can't define the classes dynamically.
- TenSEAL: discussed with the head of SEAL: CKKS (levelled-homomorphic encryption (HE)) which supports real numbers (instead of BFV which needs fixed precision and doesn't have very practical bootstrapping).
- Suggestion to mix SMPC & HE (see Gazelle paper)
- Instead of boostrapping, add interaction: request the client to decrypt intermediate masked values to refresh the ciphertexts.

THEO
- PR to update for syft-core
- Working on some topics with Silvia, Adam, Muhammed & Yugandhar
