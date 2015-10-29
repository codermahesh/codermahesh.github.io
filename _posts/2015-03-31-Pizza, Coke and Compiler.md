---
layout: post
title: Pizza, Coke and Compiler
---
@21:00 hr  still busy hexagon, rattled with issues, we questioned issues in  computer science, typically  compiler.
Just light on  few sections. [organised content] 

> What "people" know about compiler? <br/>
>Compiler is software that converts source programming language to machine level/ assembly language.

>What "people" mean to say "exactly" <br/>
>Compiler is software that creates "semantically equivalent transformation" on source language to target language domain.

Weird Fact but true!

What Happens when we compile...

![Traditional Compiler](/public/locals/TraditionalCompiler.svg "Try Coding Again!")

What happens when web server serves...

![Internet Model](/public/locals/InternetModel.svg "Try Coding Again!")

viola! Everything that computer does has same FLOW! :D

####Specious Thoughts 
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

*Optimization reduces code!*

Almost right!, Optimizations tend to reduce code, lesser code, minimum processor power up time, less heat.
although some optimizations increase code length say, auto vectorization which increases code size by adding code for runtime checks,
guards etc. keeping in mind it increase performance several times compared to code length.


*Trees,Directed Acyclic Graphs...*

Misconception at its best! Trees are graphs without cycle, so as Directed Acyclic graphs but in DAG node can have two parents, in tree they don't!

*Low Heat Instructions* 

Here is neat instruction from hardware designer 

"During optimization choose instruction"s"  those emit less heat!"

Optimizations on front line instructions in peep-hole expands code into low heat instructions.This is wasteful attempt, this expansion over huge code tend to keep silicon power on for longer time than usual. weird but true!, been there instrumented that!

#### What book skipped?
1.Code Instrumentation and Profiling is as strong issues as Compiler itself. Profile-evaluate-re-engineer would be the perfection.
Hot path identification is used in runtime optimizations.

2.Runtime engineering with compiler

