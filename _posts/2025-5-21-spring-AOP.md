---
title: Aspect Oriented Programming
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ AOP

- Distinguish between `cross-cutting concern` and `core concern`
- `공통 관심 사항`과 `핵심 관심 사항`을 분리하기

- 예를 들어 `회원가입`, `상품 조회`, `주문, 구매`등 하는 쇼핑몰이 있다고 하자
- 그런데 성능 측정을 위해 `회원가입`, `상품 조회`, `주문, 구매` 메소드 시간을 측정하고 싶다
- 👎🏻 AOP 적용 전: `회원가입`, `상품 조회`, `주문, 구매` 각 메소드에 getTime하는 함수를 붙여 코드를 바꿔야 한다
- 👎🏻 비즈니스 로직과 `cross-cutting concern`이 섞여서 코드 구성, 유지보수 어려움

<img width="208" alt="Image" src="https://private-user-images.githubusercontent.com/97790983/446046534-46eaf4ca-218f-400e-a3ee-7bd2a9fcc909.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDc4NTI0MTYsIm5iZiI6MTc0Nzg1MjExNiwicGF0aCI6Ii85Nzc5MDk4My80NDYwNDY1MzQtNDZlYWY0Y2EtMjE4Zi00MDBlLWEzZWUtN2JkMmE5ZmNjOTA5LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA1MjElMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwNTIxVDE4MjgzNlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTQ4ZDIxYzdhMjljOTE3MjhjODc1NjhmNjkxZTQyZjM4YWUyZWRkYjFjMDU2MDYyNzVkZjA4YzA5NzE3Y2Q3NWMmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.iQOh9osDQW0IHDcXCouOgkCgS-OMWcx9oNtTFZkWRgM" />

- 👍🏻 AOP 적용 후:
- `cross-cutting concern` and `core concern` 분리
- `cross-cutting concern`: 시간 재기
- `core concern`: 쇼핑몰 메소드
- getTime하는 클래스`TimeTraceApp`를 만들고, 이 클래스를 메소드가 실행될 때 적용시킨다
- 시간을 측정하는 로직을 별도의 공통 로직으로 따로 빼서 만들었다
- 그리고 `@Around`를 사용해 원하는 적용 대상을 선택해 적용시켰다.

<img width="307" alt="Image" src="https://private-user-images.githubusercontent.com/97790983/446046686-f669fe5a-0b31-4c23-aa8d-4087fa86076a.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDc4NTk1NTQsIm5iZiI6MTc0Nzg1OTI1NCwicGF0aCI6Ii85Nzc5MDk4My80NDYwNDY2ODYtZjY2OWZlNWEtMGIzMS00YzIzLWFhOGQtNDA4N2ZhODYwNzZhLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA1MjElMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwNTIxVDIwMjczNFomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWE3NThjYzVkOWQxMmQxMWZmYmM2YWJlYjE0MGVmNzdmYTc5YTA4YmQ0Y2I4ZDlmMDdlMmU4YTE1OWYwZmUyYTAmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.4Yrm_6SThFGM20Qnx1_Ru4CXLPK8Ismc5IEjkQC25TA" />

```java
@Aspect //aspect of programming
@Component //component scan
public class TimeTraceApp {

    @Around("execution(* com.example.java_spring..*(..))") //이 공통 관심사를 어디에 적용시킬지
    //이 경우 com.example.java_spring 밑에 있는 모든 파일에 적용
    public Object execute(ProceedingJoinPoint joinPoint) throws Throwable{
        long start = System.currentTimeMillis();
        try{
            Object result = joinPoint.proceed();
            return result;
        }finally{
            long finish = System.currentTimeMillis();
            long timeMs = finish - start; //시간 재는 로직
        }
    }
}
```

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅
