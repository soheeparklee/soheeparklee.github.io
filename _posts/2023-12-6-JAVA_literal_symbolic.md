---
title: Literal/ Symbolic final(상수)/ NULL
categories: [JAVA, JAVA_Basics]
tags: [char, string, ofvalue, parse, literal, instance, format] # TAG names should always be lowercase
---

## ✅ Symbolic 상수

한번 정하면 다시는 바꿀 수 없는 값 <br>
Symbolic 상수 이름지을 때는 `대문자 + "_"` <br>
조건문에서 절대 변하면 안 되는 조건들을 상수로 정의하기 좋음. 어짜피 안 변하니까! <br>

```java
final int MY_NUM = 100;
MY_NUM = 200; //❌

final double MY_DOUBLE = 123.456;

```

## ✅ literal 리터럴

우항의 값 = 데이터 그 자체 = java literal <br>

```java
int year= 2023; //literal: 2023 , variable: year
long longNum = 1L; //literal: 1L
boolean bool1= true; //literal: true
char ch1= '\u00F2' //literal: '\u00F2'
final int MAX_VALUE= 100; //literal: 100, symbolic: MAX_VALUE
```

단, 문자열 literal은 주의깊게 볼 필요가 있다. <br>

```java
String str1= "Hello"; //literal: "Hello"
String str2= String.valueOf(123); //this is not a literal!!!
```

### ☑️ 여러 진수법의 정수 리터럴 표기

#### 2진법 0b

```java
int num1= 0b111; //맨 앞에 Ob를 붙인다.
//num1= 1+ 2+ 4= 7
```

#### 8진법 0

```java
int num2= 055; //맨 앞에 O를 붙인다.
//num2= 5+ 4*8= 45
```

#### 16진법 0x

```java
int num3= 0xA2; //맨 앞에 Ox를 붙인다.
//num3= 2 + 10 * 16
int num4= 0xAC0;
//num4= 12 * 16 + 10 * 16^2 = 2752

```

### ☑️ E

double타입일 때 E를 붙이면 10의 제곱을 곱한다. <br>

```java
double doubleNum1= 5E5;
//E와 양수를 붙이면 10의 제곱을 곱한다.
//result: 5 * 10^5
double doubleNum2= 55.25E2;
//E와 양수를 붙이면 10의 제곱을 곱한다.
//55.25 * 10^2 = 5525.0
double doubleNum3= 55.25E-2;
//E와 음수를 붙이면 10의 제곱을 나눈다.
//55.25 /10^2 = 0.5525
```

## ⭐️ null

String은 reference type이므로 null을 사용할 수 있다. <br>
reference type만 null사용 가능함!! <br>

```java
String str= null; //가능⭕️
```

⭐️ 빈 문자열과 null은 다르다. <br>
`""` 과 `null`은 같지 않다. <br>
<br>
`""`은 길이는 0이지만, 힙 공간에 자리는 차지한다. <br>
예를 들자면, 종이는 있음. 종이에 아무것도 쓰인 건 없음. <br>
<br>
`null`은 힙에 할당조차 되지 않음. 가리키는 곳이 없음. <br>
종이조차 없는 상태 <br>
