---
title: IoC, DI
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ Inversion of Control

- control flow is inversed from programmer to ➡️ **external source**(ex: `framework`)
- `Framework` will call my code, not the programmer

- 👎🏻 **Before IoC**
- programmer explicitly codes what class will be used in `Service client code`
- `Service client code` knows what concrete class it will use

```java
public class OrderServiceImpl implements OrderService {

//  private final DiscountPolicy discountPolicy = new FixDiscountPolicy();
    private final DiscountPolicy discountPolicy = new RateDiscountPolicy();
}
```

- 👍🏻 **After IoC**
- `Service client code` does not know what concrete class will be used
- controlled by `AppConfig`
- control flow is inversed to `AppConfig`

```java
public class OrderServiceImpl implements OrderService {
    private final DiscountPolicy discountPolicy; //no concrete class, only interface
}
```

```java
public class AppConfig {

    public OrderService orderService(){
        return new OrderServiceImpl(new FixDiscountPolicy());
    }
}
```

## ✅ Dependency Injection

> Spring automatically gives one bean to another bean that needs it <br>

- 👍🏻 OCP: can refrain from modifying service code, only has to modify config file
- 👍🏻 instead of creating object manually, you let Spring inject it

- ✔️ **static DI**: can see DI even without running code

  - `extends`, `implements`
  - `import`

  ```java
  @Component
  public class OrderServiceImpl implements OrderService {

      private final MemberRepository repository;
      private final DiscountPolicy discountPolicy;

      @Autowired
      //constructor
  }
  ```

  - `OrderServiceImpl` depends on `OrderService`, `MemberRepository`, `DiscountPolicy`
  - `MemberRepository`, `DiscountPolicy` is **injected** into `OrderServiceImpl`

- ✔️ **dynamic DI**: check DI when code is run

  ```java
  public class AppConfig {

  public OrderService orderService(){
      return new OrderServiceImpl(new MemoryMemberRepository(), new RateDiscountPolicy());
  }
  ```

  - when AppConfig is **run** and `orderService` is created, return conrete class `new OrderServiceImpl`
  - when `OrderServiceImpl` is created, create conrete class `MemoryMemberRepository` and `RateDiscountPolicy`

## ✅ IoC, DI container

- tool that helps `create object` and `handle, connect dependencies`
- tool to help `IoC` and `DI`
  - ex) `AppConfig` is an example of `IoC, DI container`
  - `AppConfig` handles `DI` for `OrderService`

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅
