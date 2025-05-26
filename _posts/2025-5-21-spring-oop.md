---
title: SOLID, DI
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

# ✅ What is a good OOP

> distinguish **role** and **implementation**

- ✔️ `role`: **interface**, **abstraction**
- what something should do
- ex) `OrderService`, `MemberRepository`

- ✔️ `implementation`: **class** that implements interface
- how to do
- ex) `OrderServiceImpl`, `JpaMemberRepository`

- ➡️ `DIP`, `ISP`를 지킨다
- 👍🏻 향후 구체 클래스가 바뀌더라도 쉽게 바꿔끼워 대처할 수 있다

# ✅ SOLID

- SRP
- OCP
- LSP
- ISP
- DIP

## ☑️ Single Responsible principle

- one class should have one responsibility
- when extended, modification should be minimized
- ex) `MVC`: model, view, controller code is distinguished
- ex) `controller`, `service`, `repository`

## ☑️ Open Closed principle

- open for extension, closed for modification
- do not modify client code, modify concrete class only
- should be able to add `Fish`, without changing `Animal`, `Dog` class
- use polymorphism, interface

<!-- ```java
public class MemberService{
    //MemberRepository repo = new JDBCMemberRepository();
    MemberRepository repo = new JPAMemberRepository();
}
``` -->

## ☑️ Liskov Substitution principle

- correctly use inheritence without breaking the program
- Objects of a superclass should be **replaceable** with objects of its subclass

- If `Bird superclass` has `fly()` method
- `Penguin extends Bird` should override `fly()` and penguin should be able to fly ➡️ bad LSP
- `Parrot extends Bird` should override `fly()`. If parrot eats instead of flying ➡️ bad LSP
- thus, create `Bird superclass` and `Flyable interface` with `fly()`
- `Penguin extends Bird` only
- `Parrot extends Bird implements Flyable`

## ☑️ Interface Segregation principle

- instead of having one large interface with many unrelated methods, break it into **smaller** more specific interfaces
- `Car` class can have `Drive interface` and `Fix interface`
- can have `driver client class` and `engineer client class`
- even when `Fix interface` is modified, `driver client class` does not have to be altered

## ☑️ Dependency Inversion principle

- depend on `abstract` or `interface`, not on a certain class

# 👎🏻 Bad example of solid

- `OrderServiceImpl` is client code
- `OrderServiceImpl` needs `DiscountPolicy`
- so, created `DiscountPolicy interface`
- then, created `FixDiscountPolicy implements DiscountPolicy`
- however, decided to change business logic from **Fix ➡️ Rate**
- now, `OrderServiceImpl` needs `RateDiscountPolicy`
- 1️⃣ 👎🏻 have to change `OrderServiceImpl`

- 1️⃣ 👎🏻 OCP: need to modify client code
- 2️⃣ 👎🏻 DIP: relying on a concrete class, instead of interface or abstract

```java
public class OrderServiceImpl implements OrderService {

//  private final DiscountPolicy discountPolicy = new FixDiscountPolicy();
    private final DiscountPolicy discountPolicy = new RateDiscountPolicy(); // 👎🏻 OCP, DIP 못 지킴
}
```

- `OrderServiceImpl`은 주문하는 business logic만 가지고 있어야 하는데
- `DiscountPolicy`도 받아와야 하는 책임도 있음
- 3️⃣ 👎🏻 `OrderServiceImpl`은 책임이 너무 많음!
- 👎🏻 `SRP`

- ✔️ bad example of stucture in image
  <img width="476" alt="Image" src="https://private-user-images.githubusercontent.com/97790983/446953140-79c0a921-3378-4265-a606-9d70d397126e.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDc5OTI4MDYsIm5iZiI6MTc0Nzk5MjUwNiwicGF0aCI6Ii85Nzc5MDk4My80NDY5NTMxNDAtNzljMGE5MjEtMzM3OC00MjY1LWE2MDYtOWQ3MGQzOTcxMjZlLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA1MjMlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwNTIzVDA5MjgyNlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTk0OTU0Zjc1ZTA3ZDE4NWJjNDY1NDUzMmZhYTU3ZjI3NTJiNzExOGFlMjBhYzA2NDMzYTlkNGIyZWY5ZTdmM2QmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.J0utADhPCfuX2Td4l3DnAhaExnS8mnwWVoSdMmDYvqU" />

- `OrderServiceImpl` should only depend on interface `DiscountPolicy`
- however, in this case, depends both on interface and on concrete class `FixDiscountPolicy`

# 👍🏻 Implement SOLID

- implement `AppConfig`

- 이제 `OrderServiceImpl`은 **생성자**를 통해 `DiscountPolicy`를 **주입**받는다
- ⭐️ Dependency Injection
- 3️⃣ `OrderServiceImpl`는 fix인지 rate인지 전혀 모른다! 나는 이제 비즈니스 로직에만 집중하면 된다. ➡️ **SRP**
- 2️⃣ only rely on abstract `interface DiscountPolicy` ➡️ **DIP**
- 1️⃣ fix에서 rate으로 변경되더라도 client code인 `OrderServiceImpl`는 바뀌지 않는다 ➡️ **OCP**

```java
public class OrderServiceImpl implements OrderService {
    private final DiscountPolicy discountPolicy; //DIP, Dependency Injection

    public OrderServiceImpl(DiscountPolicy discountPolicy) {
        this.discountPolicy = discountPolicy;
    }

//SRP
//only business logic
```

- 그리고 별도의 클래스 `AppConfig`를 만들어 의존관계를 관리한다.
- 이제 **Fix ➡️ Rate**으로 바꿔도 `OrderServiceImpl`은 바뀌는게 없음
- `AppConfig`만 바꿔주면 됨

```java
public class AppConfig {

    public OrderService orderService(){
        return new OrderServiceImpl(new FixDiscountPolicy());
    }
}

//여기서 Rate으로 바꾸면?
//AppConfig만 바꾸면 됨, OCP
public class AppConfig {

    public OrderService orderService(){
        return new OrderServiceImpl(new RateDiscountPolicy());
    }
}
```

- 👍🏻 `OrderServiceImpl` has **SRP**
- 👍🏻 `OrderServiceImpl` does _not_ rely on a concrete class, relies on interface ➡️ **DIP**
- 👍🏻 application maintains **OCP**, only has to modify `AppConfig`, and not modify client code

- now, config and business logic is totally seperate

<img width="495" alt="Image" src="https://private-user-images.githubusercontent.com/97790983/446952518-8e305f1f-e4e2-428e-8326-fd4ea7d4a8cd.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDc5OTI2OTIsIm5iZiI6MTc0Nzk5MjM5MiwicGF0aCI6Ii85Nzc5MDk4My80NDY5NTI1MTgtOGUzMDVmMWYtZTRlMi00MjhlLTgzMjYtZmQ0ZWE3ZDRhOGNkLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA1MjMlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwNTIzVDA5MjYzMlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWVjYzM1MWRmOWE2OGU3MGQ5N2Y5NGQ2MjAzNDZkNmU2ODlkNTAxYjhjNzE1MDY4YmJkNzgwMjc0NjQ1MzBjNDImWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.uzhmXJR2BQfnUTMLAKdY4anPw2b5CXl8_lc4XlsOvRA" />

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅
