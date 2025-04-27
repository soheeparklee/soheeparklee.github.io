---
title: Access modifier
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ What does access modifier do?

> **Allow** access or **hide** `class`, `field`, `constructor`, `method` from outside class/package <br>

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

## ✅ Where is access modifier used?

- field
- method
- contructor
- class

## ✅ Class and access modifier

- class can only be `public` or `default`

## ✅ Encapsulation

- make a class's `field` and `method` together into a `capsule`
- 🟰 `OOP`
- `Access modifier` helps `encapsulation` safe
- by limiting access to `field` and `method` inside `capsule`

- ✔️ `field` should be `private`
- `private field`: `field` should not be altered from outside class

  - `field` should be accessed through `method`
  - 계좌에서 입금, 출금을 하기 위해 버튼을 누르지 우리가 직접 잔액을 바꿀수는 없음!
  - 입금, 출금은 버튼을 통해서 ➡️ `field` 접근은 `method`를 통해서

- ✔️ make the most `method` `private`
  - hide `methods` that should not be altered from outside class
  - limit access to `method` from outside
  - 꼭 필요한 `method`만 노출하기
  - 사용자는 입금, 출금만 간단하게 하고, 금액이 유효한지/잔액이 충분한지 등 로직은 숨김

## ✅ what is a good Encapsulation?

- `field` and `method` in one `class(capsule)`
- `field` are private
- `field` should be accessed through method
- only required `method` should be accessible from outside
- limited access to `method` as well

## ✅

## ✅
