---
title: Interview_
categories: [JAVA, JAVA_Basics]
tags: [] # TAG names should always be lowercase
---

## ✅ String literal과 new String("")의 차이

- `String literal`: saved in **constant pool**
- `new String("")`: saved in memory **heap**

- `constant pool`에 저장되면 동일한 문자열에 대해서는 하나의 참조를 재사용
- `constant pool`에서는 같은 값이 존재한다면, 새로 정의한 변수여도 같은 주소값을 가진다

## ✅ What is literal?

- fixed, constant value
- `int PI = 3.14; `
- `String greeting = "Hello, world!";`

## String 🆚 StringBuilder 🆚 StringBuffer

- String: immutable
- StringBuilder: mutable(same memory), single thread
- StringBuffer: mutable(same memory), multithread safe

## Exception 🆚 Error

<img width="910" alt="Image" src="https://private-user-images.githubusercontent.com/97790983/454097085-6e4a1cfd-0e1a-43c4-996a-3b2530018bdd.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDk2NzQ3MjEsIm5iZiI6MTc0OTY3NDQyMSwicGF0aCI6Ii85Nzc5MDk4My80NTQwOTcwODUtNmU0YTFjZmQtMGUxYS00M2M0LTk5NmEtM2IyNTMwMDE4YmRkLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA2MTElMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwNjExVDIwNDAyMVomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTQ5MTdjZDIxODY0NjgyNjMyNTE4YzRkMjBhOWYyMmQzZWMwODc3MDllNmMzYTNmZDQxMmNjODZhMjg3NWRmZGUmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.p-RHXabBXE10i11MuxSDWoSnY35cfZPCaGitjNCd9VQ" />

- **Exception**: event that disrupts flow, usually recoverable
  - **checked exception**: exception in compile time, handled with `try-catch` or `throws`, `IO exception`, `SQL exception`
  - **unchecked exception**: exception in runtime, `NPE`, `IAE`
- **Error**: system level failure, usually not recoverable
  - `Out of Memory`, `JVM crash`

## ✅ Exception 클래스의 예시

- `IO exception`: checked exception
- `SQL exception`: checked exception
- `Null Pointer Exception`: unchecked runtime exception
- `Illegal Argument Exception`: unchecked runtime exception, divide by 0

## Checked Exception 🆚 Unchecked Exception

- **Checked Exception**: exception in compile time, `"You must deal with me, or your code won’t compile."`, thus, `try-catch or throws`
- **Unchecked Exception**: exception in runtime, ` "You can deal with me, but I won’t force you — until I crash your app."`

## throw 🆚 throws

- `throw`: throw exception

```java
public void checkAge(int age) {
    if (age < 18) {
        throw new IllegalArgumentException("Age must be 18 or older.");
    }
}
```

- `throws`: declare exception in method declaration

```java
public void myMethod() throws IOException, SQLException {
    // method code
}
```

## ✅ try-catch-finally 구문에서 finally의 역할

- `try`: code that might throw exception
- `catch`: what to do when exception occurs
- `finally`: code that must be run regardless of exception

- `finally`: after `IO`, return DB connectoin pool regardless of exception

## Throwable 🆚 Exception의 차이

## ✅ 제네릭(Generic)이란 무엇이고, 왜 사용할까요?

## ✅ What is Lambda?

## ✅ What is procedural programming?

## ✅ What is Stream?

## ✅ 람다와 스트림은 왜 생겨났을까요?

## ✅ 어노테이션이란?

## ✅ 어노테이션 사용 이유

## ✅ 리플렉션이란

## ✅ System.out.println 클래스는 성능이 좋지 않다고 하는데 이유?

## ✅

## ✅
