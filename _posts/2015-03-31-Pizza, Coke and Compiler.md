---
layout: post
title: Pizza, Coke and Compiler
---
@21:00 hr  still busy hexagon, rattled with issues, we questioned issues in  computer science, typically  compiler.
Just light on  few sections. 

> What "people" know about compiler? <br/>
>Compiler is software that converts source programming language to machine level/ assembly language.

>What "people" mean to say "exactly" <br/>
>Compiler is software that creates "semantically equivalent transformation" on source language to target language domain.

### Compilers etc.
1.Traditional Compiler -- Binary/ Object Code  creation

* Static Compiler
* Interpreter	
* Just in Time Compiler	

2.Source-2-Source
--Convertion between two programming languages. say Cpp => Java

3.Configuration-2-Source 
--Generative Programming, accurately just subset of it. taking configuration about code to generate.
Tablegen
Google MockTests

4.*Virtual Machines* 
--Tight couping between compiler backend phases. online compilation

Trace based Compilers
Interpreters
Source-2-Source --
Configuration-2-Source  --  some sort of Generative Programming

Virtual Machines


link time opts and runtime opts
High level Virtual Machines
Platform JVM .Net
Native VMs
Garbage Collections


####\~ Specious Thoughts
#####Expression Tree

*There is no such term "Expression Tree"!*

Source language inputs are "Parsed" for validity in lexical and semantic constraints. Parsers use "Concrete Syntax Tree" to check semantic validity,
which literature calls "Parse Tree". Parse Tree are implementation for Source language grammer.

To convert valid input language to "target languague" (not target yet!) one has to create abstract computation which can be operated machine independently for optimizations and then can be mapped into machine dependent form(now target :D ). This abstract computation is represented in 
tree form, "Abstract Syntax Type".

There are three types of Notation for expression, (Prefix,infix and postfix). 
Intermediate representation for expressions can be written in stack machine form, three address code, quadraple forms "linearly".
Intermediate representation for expressions are practically trees or directed acyclic graphs in  "Graphical" formats .
so no "Expression Tree" !

Optimizations
Trees and DAGs
Low heat Instructions
C++, Java Compare

Compilers and Computer Security
Compilers and Performance through Programming

Hot Topics

Data locality Optimizations
	Affine transform 
	Pipeline 
Multicore optmizations

What is not told
	intrumentation
	Cachegrind
		
DSLs
1.Spreadsheet
2.Image
3.GraphViz
4.Tablegen 

Cool Stuff
    Battle Code
    Xtext
    emscripten
    webCL
    
