---
title: Object class, equals()
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

<img width="495" alt="Image" src="https://private-user-images.githubusercontent.com/97790983/438136742-5f0139eb-6e9d-49b1-a27a-9c922a0eeffd.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDc4NjEyMTEsIm5iZiI6MTc0Nzg2MDkxMSwicGF0aCI6Ii85Nzc5MDk4My80MzgxMzY3NDItNWYwMTM5ZWItNmU5ZC00OWIxLWEyN2EtOWM5MjJhMGVlZmZkLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA1MjElMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwNTIxVDIwNTUxMVomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPThlMWY4ODBiZDQ4NGVmOWY2ZmNkZWIyNDczZjM0MGQ0NTNjZjNkNmQxMTgzYWViZTVlYjdlYzk5NDMyZjMwMTImWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.x-L7UY28ymU7K5DtM_MKObnqaYMqeDGBI8O0kveR1Ro" />

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

## 💡 `==` and `equals()` 심화

#### ✔️ primitive int

```java
int a = 5;
int b = 5;

a == b;      //true
a.equals(b)  //do not exist
```

- primitive type에서 `==`는 **compare values**
- primitive type에서 `equals()`는 존재하지 않는다

#### ✔️ -128 ~ 127 Reference type Integer, Wrapper

```java
Integer a = 5;
Integer b = 5;

a == b;        // true (cached values between -128 and 127)
a.equals(b);   // true
```

- Normally, in reference type `==` checks if they refer to the same object in memory
- so it seems `a == b` should be false...
- ⚠️ HOWEVER, Java has optimization called **Integer cache**
- JVM reuses Integer objects for all values in the range of `-128` to `127`
- so, both `a` and `b` **point to the same cached Integer object**, `5`

- ⚠️ JVM only caches numeric weapper types,
  - Byte
  - Short
  - Integer
  - Long
  - Character (for small characters)
- and their cache ranges are typically -128 to 127

#### ✔️ Reference type Integer, Wrapper outside cache range

```java
Integer a = 128;
Integer b = 128;

a == b;        // false (different objects)
a.equals(b);   // true  (same value)
```

#### ✔️ Wrapper class that is not cached

```java
Double a = 10.0;
Double b = 10.0;

a == b;        // false
a.equals(b);   // true
```

#### ✔️ Compare primitive and wrapper

```java
double a = 10.0;
Double b = 10.0;

x == y; //true
```

- true bc Java `unboxes` the `Double` into `primitive double` for comparison

#### ✔️ String

```java
String a = "hello";
String b = "hello";

a == b;        // true
a.equals(b);   // true
```

✔️ `==`

- normally, in reference, `==` compares reference, whether they refer to the same object in memory
- ⚠️ HOWEVER, `string literals` in Java are saved in **string pool**
- 그래서 `String`이 똑같으면 string pool에 한번만 저장함
- 따라서 `a == b` is `true`

✔️ `equals()`

- String class overrides .equals() to compare the content (characters) of the string

#### ✔️ String Instance

```java
String a = new String("hello");
String b = new String("hello");

a == b;        // false (different objects)
a.equals(b);   // true  (same content)
```

## ✅

## ✅

## ✅

## ✅
