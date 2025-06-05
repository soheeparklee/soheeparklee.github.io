---
title: Interview
categories: [JAVA, JAVA_Basics]
tags: [] # TAG names should always be lowercase
---

## ✅ Charecteristics of Java

- OOP

  - Polymorphism: single function can behave differently depending on the context, `overriding(dynamic, runtime)` and `overloading(static, compile time)`
  - Abstract: get common fields and methods of classes, `interface`
  - Inheritence: extends parent class field and method
  - Encapsulation: field and method in a class, `access modifiers` to limit access

- object is created with `new`
- and saved in `heap`, where `GC` cleans unused objects
- call by value, no pointer
- multithread
- runs on `JVM`, so it can run on all OS with same code

## ✅ Limits of Java

- slower
- JVM needs to `compile` byte code
- when GC cleans unused `instances`, calls `Stop the world`
- `Stop the world`: when GC is running, all threads except GC stops running

## ✅ How Java is run, JVM

<img width="589" alt="Image" src="https://private-user-images.githubusercontent.com/97790983/451853809-590c6fcc-4401-4137-8417-6454c32d15c4.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDkxMjM0NTgsIm5iZiI6MTc0OTEyMzE1OCwicGF0aCI6Ii85Nzc5MDk4My80NTE4NTM4MDktNTkwYzZmY2MtNDQwMS00MTM3LTg0MTctNjQ1NGMzMmQxNWM0LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA2MDUlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwNjA1VDExMzIzOFomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTlhMGExMmQyMmM4ZDM2NTdjM2YwY2E1NTE4YzEzMmE4ZWFhNDAzNzFkNGIwZjI4NzY0ZTYzMWFlYWYxMzI1YjcmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.al5aHuABVLzhx3WghmP9FPe0XUsJg8SGgx3yXNh5UPQ" />

**1. Java compiler javac**

- developer writes `.java` `source code`
- `javac(java compiler)` will convert `.java source code` to `byte code` which is stored in `.class`
- `.class` file will be handed over to `class loader`

**2. Class Loader**

- `class loader` will **dynamically** load/link files into `runtime data JVM memory area`
- `loading`, `linking`, `initialization`
- `class loader` ensures classes are loaded **on demand**, saving memory
- dynamic loading: 클래스/리소스를 필요한 시점에 메모리에 load

**3. Runtime data area**

- `runtime data area` is memory managed by JVM
- `method area`: class level data, static
- `heap`: `new` instances, objects, arrays, shared across threads
- `stack`: local variables, parameters, each thread has own stack
- `Program Counter(PC)`: keep track of next instruciton for each thread
- `Native Method Stack`: non-Java code

**4. Execution Engine**

- `execution engine` will execute the `byte code`
- `interpreter`: reads and execute `byte code` line by line(slow)
- `Just-In-Time(JIT) Compiler`: compile bytecode to native machine code for frequently used code blocks(fast)
- `Garbage collector`: reclaim memory from objects that are no longer in referenced

## ✅ What is Java Byte Code?

- code that `JVM` can understand
- compiled through `javac`

## Java interpreter 🆚 JIT compile

- Java interpreter: reads java code line by line
- JIT compile: compile the whole programming code into executable byte code

## ✅ Java versions?

## ✅ JDK and JRE?

## equals() 🆚 ==

## equals() 🆚 hashCode()

## ✅ toString() 이란?

## ✅ Java의 메인 메소드는 왜 static일까?

## ✅ Constant and Literal

## Primitive type 🆚 Reference type

## ✅ Java serialization

- the **conversion** of the state of an object into a byte stream
- change `object`to `byte stream`
- to be able to transmit as file, memory, database
- so we can then save to a database or transfer over a network
- convert object format so it can be transmitted

## Overloading 🆚 Overriding

## ✅ What is polymorphism?

## ✅ What is inheritence?

## ✅ What is combination?

## Interface 🆚 Abstract class

## ✅ final keyword in java

## ✅

## ✅
