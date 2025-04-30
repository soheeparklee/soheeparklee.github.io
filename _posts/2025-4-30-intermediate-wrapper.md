---
title: Wrapper
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## 👎🏻 Limit of Primitive type

- 1️⃣ primitive type is not an instance
- cannot use collection framework
- 2️⃣ cannot use `null`

- 👍🏻 Advantage of primitive type: faster than wrapper type

## ✅ Wrapper

- Reference type: use `equals()`
- immutable
- 값을 바꿀 때마다 새로운 인스턴스 생성

## ✅ Boxing, Unboxing

- Boxing: primitive type ➡️ wrapper type(reference)
- Unboxing: wrapper ➡️ primitive type

```java
Integer wrapper = Integer.valueOf(10); //Integer 10
int primitive = newInteger.intValue(); //int 10
```

## ✅ AutoBoxing

- `valueOf`, `intValue()` 없이 그냥 primitive type ➡️ reference type으로 자동으로 바꿔준다

```java
//auto-boxing
Integer wrapper = 10;

//auto-unboxing
int primitive = wrapper;
```

## ✅ Wrapper Methods

```java
Integer i1 = Integer.valueOf("10"); //String -> Integer(wrapper)
int i2 = Integer.parseInt("10"); //String -> int(primitive)

i1.compareTo(20);
Integer.sum(10, 20); //30
Integer.min(10, 20); //10
Integer.max(10, 20); //20
```

## ✅

## ✅

## ✅

## ✅

## ✅
