### Recap

- Syft Core: Turning Plans in Protocols
- Concrete usecases on SyferText & Research teams -> new bugs :)
- FALCON is out

### Updates

SHARAN
- Working a lot on GC issues, including inplace operations
- Working on size hooking
- "custom" dtype fix

SUKHAD
- Backdoor FL: should be ready for test for next week

ALAN
- Training after GC fixes: the number of objects in workers don't increase, but there is still a leak. Cryptoprovider ? Use debugger in PyCharm ? 
- Pygrid <-> Syfertext : fixed the remote sharing, working on get() remote AST
- Pipeline coming along

RAVIKANT
- Working on the decryptor part
- Redesigning the project with new SEAL 3.5
- New release manager!

AYOUB
- TenSEAL: automatic workflow to publish the wheels to pipy (for macOS Catalina, Linux, Windows on the way)
- TenSEAL: PR porting the whole api c++ to python
- CrypTen: utility to send a pytorch model and build a crypten model 
- Crypten computation with jails now integrated with plans. 
- Next step: have a full pipeline to train a crypten model using the jail.

GEORGE
- CrypTen: Lots of rebasing 
- CrypTen: wokring on temporary hooking of crypten tensor and module to work together with jails
- Removing the wrapper: 4 tests still failing

THEO
- Function Secret Sharing - go to benchmarking
