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

- reference type can be initialized as `null`
- `null` means address has not been set yet

## ✅ 대원칙: 자바는 항상 변수의 값을 복사해서 대입한다

```
자바는 항상 변수의 값을 복사해서 대입한다
```

## ✅ copy value

- ✔️ primitive type
- a, b have different memory address
- 기본형은 변수의 **실제 값**을 복사해서 대입
- 나도 종이를 가지고 있고, 상대방도 종이를 가지고 있는데 내 종이에 있는 값을 그대로 상대방 종이에 복사해 줌
- 내 종이 내용을 바꾼다고 해서 상대방 종이 내용은 바뀌지 않음

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

- ✔️ reference type
- 참조형은 변수에 들어있는 **참조값**을 복사해서 대입
- 나와 상대방은 구글 클라우드에서 같은 문서를 공유함
- 내 문서를 바꾸면 상대방 문서 내용도 바뀜

```java
    public static void main(String[] args) {
        Data dataA = new Data();
        dataA.value = 10;
        Data dataB = dataA; //dataB copy address of dataA

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

## ✅ Null

- reference type can be initialized as `null`
- `null` means no address has been allocated

```java
        Data data1 = null;
        System.out.println(data1); //no address, null

        Data data2 = new Data();
        System.out.println(data2); //has address
        System.out.println(data2.value); //0

        data2 = null;
        System.out.println(data2); //no address, null
```

- `GC` will free unused `address space`
- after `data2 = null`, the `address space` that `data2` was using will be freed by `garbage collector`

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅
