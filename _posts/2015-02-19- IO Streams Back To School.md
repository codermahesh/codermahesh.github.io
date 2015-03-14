---
layout: post
title: IO Streams Back To School
---

 Just a Helping note on IOStream because ppl are too lazy to learn, write and share (for free!, you codeholes). 
 <br/>
So annoyed by people whining about performance degradation over issues from compiler,bandwidth,CPU,network latency etc.
while simply overlooking programming mistakes from their programming.

POST CONTAINS STUBORN, DOGMATIC and POMPOUS VIEWS, NOT INTENDED FOR CHILDREN!

 
### Basic C style IO and Low Level IO-library
Operating system provides low level API for writing files which happen to be implemented in C-programming language.
It includes low level functions such as open(2), read(2), write(2) etc. This functions write to file buffer
described by file descriptor. This low level work is done in form of "BYTES".
so call is going to transfer all bytes from buffer to file.

There is other form of API comes with C-library that does interesting work of formatting, locale, interpreting
bytes as Objects and more.
C-library  includes wrapper functions fprintf,printf,vsprintf which do formatting.

Performance Tip:

* While Writing to File say serializing object or index of document, write in binary rather that characters.
* While reading file read file contents in  object memory.

Use macros if you need to debug  file contents
<br/>
 #ifdef   DEBUG_ON <br/>
 	//formatted write <br/>
 #else<br/>
 	//binary write<br/>
 #endif<br/>
 
Writing your own functions over  low level  functions always  best solution.
CS101 says file is persistent storage while sometimes there is need of in memory files,
it is easy to rely on low level functions  and create  memory buffers as files.

 		 	
### C++ IO Streams
C++ IO functions as part of "Standard" Library. That is clear indication this as language abstractions over basic low level
function. This standard functions are for "AAM" people. People who care about issues implemented in this 
library should be carefully managed in their own implementations.


[Head to the readme](https://github.com/poole/lanyon#readme) to learn more.

### FAST IO as Per Domain
Relational DBMS

Driver

Web Indexing

COmputer Vision

### FAST IO for Competative Programmers

Lanyon is developed on and hosted with GitHub. Head to the <a href="https://github.com/poole/lanyon">GitHub repository</a> for downloads, bug reports, and features requests.

### TAKE AWAY

* IO Library are built upon Language Specification and are not part of language itself!

* Use Your OWN head to mock every usecase!

* Make No Implicit Assumptions when it come to performance

* CPUs in assumption must be Multicore.

* Design your OWN library for your TASK!

