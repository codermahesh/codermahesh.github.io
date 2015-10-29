---
layout: post
title: Mocking OpenCL-C++
---

Khronos group just came up with newest specification in OpenCL based on new C++ 14.
This specifications allows programmers to write their code in restricted C++, and so we got chance to take
hands on this new deal.


OpenCL-CPP is mostly based on core features of OpenCL with additional Object Oriented swing on it. Even though
current specification is provisional, as normal developer it bursted me out for number of reasons, which led to this post.


Most of GPU/DSP vendors like to put machine level control to programmers because of core PERFORMANCE reason. Keeping in mind
this, OpenCL specification worked out very well. While designing compiler "C-language" becomes inevitable choice. C stands in
procedural language context, data and functions can be managed easily by means of Opaque types. While in case of C++, Objects are 
bound to procedures and object have states! so designing compiler with this approach is no longer bookish.
While going through specification, several times it occured that OpenCL-CPP spec looks more like OpenCL-C in different scenerios,
this does not clear their intent. Below i have listed few issues that govern use of C++ for doing exactly what spec means to do,
in some what different orientation. 
   
 
### 1. CL Types
* Type semantics

Consider case of Builtin Image Types.

	template <typename T>
	class Image2D{
		public :
		void write(int2 coordinate, T color);		
	};


It makes sense to write "Image2DCordinate coord" than "int2 coord", as C++ offers zero abstraction overhead.

> Why int2 in first place?

   According to people worked on this before, it gives clear idea on 32 bit coordinates so that all implementors has to support so
as to maintain conformance and portability.

> What's wrong with it?
Implementor I has 32 bit coordinates, sounds good, holds good. Implementor II comes with 16 bit coordinates,With trucation of bits in compiler
works good. Implementor III came up with 64 bit coordinates and suddenly all failed! 	 

> Solution
>>  Best Feature in C++ and Design,Use of Abstraction

* Ambiguity of Type Layout

Cosider type halfn from spec. 
```
	union{
		
		struct half_{
			ushort mantissa : 10,
			ushort exponent :  5,
			ushort sign     :  1
		}__attribute__ ((__packed__));

		ushort halfbits_;
	}half;
```

Types like half put compiler writer into serious trouble as they are not conventional. not to forget simulating half is funny!
Only choice here is Taking control over AST and IR specification.

After putting prolong thought into it, one could easily strike on fact
Intermediate Representation is machine independent, but It has directly mapped semantics with machine level working e.g. Types,Control Flow
so When "they" told you Machine Indepedent code, it was lie!!!

Although Khronous has given many hints in SPIR-V to accomadate that,C++ to SPIR-V still comes with few nasty questions,So solution add another
layer of Abstraction?? 


* Comparing Real Values


        float x = 0f, y = 0.001f
        if(x == y){
        ....
        }


* Saga of && and \|\| on Values


* Copy &\| Assignment on Built-in types


* Casting Ops

	Consider vector class Int2 that need to be converted to uint2 by typecasting. Specification mentions function
convert_cast to achieve same. this function is free template function. As per Spec writer, We are adopting C++ for Object-oriented programming 
model, so obious choice of casting would be overload of operator() to maintain integrity. 

	/* To be*/

        template<typename T>
        T convert_cast<T>(uint2&);

	/* or not to be */

        class uint2{
          int2 operator()(uint2&); 
        };

	and the story continues with isEqual function and == operator.


### 2. Macro defs

Just like opencl-c, this spec contains macros which give sheer advantage of "token replacement". This processing is semantically impaired
and has been quite a pain. With new C++ we have features like enum classes and constexpr which can easy many of this issues.

Conventional enumarators are replaced with enumarator classes which provide scoping details, but spec does not seem to encourage it.

To reduce compilation, using pre-compiled headers is obious choice, Nature of this macros is vanished for pre-compiled headers, so cheers to 
few more bugs!!.

### 3. Promiscous
*  C++ supports Object oriented programming, but c++ is not exactly OO programming language.
*  Specification asks whether to support Iterators on container types. 