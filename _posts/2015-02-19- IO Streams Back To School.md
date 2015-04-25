---
layout: post
title: IO Streams Back To School
---

 Just a Helping note on IOStream because ppl are too lazy to learn, write and share (for free!, you codeholes). 
 <br/>
Annoyed by people whining about performance degradation, blaming issues from compiler, software library in terms of bandwidth,CPU,network latency etc.
while simply overlooking programming mistakes from their source code

POST CONTAINS STUBORN, DOGMATIC and POMPOUS VIEWS, don't care about your sentiment to issue!

![Try Again](/public/locals/slap001.jpg "Try Coding Again!")


 
### Basic C style IO and Low Level IO-library
Operating system provides low level API for writing files which happen to be implemented in C-programming language.
It includes low level functions such as open(2), read(2), write(2) etc. This functions write to file buffer
described by file descriptor. This low level work is done in form of "BYTES".
so call is going to transfer all bytes from buffer to file.

There is other form of API comes with C-library that does interesting work of formatting, locale, interpreting
bytes as Objects and more.
C-library  includes wrapper functions fprintf,printf,vsprintf which do formatting.

Performance Tip:

* While Writing to File say serializing object or index of document, write in binary rather that ASCII characters.
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

What is locale in IOStreams?
When we are dealing with money americans tend to use doller, english use pound and so on. In our case we have platform specific
traits,timezone traits etc. to denote in some format. local facets are objects that describe such characteristics in file representation.
Standard Stream objects	are larger in size due to formatting options,locale objects and book keeping variables.

####Stupid Assumptions

>Buffering inputs from stream is efficient

If data is in stream buffer then it is already in main memory, there is no point in creating new memory buffer and copy 
data from stream buffer to new buffer it is just very stupid!

>Order in which data is written in buffer is same as it appears, 

No way, as buffers are usually flushed on request or buffer full.
also sequence depends upon clients holding stream. Standard streams provide "hooks" for ordering this sequence. For example if one is working
with interactive console based application then every console write message should appear on screen before it accepts any inputs, and standard library gives that hook.

>Console streams are same as Standard stream. 

On Most of systems Virtual Consoles/shells redirect/dup(2) streams to standard stream.
Outputting to screen is not standard stream all the time nor do all standard streams go to console.

### FAST IO as Per Domain
#####Driver

#####Relational DBMS
RDBMS sees files are sequence of fixed or/and variable length records and indices. Algorithms operating on this records use iterator model
to fetch records. Reads dont create issues but writes do. say in record updates or joins. To create efficient model, iterators are placed on
primary buffer itself.

Database softwares usually create their own buffer manager to acheive performance. Buffer manager creates buffer pool which came with prefetch and replacement policy so their is abstraction over file IO.
#####Web Indexing

#####Computer Vision

### FAST IO for Competative Programmers


### TAKE AWAY

* IO Library are built upon Language Specification and are not part of language itself!

* Use Your OWN head to mock every usecase!

* Make No Implicit Assumptions when it come to performance

* CPUs in assumption must be Multicore.

* Design your OWN library for your TASK!

* Consider statically linked archives


### References
1.Technical Report on C++ Performance

2.Optimizing Software in C++

3.C++ Specification

4.Common sense :P better if yours!

