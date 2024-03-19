---
title: Wrapper Class
categories: [JAVA, JAVA_Basics]
tags: [wrapper] # TAG names should always be lowercase
---

## ✅ Wrapper Class

primitive data type는 객체 ❌<br>
Wrapper Class는 클래스이기 때문에 객체의 reference type ⭕️<br>

<img width="441" alt="스크린샷 2023-12-20 오후 5 18 17" src="https://github.com/soheeparklee/sc_project_carrotMkt_improved/assets/97790983/0a6814b1-3c58-40c1-9994-42cff5ecaf3f">

### Wrapper Class 장점

1. 객체지향적 프로그래밍 실현 & 자료구조 일관성 유지<br>
   객체지향을 좋아하는 사람들이 "JAVA의 정체성은 OOP니까 primitive type도 객체로 만들어보자" 라는 취지에서 나옴.<br>
2. **null**을 선언할 수 있음<br>
3. library사용할 때 wrapper을 사용하면 지원받을 수 있다.<br>
4. **GENERIC 프로그래밍은 wrapper만 지원하기 때문이다.**<br>

## 💡 어떤 때 primitive쓰고 어떤 때 wrapper쓰나요?

integer에 null을 넣고 싶을 때<br>
Wrapper은 integer 객체이기 때문에 null을 넣을 수가 있다.<br>
객체이다보니까 일관성이 있다.<br>

```java
Integer integerNull= new Integer(0);
int integerNull= null;
```

🆚 그러나 int는 null을 넣을 수가 없잖아!<br>

## ✅ Boxing, unboxing

Boxing: 기본 타입을 래퍼 클래스에 매칭하는 것, 객체로 선언<br>
unboxing: 객체 선언 전 value를 구해오는 것<br>
요즘은 오토 박싱, 오토 언박싱을 한다.<br>
그래서 그냥 class로만 선언해도 된다.<br>

## ✅ Wrapper Class 사용법

integer타입의 reference type임에도 operator사용해 더하고 뺴면 값 구할 수 있음<br>

```java
package chap45_wrapper;

public class WrapperClassTest {
    public static void main(String[] args) {
        //⭐️ Integer
        Integer integerBoxing= new Integer(20); //Integer 이라는 wrapper로 boxing
        int intUnboxing= integerBoxing.intValue(); //unboxing
        System.out.println(integerBoxing); //20
        System.out.println(intUnboxing); //20


        //autoboxing
        Integer integerAuto= 30; //Integer integerAuto= new Integer(30);
        System.out.println(integerAuto); //30
        //auto Unboxing
        int intAuto= integerAuto;
        System.out.println(intAuto); //30

        //operator 가능하다
        System.out.println(integerBoxing + intUnboxing); //20+20= 40
        System.out.println(integerBoxing + integerAuto); //20 + 30= 50

        //⭐️ char
        Character character1= new Character('A'); //Character 이라는 wrapper로 boxing
        char ch1= character1.charValue(); //unboxing

        System.out.println(character1); //A
        System.out.println(ch1); //A

        //autoboxing, autoUnboxing
        Character character2= 'B'; //autoboxing
        char ch2= character2; //autoUnboxing

        System.out.println(character2); //B
        System.out.println(ch2); //B

        //❗️ char valueOf 배열일 때 주의할 것
        char[] characters= {'a', 'b', 'c'};
        String str= String.valueOf(characters); //abc

        //⭐️ Boolean
        Boolean boolean1= new Boolean(true); //boolean 이라는 wrapper로 boxing
        boolean bool1= boolean1.booleanValue(); //unboxing

        //autoboxing, autounboxing
        Boolean boolean2= false; //autoboxing
        boolean bool2= boolean2; //autoUnboxing

        System.out.println(bool1 && bool2); //false
        System.out.println(boolean1 || bool2); //true
    }
}

```
