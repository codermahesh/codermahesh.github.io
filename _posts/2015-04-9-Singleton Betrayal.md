---
layout: post
title: Singleton Betreyal
---

So test ran several times in past week and failed thrice, undefined behaviour at first, once again mud ball was in court!
Debugging started with failure scenario almost 100:3, with absolutely no clue, tons of guess work. Most difficult task
was to regenerate fail case, having spent more than 10 hr finally come up to issue.

Test did not failed because of bug in core but due to bug in architecture of environment under which test ran.
While running test on server created multiple thread to run test in parallel. ComputeDispach thread forked threads
with sharing "Context" objects. This context had exactly same data content but had different addresses. Context being singleton
class, supposed to create only one object but it appeared to create two! 

So came up with new questions and design considerations listed below

Questions

1. Singleton behaviour in multi-thread
2. Singletons in managed/ virtual platform [jvm]
3. Singletons in shared library
4. Singleton Object placement in memory [copyout-immutable,kernel objects]
5. Singleton object destruction
6. Singletons for loosely coupled memory system  [e.g. Multiple web service endpoints with same Application Context]
7. Singletons on interpreter
   
Possible designs

* Atomic Initialization for Singleton, typically registry based singleton should have atomic operation of registration.
* Immutable Singletons should be de-serialized from lock-based file.s
* Forcing static initializations by static code snippets.

Design Rationale

* Unique Point of Access is behavioural constraint, single object in memory is data constraint
w.r.t. GoF pattern. 
So singleton ends up having static "creator" method and single static "pointer to object".
Monostate tend to have same features but different architecture.
* Kernel locks and its abstractions are neat way to implement singleton constraints keeping in mind about "Compulsory" destructor execution
whenever object is destroyed.
* Registry should use data structures those are thread-safe.   

Implementations

[Singleton_GOF_Implementation](https://github.com/codermahesh/design-lib/blob/master/C-Pattern/Singleton/Static-SingleClass.cpp)

[Registry based Singleton](https://github.com/codermahesh/design-lib/blob/master/C-Pattern/Singleton/Static-DerivedSupport.cpp)

[Monostate](#)

[ThreadSafe Singleton](#)
