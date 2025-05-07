---
title: Class, System, Math 클래스
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ Class 클래스

- Class 클래스를 통해서 get **metadata** about a class 할 수 있다

- ✔️ get class type information: class name, super class, interface, access modifier...
- ✔️ reflection: get `field`, `method`, `constructor` info in class
- ✔️ dynamic loading: `Class.forName()`, `newInstance()`
- ✔️ annotation

## ✅ How to get metadata of class

- get metadata of `String` class
- reflection of a class

```java
Class clazz = String.class; //get metadata of String class

clazz.getDeclaredFields(); //get fields
clazz.getDeclaredMethods(); //get methods
clazz.getInterfaces(); //get interface
clazz.getSuperclass() //get parent class

```

## ✅ System 클래스

- get **metadata** about system

- get time
- get env variable
- get system info
- copy array
- exit program

```java
//get time
long currentTime = System.currentTimeMillis();
long nanoTime = System.nanoTime();

//get env variables
System.getenv();

//get system properties, 자바의 환경설정
//encoding info, java version
System.getProperties();
System.getProperty("java.version"); //get java version

//copy array
char[] originalArray = {'h', 'e', 'o'};
char[] copyArray = new char[3];
System.arraycopy(originalArray,0, copyArray, 0, originalArray.length);

//exit program
System.exit(0);
```

## ✅ Math 클래스

- useful methods for math

```java
Math.max(10, 20);
Math.min(10, 20);
Math.abs(-10);

Math.ceil(2.1); //올림
Math.floor(2.1); //내림
Math.round(2.1); //반올림

Math.sqrt(4); //제곱근
Math.random(); //0.0 ~ 1.0 사이의 랜덤 숫자
```

- ✔️ **random**
- if there is seed, random result will always be same

```java
Random random = new Random();

random.nextInt(); //random Integer
random.nextDouble(); //random Double
random.nextBoolean(); //random Boolean(true or false)

random.nextInt(10); //random Integer between 0~9

Random randomSeed = new Random(1); //if seed is same, random result is same
randomSeed.nextInt(); //always return same int
```

## ✅

## ✅

## ✅

## ✅
