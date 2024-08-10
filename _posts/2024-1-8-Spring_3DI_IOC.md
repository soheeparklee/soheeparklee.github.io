---
title: AOP, PSA, Bean, DI, IoC
categories: [JAVA, Spring]
tags: [di, ioc, bean, aop, oop, psa] # TAG names should always be lowercase
---

## ✅ Spring 3대 요소

![코딩공책-19](https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/bf7184c4-1d01-4e79-997f-c05fe556795e)

- JAVA OOP
- JAVA meta programming
- JAVA design pattern

## ⭐️ POJO

> Plain Old Java Object <br>
> 깔끔하고 정통적인 JAVA OOP를 가능하게 함<br>

simple java classes that does NOT depend on any Spring specific interfaces or classes.<br>
for exmaple, **DTOs**<br>
thanks to the use of pojos, we can have loose coupling and easy integration with other components in the framework. <br>

## ⭐️ AOP

> Aspect Oriented Programming <br>
> 관점 지향형 프로그래밍 <br>

<br>

- 공통의 관심 사항을 적용
- 공통 사항 구현한 모듈에 대한 의존 관계 ❌
- aspect를 이용해 핵심 로직을 구현한 각 클래스에 공통 기능 적용

> Cross Cutting concern <br>
>
> > aspects of program that affect multiple parts of the applcation <br>

- in AOP, **modularize** the `cross cutting concerns` into seperate unit called **aspect**
- addressing cross-cutting **concerns** in a more modular and centralized way

<br>

- Aspect: 여러 객체에 공통으로 적용되는 공통 관심 사항
  - concern that cuts across multiple classes
- Advice: action taken by aspect at a certain **time**
  - 모아서 구현해 둔 코드, 이 코드를 필요할 떄 침투시킨다
- Join Point: specific point **where** aspect can be applied
- Pointcut: specify **where** advice should be applied, `join point`의 부분집합
- Weaving: process of linking apsect w target object
- **모듈화**: 횡단 관심사를 따로따로 반복되게 코드를 작성하는게 아니라, 한 곳에 **모아서** 처리

### 🔎 Exmaple of AOP

- logging
- 공통 에외처리: 예외들이 비슷비슷하니까 예외들만 ExceptionControllerAdvice에 모아서(모듈화) 적용(침투적용)
- 트랜잭션: 공통 데이터 원자화(몽땅 실패하거나 몽땅 성공하거나)

<img width="716" alt="스크린샷 2024-01-16 오후 3 52 23" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/aee560a9-c741-4130-8d1a-e4cd464ad6cf">

## ⭐️ PSA

> Portable Service Abstraction
> 일관성 있는 추상화

특정 기술에 접근하는 것이 아니라 ❌ <br>
**스펙을 추상화**해서 사용 <br>
👍🏻 코드 이식성, 유용성 향상 <br>

### 🔎 Exmaple of PSA <br>

JPA JPQL을 사용하면 여러 DB의 기술을 추상화한다. <br>
따라서 DB에 따라 언어가 조금씩 달라도 JAVA에서는 문제없이 사용 가능하다. <br>

## ✅ Bean

> a set of conventions for designing and creating **reusable** software components in Java.<br>
> JavaBeans are often designed to be serializable, which means they can be easily saved to a persistent storage or transmitted over a network.<br>
> Default constructor is required for JavaBean<br>

### 💡 스프링 컨테이너에 빈 등록하면 싱글톤 패턴 구현

기본적으로 싱글톤 패턴으로 구현이 된다.<br>
(여러 스레드가 하나의 객체 사용)<br>
따라서 **멀티쓰레딩**으로 자원을 공유한다.<br>

### 💡 Bean등록하는 방법

1. `@Bean annotaion` 추가

<img width="1028" alt="스크린샷 2024-01-08 오후 3 34 45" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/f4e08064-6f5c-4ab1-a0ec-2b9c0d0a03bc">

