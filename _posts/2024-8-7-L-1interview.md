---
title: Interview_GC/StringBuilder/
categories: [JAVA, JAVA_Basics]
tags: [] # TAG names should always be lowercase
---

## ✅ Garbage Collection?

> Garbage collection <br>
>
> > When Java is run on JVM, manage heap <br>
> > Stop the world, major GC <br>

💡 <https://soheeparklee.github.io/posts/JAVA_JVM/#%EF%B8%8F-garbage-collector-1> <br>

## String Builder 🆚 String Buffer

> Difference between stringbuilder and stringbuffer? <br> > <br>
>
> > 같은점: mutation, APIs like append() <br>
> > 참고로, string is immutable <br>
> > 다른점: <br> > > <br>
> >
> > - String Builder: synchronization ❌, fast in **single** thread <br>
> > - String Buffer: synchronization ⭕️, **multithread** <br>

💡 <https://soheeparklee.github.io/posts/JAVA_library/#-string-class> <br>

## ✅ Memory in JAVA

> How is JVM memory? <br> > <br>
>
> > method area: (class loaded) static, method, final <br>
> > heap: (runtime) instance, array <br>
> > JVM stack: (compile) local variable, parameter <br>
> > PC register: (thread created) <br>
> > native method stack: not java <br>

💡 <https://soheeparklee.github.io/posts/JAVA_JVM/#-jvm-runtime-data-area-%EC%A0%80%EC%9E%A5> <br>

## Overloading 🆚 Overriding

> Overloading and Overriding? <br> > <br>
>
> > ✔️ Overloading: <br>
> > method name 🟰 <br>
> > parameter ✖️ <br>
> > return type ✖️ <br>
> > when need several <br>

<br>

> ✔️ Overriding: <br> > <br>
>
> > method name 🟰 <br>
> > parameter 🟰 <br>
> > return type 🟰 <br>
> > need inheritence from parent <br>

💡 <https://www.geeksforgeeks.org/difference-between-method-overloading-and-method-overriding-in-java/> <br>

## Abstract class 🆚 Interface

both used for **abstraction** <br>

<img width="569" alt="Screenshot 2024-08-07 at 13 19 58" src="https://github.com/user-attachments/assets/0635c5eb-bfe3-4838-b002-8aab0e2c8a6a">

> Abstract class <br> > <br>
>
> > extends <br>
> > cannot be instantiated directly, serves as blueprint for other classes <br>
> > class can inherit from only one abstract class <br>
> > method, properties can have any access modifier <br>
> > can have variables <br>
> > need to have minimum one abstract method <br> > > <br>

> Interface <br> > <br>
>
> > implements <br>
> > set of methods a class must implement <br>
> > class can inherit multiple abstract class <br>
> > method, properties: public <br>
> > no variables <br>
> > inheriting class should override all interface methods <br>

💡 <https://www.geeksforgeeks.org/difference-between-abstract-class-and-interface-in-java/> <br>

## ✅ Generic

> parameterized types <br>
> allow type to be a parameter to method, class, interface <br>
> have predefined type <br>
> Inside <>, only `reference type`(class, interface, array) is possible. <br>
> To use `primitive types`, use `wrapper` <br>

## ✅ Access Modifier

- public
- protected: inherited
- default: same class, same package
- private

## Vector 🆚 Arraylist?

> Vector <br>
>
> > Synchronized. <br>
> > If one thread is working with vector, other thread cannot have vector <br> > > <br>

> ArrayList <br>
>
> > Unsynchronized <br>
> > several thread can work on arraylist <br>

## ✅ Serialization?

> JSON ➡️ Java, visa versa <br>

💡 <https://soheeparklee.github.io/posts/l-serialization/>
