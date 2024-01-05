---
title: Data Type
categories: [JAVA, JAVA_Basics]
tags: [bit, byte, float, double, casting, implicit, explicit] # TAG names should always be lowercase
---

## ✅ 정수의 크기

각 변수에 알맞는 메모리 용량을 배정한다. <br>
맨 앞 0,1은 +, - 파악하는데 씀. <br>

#### bit: 0,1

#### byte: 8bits

max: 127 <br>
min: -128 (-2의 7제곱) <br>

#### short: 2bytes

#### int: 4bytes

max: 2의 31승-1 <br>
min: -2의 31승 <br>

#### long: 16bytes

## ✅ 실수

#### float

#### double

## ✅ Casting 형 변환

int를 short에 넣으면 왜 안될까? <br>
int에서 double을 더하거나 빼려면 어떻게 해야 할까? <br>

#### ☑️ Implicit Casting

묵시적 형 변환(자동 형 변환)

작은 데이터형이 ➡️ 큰 데이터 형으로 변함
int VS double ➡️ double

✔️ float 또는 long 안에 int 넣기 ⭕️
int안에 float넣기 ❌

```java
int myInt=5;
float myFloat = myInt;
long myLong= myInt;
```

✔️ 서로 다른 두 개의 형 더해서 더 큰 데이터형에 저장

```java
int myInt=10;
double myDouble = 55.123;
double result= myInt + myDouble;
```

✔️ 나누기 주의하기

```java
int num1=10;
int num2=3;
int result1= num1/num2; //result: 3

//그러면 result을 float로 하면 되겠다 ❌
int num1=10;
int num2=3;
float result1= num1/num2; //result 3.0 , 이미 int에서 소수점 버려버림

//자료형 선언할 때부터 float으로 해 주어야 한다.
int num1=10;
float num2=3.0f;
float result1= num1/num2; //result 3.333...
```

#### ☑️ Explicit Casting

더 정밀한 자료형 ➡️ 덜 정밀한 자료형 <br>
큰 바이크 크기 ➡️ 작은 바이트 크기 <br>

✔️ 자료 손실 주의하기

```java
float numFloat=10.5f;
int changeInt= numFloat; //그냥 이렇게 하면 안 됨.
int changeInt= (int)numFloat;  //result: 10
```
