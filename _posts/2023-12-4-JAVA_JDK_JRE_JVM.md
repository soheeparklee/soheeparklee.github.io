---
title: JDK_JRE_JVM
categories: [JAVA, JAVA_Basics]
tags: [jdk, jre, jwm] # TAG names should always be lowercase
---

## ✅ JAVA

### compile 언어

- 소스코그를 목적코드로 옮기는 것 <br>
  (여기서 말하는 목적코드는 컴파일러나 소스코드 파일을 컴파일 해서 생성하는 파일) <br>
- 인간이 개발도구로 완성한 코드를 **컴파일**해서 운영체게가 이해 가능한 프로그램 언어로 바꿔줌, 이를 또 컴퓨터 하드웨어에 전달 <br>

#### compiler:

번역기, 특정 프로그래밍 언어를 다른 언어로 옮기는 프로그램, 즉 컴파일해주는 프로그램 <br>
인간이 짠 프로그래밍 코드를(program.java)를 **바이트 코드(program.class)**로 바꿔줌 <br>

#### ↔️ 인터프리터 언어(컴파일 언어와 반대되는 개념)

exe파일로 만들지 않고 <br>
실제 브라우저 console에서 바로 동작 가능(console.log) <br>

## ✅ JVM Java Virtual Machine

인간이 프로그래밍 언어로 코드 생성 ➡️ 컴파일러 ➡️ JVM ➡️ 프로그램에 전달 <br>
자바에게는 가상 메모리가 하나 있다. <br>

<img width="237" alt="스크린샷 2023-12-04 오후 8 56 03" src="https://github.com/soheeparklee/personal_project_musicApp/assets/97790983/21b93404-5866-4a1a-b80d-2477f19b443c">

원래는 운영체제 바로 위가 애플리케이션임. <br>
JAVA는 중간에 JVM이 윈도우든, 맥이든 어디에서든 운영 가능하도록 만들어준다. <br>

## ✅ JDK

java development kit(tools) <br>
JDK(필수 파일 + 개발자 패키지)안에 JRE(개발은 안하고 실행만 할 때), JVM <br>
개발까지 할 것이니 풀 패키지, 즉 JDK를 설치해야 한다. <br>
