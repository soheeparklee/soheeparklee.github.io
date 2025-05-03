---
title: Type safe Enum
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ Why do we need Enum?

- Limit field to certain value

- User role can be only `BASIC`, `GOLD`, `DIAMOND`
- 👎🏻 how can we prevent entering `basiiiic`(오타) or `diamond`(소문자) or `VIP`(존재하지 않는 값)?
- 💊 ENUM

## ✅ Type safe enum pattern

- can only use enumerated fields
- if only enumerate `BASIC`, `GOLD`, `DIAMOND`, can only use these three values

- 👍🏻 type safe: only can use enumerated fields
- 👍🏻 data consistency

## ✅ Implement enum pattern

- 1️⃣ constant, `static final` enum field
- 2️⃣ `private` constructor, cannot be created from outside ENUM class

- ✔️ **Example of enum pattern**

```java
public class ClassGrade {
    //same class, but different instance
    public static final ClassGrade BASIC = new ClassGrade(); //1️⃣ constant, static final
    public static final ClassGrade GOLD = new ClassGrade();
    public static final ClassGrade DIAMOND = new ClassGrade();

    //2️⃣ private constructor, cannot create from outside this class
    private ClassGrade() {
    }
}
```

- `ClassGrade.BASIC`, `ClassGrade.GOLD`, `ClassGrade.DIMAOND` is same class
- but different instance

## ✅ ENUM

- Java helps the use of `enum pattern`
- 👍🏻 type safe: only can use enumerated fields
- 👍🏻 data consistency

```java
public enum Grade {
    BASIC, GOLD, DIAMOND
}
```

- same code as `ClassGrade`
- CANNOT be created as instance(`private constructor`)
- `Grade.BASIC`, `Grade.GOLD`, `Grade.DIMAOND` is same class
- but different instance

## ✅ Enum methods

- `.values()`: get enum values
- `.name()` : get name of value
- `.ordinal()`: get number of value
- `.valueOf()`: set enum value

```java
Grade[] values = Grade.values(); //get all values of ENUM


for(Grade value : values){
    value.name(); //value 이름 얻기
    value.ordinal(); //몇 번째 value인지 return
}

String input = "GOLD";
Grade gold = Grade.valueOf(input); //set ENUM value
```

## ✅

## ✅

## ✅

## ✅

## ✅
