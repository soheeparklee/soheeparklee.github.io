---
title: Exception
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ Why do we need Exception class?

- `정상 흐름`과 `예외 흐름`을 따로 분리하기 위해

- 👎🏻 **before**
- `connect` -> `send` - `disconnect`하는 코드라면
- `정상 흐름`과 `예외 흐름`이 섞여서
- 이 코드가 도대체 어떤 순서로 무엇을 하는지 알기가 어려움

```java
client.initError(data); //init 정상흐름

String connectResult = client.connect(); //connect 정상흐름
if(isError(connectResult)){ //if connect fail 예외 흐름
}

String sendResult = client.send(data); //send 정상흐름
if(isError(sendResult)){ //if send fail 예외 흐름
}

client.disconnect(); //disconnect  정상흐름
```

## ✅ Exception and Error

<img width="518" alt="Image" src="https://github.com/user-attachments/assets/2f83c619-9080-47a1-8e24-950cbc73b297" />

- Error: developer does not catch error
- Exception:

  - Checked exception:
  - Unchecked exception(`Runtime Exception`)

- ✔️ **Checked exception**
  - developer **MUST** explicitly `catch` or `throw` the exception
  - `SQL Exception`, `IO Exception`
  - `extends Exception`

```java
public class MyCheckedException extends Exception{ //checked exception extends Exception
}
```

- ✔️ **Unchecked exception(`Runtime Exception`)**
  - developer `catch` or `throw` exception is **NOT** mandatory
  - `catch` or `throw` 생략가능!
  - if developer do not `catch` or `throw` exception, Java will **automatically** `throw` the exception
  - `Null Pointer`, `Illegal argument`
  - `extends RuntimeException`

```java
public class MyUncheckedException extends RuntimeException {
}
```

## ✅ Throw, catch

- every exception should be `thrown` or `caught` by the class who called the exception

- 💡 **catch**:

  - 내 클래스에서 예외 잡아서 해결⭕️
  - use `try-catch`
  - 잡아서 해결한 다음에는 정상흐름으로 이어서 실행

- 💡 **throw**:

  - 내 클래스에서 해결❌
  - 나를 부르는 클래스로 던지기
  - 계속 던지고 던져서 미루고 `main()`에서도 던지면 프로그램 종료

- `client.call()` is calling exception
- `callCatch()`: catch and handle exception, run 정상흐름
- `callThrow()`: cannot handle exception, throw outside this class

```java
Client client = new Client();

public void callCatch(){ //💡 catch exception, try-catch
    try{
        client.call();
    }catch (MyCheckedException e){ //해결⭕️
         e.getMessage() //handle exception
       }

    System.out.println("running code"); //after handling exception, 이어서 정상흐름
}

public void callThrow() throws MyCheckedException { //💡 cannot catch, throw to outside 해결❌
    client.call();✔️
}
```

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅
