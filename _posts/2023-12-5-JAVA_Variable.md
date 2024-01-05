---
title: Variable
categories: [JAVA, JAVA_Basics]
tags: [local, class, instance] # TAG names should always be lowercase
---

## ✅ 선언 위치에 따른 변수 종류

멤버변수 🟰 class 변수, instance 변수

#### class 변수 🟰 static

📍 선언 위치: 클래스 영역
⏰ 생성 시기: 클래스가 메모리에 올라갈 때
⚡️ 초기화: 선택적
➖ 모든 인스턴스들이 공통된 값 가져야 할 때

#### instance 변수

📍 선언 위치: 클래스 영역
⏰ 생성 시기: 인스턴스 생성될 떄
⚡️ 초기화: 선택적
➖ 인스턴스마다 다른 값 가질 때

#### local변수

📍 선언 위치: 클래스 영역 이외(메서드, 생성자 등)
⏰ 생성 시기: 변수 선언문이 수행되었을 때
⚡️ 초기화: 사용하기 전에 반드시 초기화 필수
➖ 선언 블록 `{ }`내에서만 사용 가능

## ✅ 멤버변수 초기화 방법

### ✔️ explicit initialization

```java
class Car{
    int door= 4;
    Engine e= new Engine();
}
```

### ✔️ constructor

### ✔️ initialization block 초기화 블럭

- 인스턴스 초기화 블럭: 인스턴스 변수 초기화
- 클래스 초기화 블럭: 클래스 변수 초기화

```java
//constructor 1
    Car(){
        count++;
        serialNo= count++;
        color= "White";
        gear= "auto";
    }

//constructor 2
    Car(String color, String gearType){
        count++;  // 👎🏻 같은 코드 중복
        serialNo= count++;  // 👎🏻 같은 코드 중복
        this.color= color;
        this.gearType= gearType;
    }

// 👍🏻 initialization block 사용한 코드
{
            count++;
        serialNo= count++;
}
Car(){
        color= "White";
        gear= "auto";
    }
Car(String color, String gearType){
        this.color= color;
        this.gearType= gearType;
    }

```
