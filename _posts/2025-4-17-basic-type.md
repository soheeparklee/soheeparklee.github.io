---
title: Primitive type, Reference type
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ Primitive type

- `int`, `long`, `double`, `boolean`
- save value itself
- `int A = 10;`

## ✅ Reference type

- `class` is reference type
- `String`
- save memory value

```java
Student student = new Student();
student.age = 10;
```

## ✅ 대원칙

```
자바는 항상 변수의 값을 복사해서 대입한다
```

- primitive type

```java
int a = 10;
int b = a;
```

- reference type

```java
Student s1 = new Student(); //memory address x001
Student s2 = s1; //s2 = x001
```

- primitive type
- a, b have different memory address

```java
    public static void main(String[] args) {
        int a = 10;
        int b = a;

        System.out.println("a: " + a);
        System.out.println("b: " + b);

        a = 20;
        System.out.println("a is changed to 20");
        System.out.println("a: " + a); // a = 20
        System.out.println("b: " + b); // b = 10

        b = 30;
        System.out.println("b is changed to 30");
        System.out.println("a: " + a); // a = 20
        System.out.println("b: " + b); // b = 30
    }
```

- reference type

```java
    public static void main(String[] args) {
        Data dataA = new Data();
        dataA.value = 10;
        Data dataB = dataA;

        System.out.println("dataA 참조값=" + dataA); //Data@7344699f
        System.out.println("dataB 참조값=" + dataB); //Data@7344699f
        System.out.println("dataA.value = " + dataA.value); //10
        System.out.println("dataB.value = " + dataB.value); //10

        //dataA 변경
        dataA.value = 20;
        System.out.println("a is changed to 20");
        System.out.println("dataA.value = " + dataA.value); //20
        System.out.println("dataB.value = " + dataB.value); //20

        //dataB 변경
        dataB.value = 30;
        System.out.println("b is changed to 30");
        System.out.println("dataA.value = " + dataA.value); //30
        System.out.println("dataB.value = " + dataB.value); //30
    }
```

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅
