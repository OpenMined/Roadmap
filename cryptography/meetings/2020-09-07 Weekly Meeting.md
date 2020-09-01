### Update
The cryptography team will be split in 4 teams:
- HE
- SMPC
- FE
- and PSI!!

### Recap

SHARAN
- Reading in details the FE paper
- Getting familiar with the reading in the dark code!

MUHAMMED
- Public multiplication in RST which doesn't need correlated randomness
- Wait on George for private multiplication
- Refactor reconstruction / addition algorithm to optimize communication on RST
- Found a bug for + with torch tensor & FPT

GEORGE
- Solved the issue with Crypten tutorial with PyGrid
- Correlated randomness: investigating how to implement it. Pr coming next week!
- syft-proto: simplifying the generation of the definitions from the codes. Can we automatize?

ALAN
- Release will be in september!
- Working in Plans integration in the Pipeline for inference
- Adapting the CI to use language models with a Pygrid network
- Meeting an AI resident from microsoft about DP for transformer -> a research team for NLP?
- think about extending to topics like vision & audio

MICHAEL
- Rust binding almost done
- Java binding in progress
- Blogpost next week for PyVertical!
- Looking for someone with crypto experience

RAVIKANT
- Relinearization part implemented requires coefficient modulus changes

AYOUB
- Building a contribution guideline on TenSEAL
- Working on the client / server for TenSEAL: https://github.com/youben11/encrypted-evaluation : with an awesome CLI

BILAL
- Implementing on matrix encoding and transformation for convolution in C++
- Will be possible to bind to Rust and other language
- Working on a demo for CNN evaluation

IAN
- Discovering the code of TenSEAL!

THEO
- Max & argmax + SPDZ integration PR merged
- FSS little stuff in a PR under review
- WS: using get new workers + new PyGrid -> that's cool
- Handling errors forwarding acros WS workers
- Pygrid WS bandwidth is low ~10Mo/s
- Research in FSS : Rust implementation for equality
