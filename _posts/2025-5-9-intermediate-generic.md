---
title: Generic, generic method
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ Generic

> 사용할 타입을 미리 결정하지 않는다, `type parameter` 결정을 미루기 <br>
> 클래스 생성할 때 타입을 결정하지 않고, 인스턴스 생성 때 타입 결정 <br>

- when creating class: use `type parameter <T>`
- when creating instance: **set** type when creating `instance`
- 👍🏻 can create class with all types
- 👍🏻 클래스 만들때는 어떤 타입으로 만들지 결정을 미뤘다가, `instance`생성할 때 타입 결정
- 👍🏻 reuse code
- 👍🏻 type safety

<br>

- 👎🏻 **before generic**
- IntegerBox, StringBox 따로 두 개 만들어야 함

```java
public class IntegerBox { //👎🏻 IntegerBox, StringBox 따로 만들어야 함
    private Integer value;
}

public class StringBox { //👎🏻 IntegerBox, StringBox 따로 만들어야 함
    private String value;
}

//Main
public class Main {
    public static void main(String[] args) {
        IntegerBox integerBox = new IntegerBox();
        StringBox stringBox = new StringBox();
    }
}
```

- 👍🏻 **with generic**
- can **handle all types** with one generic class
- write in `type parameter <T>` what type I want
- ` GenericBox<Integer> xxx = new GenericBox<>();`

```java
public class GenericBox<T> { //only need generic Box
    private T value; //DO NOT DECIDE value type in class
}

//Main
public class Main {
    public static void main(String[] args) {
        GenericBox<Integer> integerBox = new GenericBox<>(); //DECIDE value type when creating instance
        GenericBox<String> stringBox = new GenericBox<>();

    }
}
```

## ✅ Limit type parameter

- Generic써서 특정 클래스만 type parameter로 제한
- **limit** type parameter to `animal` and `children of animal`
- `Animal`과 `그 자식들`만 들어올 수 있는 `Animal Hospital` 만들기

- `Dog`, `Cat` extends `Animal`
- I want to make animal hospital that only `animal` and `animal child` to be sent as `type parameter`
- `AnimalHospital` created with `type parameter <Dog>` can use `Animal` class methods

```java
public class AnimalHospital<T extends Animal> { //⭐️ limit type parameter
    private T animal;
}

//Main
public class Main {
    public static void main(String[] args) {
        AnimalHospital<Dog> dogHospital = new AnimalHospital(); //set animal hospital type as Dog, Cat
        AnimalHospital<Cat> catHospital = new AnimalHospital();

        Dog dog = new Dog("doog", 100);
        Cat cat = new Cat("kitty", 50);

        dogHospital.set(dog); //set animal hospital as dog
        dogHospital.checkUp(); //can use animal methods()

        catHospital.set(cat);
        catHospital.checkUp();
```

## ✅ Generic method

> 사용할 타입을 미리 결정하지 않는다, `type parameter` 결정을 미루기<br>
> 메소드를 만들 때 `type parameter` 결정을 하지 않고, 메소드를 호출할 때 `type parameter`을 결정

- `<T> T method()` 나는 제네릭 메소드야
- `<T extends String> T method()`해서 limit type parameter to String

```java
public static <T> T method1(T t){ //generic method
    return t;
}

public static <T extends String> T method2(T t){ //limit type parameter to String
    return t;
}

public static <T> void method3(T t){ //return void
}
```

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅
