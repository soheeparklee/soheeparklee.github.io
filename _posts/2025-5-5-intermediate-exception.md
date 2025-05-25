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

<img width="518" alt="Image" src="https://private-user-images.githubusercontent.com/97790983/440567816-2f83c619-9080-47a1-8e24-950cbc73b297.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDc4NjExMDksIm5iZiI6MTc0Nzg2MDgwOSwicGF0aCI6Ii85Nzc5MDk4My80NDA1Njc4MTYtMmY4M2M2MTktOTA4MC00N2ExLThlMjQtOTUwY2JjNzNiMjk3LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA1MjElMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwNTIxVDIwNTMyOVomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWQ0ZDc5MjM5Nzk0NmRjOTM0NGUzODQ3NzEyNjg4OWM3N2YyMjgyMmE5YjMzZjNjYzBhN2Q5MWZkYTBmNjljNDYmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.S_oLzxmm2jnlvexVUnJbTbaTsusK5FCfdi2NA85IzBM" />

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
  - `정상흐름`, `예외흐름` 분리 성공

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

public void callThrow() throws MyCheckedException { //💡 cannot catch, throw to outside, 해결❌
    client.call();✔️
}
```

## ✅ Try-Catch Finally

- 👍🏻 `try-catch`로 정상흐름, 예외흐름 분리 성공

```java
try{
  //정상흐름
}catch(Excpetion1 e1){
  e1.getMessage(); //예외흐름
}catch(Excpetion2 e2){
  e2.getMessage(); //예외흐름
}finally{
  //무조건 실행해야 하는 흐름
}

```

- ⭐️ `try-catch`에서 어떤 예외가 터지더라도 무조건 반드시 `finally`의 코드는 실행

```java
public class NetworkServiceV2_4 {
    public void sendMessage(String data) {
        String address = "http://example.com";
        NetworkClientV2 client = new NetworkClientV2(address);

        client.initError(data);

        try {
            //하나의 try안에 정상흐름을 다 담기
            client.connect();
            client.send(data);
        } catch (NetworkClientExceptionV2 e) {
            //catch안에 예외흐름
            //👍🏻 try, catch으로 정상흐름, 예외흐름 분리 성공
            System.out.println("[error log]" + e.getErrorCode() + " message" + e.getMessage());
        }finally{ //⭐️ 반드시 실행
            client.disconnect();
        }
    }
}
```

## ✅ Exception layers

- Exception에 계층을 두어 계층별로 예외 잡기

- Runtime exception
  - NetworkClientException `extends Runtime exception`
    - Connect Exception, SendException `extends NetworkClientException`

```java
try {
// 1. RuntimeException 발생
  } catch (ConnectException e) { // 2. 대상이 다름
  } catch (SendException e) // 2. 대상이 다름
  } catch (NetworkClientException e) { // 3.대상이 다름
  } catch (Exception e) { // 4.Exception은 RuntimeException의 부모이므로 여기서 잡음
}
```

## ✅ Try with resources

- 쓰고 반드시 반납해야 하는 resource/class에 `implements AutoCloseable`하고
- 꼭 실행해야 하는 메소드를 `close()`안에 넣는다

```java
public class NetworkClientV5 implements AutoCloseable{
      public void disconnect(){} //반드시 실행해야 하는 코드

      @Override
      public void close() { //close()안에 꼭 실행해야 하는 코드 넣기
        disconnect();
    }

}
```

- ✔️ Main class
- `ry(NetworkClientV5 client = new NetworkClientV5(address))`

```java
try(NetworkClientV5 client = new NetworkClientV5(address)) { //close하는 메소드 있는 클래스를 try에서 인스턴스 생성
            client.initError(data);
            client.connect();
            client.send(data);
        }
```

## ✅

## ✅

## ✅

## ✅
