---
title: Object class
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ Object class

- `Object class` is parent of all Java classes
- highest parent of all Java class
- 자바의 최상위 부모 클래스
- implicitly imports `object`
- `public class Parent extends Object` (`extends Object`는 생략)

- `child class extends Parent`
- `Parent class extends Object`
- when `child class` is created, both `parent class` and `object class` is created

<img width="495" alt="Image" src="https://github.com/user-attachments/assets/5f0139eb-6e9d-49b1-a27a-9c922a0eeffd" />

- ✔️ **Object class methods**
  - `toString()`
  - `equals()`
  - `getClass()`

## ✅ Object and polymorphism

- `Object class` is parent of all Java classes
- parent class can become child class
- thus, `Object class` can become all class

```java
Dog dog = new Dog();
Car car = new Car();
dog.toString(); //child can call parent method

Object objDog = new Dog(); //부모는 자식을 담을 수 있다, upcasting
Object objCar = new Car();

objDog.dogSound(); //🔴 compile error, parent does not know child class field and method

if(obj instanceof Dog dog){
    dog.dogSound(); //🟢 after downcasting Obj -> dog, then can call child method
}
```

## ✅ Object and array

- `Object class` is parent of all Java classes
- `Object array` can contain all types of classes

```java
Dog dog = new Dog();
Car car = new Car();
Object object = new Object();

Object[] objectArrays = {dog, car, object};
```

## 💡 toString();

- every class can call `toString()`

```java
public String toString() {
        return getClass().getName() + "@" + Integer.toHexString(hashCode());
    }

//💡 result
com.example.javaintermediate1.lang.toString.Car@7344699f
```

- `Integer.toHexString(hashCode()`: 우리가 보는 객체의 참조값
- `hashCode()`: 객체의 참조값
- `toHexString`: 16진수 숫자문자로 바꾸기
  <br>

- able to override `toString()` method in individual class

```java
public class Dog{
    @Override
    public String toString() {
        return "Dog{" +
                "dogName='" + dogName + '\'' +
                ", age=" + age +
                '}';
    }
}
//💡 result
Dog{dogName='poppy1 ', age=2}
```

## ✅ Object and OCP

- **open** for adding new class, for example `new Car, new Dog`
- **closed** in modifying old class for example, `Object class`
- without modifying `Object class`, `Car` and `Dog` can use `Sysytem.out.println()`
- ➡️ Polymorphism(`extends Object` and `method overriding`)
- ➡️ OCP
- Thus, `Object class` is a huge example of polymorphism and OCP

## 💡 equals();

- `==` : is it pointing to the same instance?
- `equals()` : has the same value?

- `Object equals()`기본 메소드는 어떤 기준으로 비교해야 하는지 모른다
  - (회원 아이디가 같으면 같은 회원인가? 회원 주민등록번호가 같으면 같은 회원인가?)
- ➡️ `equals()` method override

```java
User userA = new User("123");
User userB = new User("123");

userA == userB //false

// 👎🏻 equals() override 전
// object class의 기본 equals()는 무엇을 기준으로 같은 회원으로 판단해야 하는지 모름
// return flase
userA.equals(userB) //false

//👍🏻 equals() override 후
//회원 아이디가 같으면 같은 회원으로 판단하라고 override 했음

@Override
public boolean equals(Object o) {
    if (this == o) return true;
    if (!(o instanceof UserV2 userV2)) return false;
    return Objects.equals(id, userV2.id);
}

userA.equals(userB) //true
```

## ✅

## ✅

## ✅

## ✅