2. `@Component` 추가

<img width="1035" alt="스크린샷 2024-01-08 오후 3 37 02" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/7ad1da49-b465-42e2-8b67-f816c83edfc0">

## ⭐️ IOC/DI

> 의존성 주입, 제어의 역전 <br>
> Bean이 넣어준다. <br>

- DI(Dependency Injection) <br>
- IOC(Inversion of Control) <br>

## ✅ IOC

> 제어의 역전 <br>
> 우리가 Bean을 만들고 해당 클래스의 객체를 만들면, 이제는 우리가 아니라 **스프링 컨테이너가 직접 생성하고 관리한다.** <br>
> 스프링 컨테이너는 서블릿 컨테이너 위에서 동작 ➡️ 서블릿 컨테이너의 흐름으로 제어되는 것 ➡️ 제어의 역전 <br>

## ❓ JAVA 클래스 의존이란?

한 클래스가 다른 클래스의 동작에 영향을 받는 경우 <br>
객체 생성 시, 다른 클래스 의존성이 생기는 경우 <br>
<br>
개발자가 직접 클래스 간 의존성 설정하는 코드 <br>

```java
public class classB {
    public String sayHello(){
        return "I am B";
    }
}

public class classA {
    private classB classB; //classA는 classB에 의존하는 상황

    public classA(classB classB) {
        this.classB = classB;
    }
    public classA(){
    }
    public void setClassB(classB classB) {
        this.classB = classB;
    }
    public void sayHello(){
        String message= classB.sayHello() + "and I am A";
        System.out.println(message);
    }
}

public class Main {
    public static void main(String[] args) {
        classA classA= new classA();
        classA.sayHello(); //실행❌
        // classB에서 받아와야 하는데 null을 받아오기 떄문에 실행 불가.
        //따라서 classA는 classB에게 의존성을 가진다.

        //⭐️의존성 푸는 방법
        //1. 생성자로 넣기
        classB classB= new classB();
        classA classA2= new classA(classB);

        classA2.sayHello(); //실행 가능

        //2. setter
        classA.setClassB(classB);
        classA.sayHello();

    }
}
```

## ✅ DI

> Dependency Injection

스프링 컨테이너가 직접 의존성을 주입해준다. <br>
빈을 생성하면 빈이 스프링 컨테이너의 것이 되니 스프링 컨테이너가 빈으로 의존성 넣어준다. <br>
대신 개발자가 넣을 방법은 아래 3가지 중 어떻게 넣을지 정해주어야 한다. <br>
 <br>

1. Field Injection <br>
2. setter Injection <br>
3. constructor Injection <br>
   그리고 constructor통해 생성하는건 `@Autowired` 생략 가능함 <br>

```java
@Component
public class MyComponent2 {
    public String sayHello(){
        return "I am myComponent 2";
    }
}

// 1. Field Injection
@Component
public class MyComponent1 {
    private MyComponent2 myComponent2;
    @Autowired
    public void sayHello(){
        String message= myComponent2.sayHello()+ "and I am A";
        System.out.println(message);
    }
}
// 2. setter Injection
@Component
public class MyComponent1 {
    private MyComponent2 myComponent2;

    public void sayHello(){
        String message= myComponent2.sayHello()+ "and I am A";
        System.out.println(message);
    }
    @Autowired
    public void setMyComponent2(MyComponent2 myComponent2) {
        this.myComponent2 = myComponent2;
    }
}
// 3. constructor Injection
@Component
public class MyComponent1 {
    private MyComponent2 myComponent2;

    public void sayHello(){
        String message= myComponent2.sayHello()+ "and I am A";
        System.out.println(message);
    }

    public void setMyComponent2(MyComponent2 myComponent2) {
        this.myComponent2 = myComponent2;
    }
    @Autowired
    public MyComponent1(MyComponent2 myComponent2) {
        this.myComponent2 = myComponent2;
    }
}
```
