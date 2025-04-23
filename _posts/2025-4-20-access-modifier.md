---
title: Access modifier
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ What does access modifier do?

> Allow access or hide from outside class/package <br>

- Developer should not change speaker volume outside `speaker` class

- 👎🏻 Before(without access modifier)

```java
public class Speaker1 {
     int volume;
}
```

```java
public class SpeakerMain1 {

    public static void main(String[] args) {
        speaker.volume = 200; //👎🏻 Can change speaker volume in main class
    }
```

- 👍🏻 After
- add `private`
- `main class` cannot access `speaker.volume`

```java
public class Speaker2 {
    private int volume; //🟢 add private access modifier
}
```

```java
public class SpeakerMain2 {

    public static void main(String[] args) {
        speaker.volume = 200; //🔴 compile error
        //👍🏻 cannot access speaker.volume
    }
```

## ✅ Access modifier

- `private`: same class
- `default`: same package(`package private`)
- `protected`: same package + inherit
- `public`: allow all access

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅
