---
title: Abstract
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ Abstract class

- Parent class, but can **NOT** be created as instance
- `동물`이라는 개념 안에 `강아지`, `고양이` 등이 있지만 `"동물"`이라고 하는 `동물`은 없음
- 따라서 `동물`은 인스턴스를 생성하면 안 됨

- `Animal class`: abstract class
- `Dog class`, `Cat class`: extends `Animal` abstract class

```java
public abstract class Animal { //abstract class, parent
}

public class Dog extends Animal{ //child class
}

public class Cat extends Animal{
}
```

- cannot create an instance of abstract class

```java
Animal animal = new Animal(); //❌ error

Dog dog = new Dog(); //⭕️ create child class that extends Animal class
Animal poly = new Dog(); //⭕️ polymorphism
```

## ✅ Abstract method

- 1️⃣ child class **MUST** override abstract method
  - abstract method is only used in abstract class
- 2️⃣ no body
  - will be overrided by child class

```java
public abstract class Animal {
    public abstract void sound(); //abstract method
    //only in abstract class
    //MUST be overrided by child class
    //abstract method has no body(will be overrided by child class)


    public void move(){ //not abstract method
        System.out.println("animal is moving");
    }
    //override not mandatory
}

public class Cat extends Animal{
    @Override
    public void sound() {
        System.out.println("meow");
    }
    //child class MUST override abstract method
}
```

- parent class: 메소드를 정의만 하고
- child class: override 해서 메소드 실제 구현

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅
