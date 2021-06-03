# 1. Translator

## a. Definition
An S -> T translator accepts code expressed in source language S, and translates it to equivalent code expressed in another (target) language T

## b. Examples:

* Compilers - translates high level code to low level code, e.g. Java -> JVM
* Assemblers - translates assembly language code to machine code, e.g. x86as -> x86
* High-level translators - translates code from one PL to another, e.g. Java -> C
* Decompilers - translates low-level code to high-level code, e.g. Java JVM bytecode -> Java

# 2. Interpreter

## a. Definition

An S interpreter accepts code expressed in language S, and immediately executes that code. It works by fetching, analysing, and executing one instruction at a time.

## b. Advantage

- Great when user is entering instructions interactively (think Python) and would like to get the output before putting in the next instruction. 
- Also useful when the program is to be executed only once 
- or the program requires to be portable.

## c. Disadvantages

* Interpreting a program is much slower than executing native machine code
* Interpreting a high-level language is ~100 times slower
* Interpreting an intermediate-level (such as JVM bytecode) language is ~10 slower
* If an instruction is called repeatedly, it will be analysed repeatedly - time-consuming!

# 3. Differences

## a. Behaviour

* A compiler translates source code to machine code, but does not execute the source or object code.

* An interpreter executes source code one instruction at a time, but does not translate the source code.

## b. Performance

* A compiler takes quite a long time to translate the source program to native machine code, but subsequent execution is fast
* An interpreter starts executing the source program immediately, but execution is slow

# 4. Interpretive compilers

## a. Definition

An interpretive compiler is a good compromise between compilers and interpreters. It translates source program into virtual machine code, which is then interpreted.

## b. Behaviour

An interpretive compiler combines fast translation with moderately fast execution, provided that:

* VM code is lower than the source language, but higher than native machine code
* VM instructions have simple formats (can be quickly analysed by an interpreter)

## c. Example

JDK provides an interpretive compiler for Java.

