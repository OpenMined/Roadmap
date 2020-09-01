### General Announcements
- Everyone will have or share a milestone :visage_légèrement_souriant:
- All sub team should have or share a Kanban + milestones
- Re-organisation of the cryptography team coming soon!
- Our dedicated writer is coming soon!

### Recap
MICHAEL
- PSI is currently used in PyVertical
- Can PSI be used in another place?!
- For secure inference, what do we have? HE vs SMPC

ALAN
- Working on the next release 0.1.0
- Bugs found in PySyft about SMPC
- Solving stuff linked to sending pipelines

BILAL
- Release 0.1.0 for TenSEAL with logistic regression!!
- Optimisation on CKKS for polynomial ops
- exponent on CKKS vectors which consumes less mult. depth
- Next milestone: convolutional layers

AYOUB
- Demo of logistic regression with TenSEAL!

BOGDAN
- TenSEAL context serialization: add protobuf support, was able to overwrite the methods for deepcopy and pickle to use protobuf.

RAVIKANT
- Linearization operations: still under debugging
- Reading the code on how to create new tensor types

GEORGE
- Merge crypten integration in master: pytorch 1.4, rm python 3.6
- Help Muhammed with FALCON -> Milestone

MUHAMMED
- Made a new tensor type to implement the replicative secret sharing scheme that falcon uses
- we can share a secret and reconstruct it, add two secrets or add secret to plain text so far

THEO
- Opened PR on optimized conv & maxpool
- Building his milestone for FSS
- Fighting against the Batch Norm
