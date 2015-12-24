---
layout: post
title: Hail Arrays!
---
  Having performance beast on back, forces one to use C/C++, mostly because of "native" code. For decades
guys are working on C++ to do all kinds of stuff and they came up with bunch of guidelines. One of which is 
striking one. "Data Locality"!
 Performance Crazy programmer can write their programs with data caching in mind and get more throughput
 on exsiting machines but not maximum all times. While designing compiler this issues came up with substance, hence post!

### So arrays?
1.Always Prefer contiguous over linked/nonlinear structuring.
2.Always consider cacheline size and array size, more aligned data, high performance code.
3.Get this Woodo of Arrays!
FOllowing are some examples of using arrays.


		/*Simple Static Array  -- Allocated on Stack */	
		char a0[8];

		/*Not so Simple Static Array  -- Allocated on Stack */	
		int a1h;
		char *a1 = (char *) &a1h;

		/*Simple dynamic Array  -- Allocated on Heap */	
		char *a2 = (char*) malloc(sizeof(char) * 8);	

		/*Woodo Static Array  -- Allocated on Stack */
		template<typename T,size_t N>
		class sarray{
			private: T data[N];	
		};	
		Woodo::sarray<char,N> a3;

		/*Woodo Dynamic Array  -- Allocated on Stack */
		template<typename T,size_t N>
		class darray{
			private: T* data;
					 size_t capacity = N;		
		};	
		Woodo::darray<char,N> a4;


Given this kind of implementations we are considering optimizations not just in data locality
but in vectorized operations. Almost every single system made today has vector unit inside it.
either SSE,AVX and/or CPU SIMD or GPU SIMD. Beast that we address here is auto-vectorization.

To detect this vector operations, one has to compute how this array locations are access in program
so as to find potentially parallel code segments. Compiler calculates Iteration Space for input source 
and replaces existing code with vector instructions. and hence Performance.

For above code, we should expect  same beahviour for all, but that is not true. Why not?
1. For calculating Iteration space we need to know starting "Lvalue" (not going with address this time :D )of Array and its length.
so a0 and a3 are ok. a1 is sincerely uneducated about arrays and structs ;). For a2 here comes drama
when we say 

	a0 :  a[3]         it refers to  *(a.Lvalue + 3 *(datatye_size of a))

    a2 :  data[3]      refers to  *(data.Rvalue + 3 *(datatye_size of a))

Vectorizer need to spend more heuristic to determine pointer is iterating array, more effort and complexity
and not always implemented with all compilers.
same issue with a4.

2.Allocations and Pointers

Allocating array statically is easy candidate vectorization because at compile time space can be iterated.
Having pointers pointing to arrays can be cumbersome,

consider code


		int a[128]; 
		int* ap = &a[64];
		for(int i = 0 ; i < 32 ;++i)  a[i] = a[64+i] + ap[i];   		


This is typical code of overlapping vectorization, and needs severe rewrite.

3.Templates and Compiler Directive
	Implementations a3 and a4 are special, they provide control to implentor to direct compiler to create vector 
	code. more over as data is private, they avoid overlapping vectorization issue too!

### Tools and References
1. perf
2. cachegrind
3. C++ spec
4. Modern COmpiler Optimizations
