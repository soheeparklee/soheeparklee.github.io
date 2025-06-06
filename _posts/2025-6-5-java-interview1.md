---
title: Interview_Java, JVM, OOP
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

## Java interpreter 🆚 JIT compiler

- Java interpreter: reads java code **line by line**
- JIT compile: compile the **whole** programming code into executable byte code

## ✅ Java versions?

- Java8: lambda, StreamAPI, Optional(solve `NPE`), LocalDateTime
- Java11: `var`(지역변수 타입 추론), new String methods `isBlank(), strip()`
- Java17: `Record` class, `Sealed` class

## ✅ JDK and JRE?

- **JDK**: Java Development Kit ➡️ for developing with Java
  - tools for **developing** with Java, `Java compiler`, `debugging tools`, `JVM`
- **JRE**: Java Runtime Environment ➡️ for running Java
  - environment for running Java
  - to **run** Java, only need JRE(코드 실행만 할꺼면 JRE만 필요)

## equals() 🆚 ==

- `equals()`: value to be same
- `==`: value and memory reference adress to also be same

## equals() 🆚 hashCode()

- `equals()`: compare value of objects
- `hashCode()`: get unique hash of value
- override `equals()` and `hashCode()`: if hashcode is same, consider objects to be same
- if only override `equals()` but not `hashCode()`: same object might have different hash code, might consider two objects to be `equals = false`

## ✅ toString() 이란?

- return as `string`
- if override, 이쁘게 `string`으로 format해서 출력
- default will be `className@16bitHashCode`

## ✅ Java의 메인 메소드는 왜 static일까?

- if `static`, saved in `method area` instead of `heap area`
- if `static`, can call method without creating instance
- thus, program **entry point** without needing an object
- JVM can call `main method()` without creating an object
- so that `main method()` can run when class is created

## Constant 🆚 Literal

- `constant`: final, does not change
- `literal`: actual value written in the code

```java
final double PI = 3.14;  // constant
int x = 10;   //literal
```

## Primitive type 🆚 Reference type

- `Primitive type`: basic data type, `int`, `char`, `double`
  - saved in `stack`
  - holds `actual value`
  - cannot be null
- `Reference type`: objects and arrays `String`, `Integer`, `Double`
  - saved in `heap`
  - holds memory address
  - can be null
  - has methods

## ✅ Java serialization

- the **conversion** of the state of an object into a byte stream
- change `object`to `byte stream Json`
- to be able to **transmit** as file, memory, database
- so we can then save to a database or transfer over a network
- convert object format so it can be transmitted

## Overloading 🆚 Overriding

- **Overloading**: define another method with same name, but different parameters in single class
- **Overriding**: child class redefines inherited parent method

## ✅ What is polymorphism?

- single object can have different types
- parent class can be converted into child class type

```java
Animal[] animalArr = new Animal[10];

animalArr[0] = new Tiger();
animalArr[1] = new Dog();
animalArr[2] = new Lion();
animalArr[3] = new Elephant();
```

- 👍🏻 code reusability, OCP(open to extension)

## ✅ What is inheritence?

- IS-A
- child class extends parent class, overrides

```java
//Dog IS-A Animal

class Animal {
  void eat() {}
}

class Dog extends Animal {
  void bark(){}
}

Dog dog= new Dog();
dog.eat(); //inherited from Animal
dog.bark(); //defined in dog
```

## ✅ What is composition?

- HAS-A
- contain references to other classes as fields
- inheritence보다 느슨한 결합

```java
//Car HAS-A Engine

class Engine {
    void start() {}
}

class Car {
    Engine engine = new Engine(); // Composition

    void startCar() {
        engine.start();
    }
}
```

## Interface 🆚 Abstract class

- **Interface**: pure abstract class

  - like a group of rules that implement classes should follow
  - like a template that defines **what** a class must do, but **not how**
  - 공통적인 기능을 정의해 여러 클래스가 동일한 동작을 수행하게 하고 싶을 때
  - only define name of methods, 즉 abstract method(without body)
  - implement class should override, define the details of method
  - can implement multiple interfaces

- **Abstract class**:
  - common methods of child classes
  - can have both abstract method(without body) and concrete method(with body)
  - to create hierchy using inheritence
  - can only extend one abstract class

## ✅ final keyword in java

- final field: field that does not change, constant
- final method: method that cannot be overrided
- final class: class that cannot be inherited

## ✅

## ✅
