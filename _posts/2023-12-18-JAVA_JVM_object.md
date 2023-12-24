---
title: Object
categories: [JAVA, JAVA_Basics]
tags: [object] # TAG names should always be lowercase
---

## ✅ Java.lang 패키지

Java.lang안에 이런 클래스들이 내장되어 있다. <br>

- Object Class
- System: `System.out.println()`
- String
- Wrapper: 기본 타입의 데이터를 갖는 객체 만들 때 사용
- Math

우리가 가져오지 않아도 자동으로 가져와져서 쓰여짐<br>

## ✅ 최상위 클래스 Object

모든 클래스의 상위 클래스<br>

```java
public class Animal extends Object
//사실은 우리도 모르게 모든 class는 Object를 상속함
//extends Object뒤에 붙여져 있음, 생략되어 있지만~

//당연히 upcasting도 가능함
Animal animal1 = new Animal("cat");
Object animal2 = new Animal("dog");
```

## ✅ Object method

<img width="1130" alt="스크린샷 2023-12-18 오후 10 42 25" src="https://github.com/soheeparklee/sc_project_carrotMkt_improved/assets/97790983/a77d2636-5b96-4f0a-b0ea-754027bfb5f0">
