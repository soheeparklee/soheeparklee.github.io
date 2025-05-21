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

<img width="208" alt="Image" src="https://github.com/user-attachments/assets/46eaf4ca-218f-400e-a3ee-7bd2a9fcc909" />

- 👍🏻 AOP 적용 후:
- `cross-cutting concern` and `core concern` 분리
- `cross-cutting concern`: 시간 재기
- `core concern`: 쇼핑몰 메소드
- getTime하는 클래스`TimeTraceApp`를 만들고, 이 클래스를 메소드가 실행될 때 적용시킨다
- 시간을 측정하는 로직을 별도의 공통 로직으로 따로 빼서 만들었다
- 그리고 `@Around`를 사용해 원하는 적용 대상을 선택해 적용시켰다.

<img width="307" alt="Image" src="https://github.com/user-attachments/assets/f669fe5a-0b31-4c23-aa8d-4087fa86076a" />

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
