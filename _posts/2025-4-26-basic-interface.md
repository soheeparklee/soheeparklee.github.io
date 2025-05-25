---
title: Interface
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ Summary

- `interface` is like pure abstract class
  - cannot create instance
  - **MUST** be overrided by child class
- `implements`
- can `implements` several `interface`

## ✅ Interface

- Interface 🟰 pure abstract class

```java
//pure abstract class
public abstract class Animal {
    public abstract void sound();
    public abstract void move();
}
//same as interface
public interface Animal {
    void sound(); //omit public abstract
    void move(); //omit public abstract
}
```

- like abstract class
- 1️⃣ cannot create interface instance
- 2️⃣ all methods in interface should be overrided by child class

  - all methods are empty

- can use `public static final` variable
- can omit `public static final`

```java
public interface Animal {
     double MY_PI = 3.14; //public static final

    void sound(); //omit public abstract
    void move(); //omit public abstract
}
```

## ✅ Implement interface

- `interface` ➡️ `implement`

```java
public interface Animal {
    void sound();
    void move();
}

public class Dog implements Animal{ //⭐️ implement
    @Override
    public void sound() {} //must override interface method

    @Override
    public void move() {} //must override interface method
}
```

## extends 🆚 implement

- `parent class, abstract class` ➡️ `extends`
  - 부모 클래스의 xxx을 child가 받아 더 발전/확장시켜 쓰는 느낌
  - 모두 override할 필요 없이 일부만 가져다 쓰기 가능하므로
  - child extends parent
- `interface` ➡️ `implement`
  - interface를 implement하는 모든 클래스가 반드시 지켜야 하는 약속/규칙
  - 모두 무조건 override해야 함
  - implement 약속/규칙

## ✅ Why use interface? not use extends or abstract class?

- extends: 일부는 override하지 않을 수도 있음
- abstract: 마찬가지로 override하지 않을 수도 있음
- 👎🏻 개발자가 override하는걸 까먹으면 어떡함??

- interface: **무조건** override해야 함
- implement하는 클래스들이 무조건 `interface의 규칙/약속`을 따르게 됨
- interface는 다중 implement 가능

## ✅ Interface can have serveral implements

- `interface` ➡️ can have **several** implements

```java
public interface InterfaceA {
    void methodA();
    void methodCommon();
}

public interface InterfaceB {
    void methodB();
    void methodCommon();
}

public class Child implements InterfaceA, InterfaceB{
    @Override
    public void methodA() {} //MUST override from InterfaceA

    @Override
    public void methodB() {} //MUST override from InterfaceB

    @Override
    public void methodCommon() {}  //MUST override from both
}
```

<img width="521" alt="Image" src="https://private-user-images.githubusercontent.com/97790983/437704864-4fbc3c3c-f9c9-4246-aaec-3a0d96411cdb.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDc4NjEyNDgsIm5iZiI6MTc0Nzg2MDk0OCwicGF0aCI6Ii85Nzc5MDk4My80Mzc3MDQ4NjQtNGZiYzNjM2MtZjljOS00MjQ2LWFhZWMtM2EwZDk2NDExY2RiLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA1MjElMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwNTIxVDIwNTU0OFomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTZmNjdhNTA5ZWYzMzMzOGE1MTgxMDQ5M2NjM2I3MWRkMDZmMGY0YzYzZTg3NDU1NjdlMjNiZDVlYzVhOTNhOWQmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.tUbiA92WZjpXhgx-sWaZAtcwUs85YUCr-v8L7uSSIek" />

- override method always has priority
- when method is called, will always return **override** method
- when `methodA()` is called, will return `override` value
- when `methodB()` is called, will return `override` value
- when `methodCommon()` is called, will return `override` value

```java
public class Main {
    public static void main(String[] args) {
        InterfaceA a = new Child();
        InterfaceB b = new Child();

        a.methodA(); //overrided in child class
        a.methodCommon(); //overrided in child class
        b.methodB(); //overrided in child class
        b.methodCommon(); //overrided in child class
    }
}
```

## ❓ Why interface can have several implements?

- `extends` ➡️ can have only **one** parent
- `interface` ➡️ can have **several** implements

- `extends` : 자식은 부모를 override할 수도 있고, 안 할수도 있음

  - 자식이 부모의 method를 override하지 않았다고 생각해보자
  - 부모 1, 부모 2에는 모두 `hello() method`가 있음
  - 그리고 자식이 만약 부모 1, 부모 2를 extends했다면,
  - 자식이 `hello() method`를 호출하면, 그 메소드를 부모 1에서 불러옴? 아니면 부모 2에서 불러오는가? 에 대한 문제가 발생

- `interface` ➡️ `implement`
  - 자식은 무조건 `interface`의 모든 메소드를 override해야 함
  - 따라서 여러 부모를 상속받는다고 해도,
  - `hello() method`를 호출하면 override한 자식의 `hello() method`가 호출됨
  - 👍🏻 위와같이 어떤 부모에서 불러와야 하는지 문제 발생하지 않음
  - 따라서 `interface`는 다중구현 허용

## ✅ use Implement and Extends together

- ✔️ Animal abstract class

```java
public abstract class Animal {
    public abstract void sound(); //abstract method, MUST override

    public void move(){ //not abstract, override not mandatory
        System.out.println("animal move");
    }
}
```

- ✔️ Fly interface

```java
public interface Fly {
    void fly(); //MUST override
}
```

- ✔️ use extends and implement

```java
public class Dog extends Animal{
    @Override
    public void sound() {
        System.out.println("woof");
    }
}

public class Bird extends Animal implements Fly{
    @Override
    public void sound() {} //MUST override from extends parent class

    @Override
    public void fly() {} //MUST override from interface
}

public class Chicken extends Animal implements Fly{
    @Override
    public void sound() {} //MUST override from extends parent class

    @Override
    public void move(){} //can override from extends parent class

    @Override
    public void fly() {} //MUST override from interface
}
```
