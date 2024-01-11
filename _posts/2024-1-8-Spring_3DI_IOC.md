---
title: AOP, PSA, Bean, DI, IoC
categories: [JAVA, Spring]
tags: [di, ioc, bean] # TAG names should always be lowercase
---

## ✅ Spring 3대 요소

![코딩공책-19](https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/bf7184c4-1d01-4e79-997f-c05fe556795e)

- JAVA OOP
- JAVA meta programming
- JAVA design pattern

#### ⭐️ AOP

> Aspect Oriented Programming
> 관점 지향형 프로그래밍

#### ⭐️ PSA

> Portable Service Abstraction
> 일관성 있는 추상화

#### ⭐️ IOC/DI

> 의존성 주입, 제어의 역전

- DI(Dependency Injection)
- IOC(Inversion of Control)

## ✅ 스프링 컨테이너에 빈 등록하기

기본적으로 싱글톤 패턴으로 구현이 된다.<br>
(여러 스레드가 하나의 객체 사용)<br>
따라서 멀티쓰레딩으로 자원을 공유한다.<br>

#### 빈 등록하기 방법 1

<img width="1028" alt="스크린샷 2024-01-08 오후 3 34 45" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/f4e08064-6f5c-4ab1-a0ec-2b9c0d0a03bc">

#### 빈 등록하기 방법 2

<img width="1035" alt="스크린샷 2024-01-08 오후 3 37 02" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/7ad1da49-b465-42e2-8b67-f816c83edfc0">

## ✅ IOC

> 제어의 역전
> 우리가 빈을 만들고 해당 클래스의 객체를 만들면, 이제는 우리가 아니라 **스프링 컨테이너가 직접 생성하고 관리한다.**
> 서블릿 컨테이너의 흐름으로 제어되는 것 ➡️ 제어의 역전

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
