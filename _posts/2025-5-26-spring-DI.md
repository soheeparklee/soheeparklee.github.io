---
title: 4 ways to inject dependency and Lombok
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ 4 Ways to inject dependency

- constructor
- setter
- field
- method

## 💡Constructor dependency injection

- 👍🏻 recommended
- Injected at the moment when object is **created** with constuctor
- 👍🏻 only called once, **never can be changed** again
- dependency cannot be changed at runtime
- 👍🏻 used for `final`, `immutable`
- dependency is **required**
- `@Autowired` can be ommited if there is only one constuctor

```java
@Component
public class OrderServiceImpl implements OrderService {
    private final MemberRepository repository; //final, immutable
    private final DiscountPolicy discountPolicy;

    @Autowired //constuctor dependency injection
    public OrderServiceImpl(MemberRepository repository, DiscountPolicy  discountPolicy) {
        this.repository = repository;
        this.discountPolicy = discountPolicy;
    }
```

## 💡 Setter dependency injection

- when injecting dependency should be changeable
- used for `mutable`, more flexible
- dependency is **not** necessarily required

```java
@Component
public class OrderServiceImpl implements OrderService {
    private  MemberRepository repository; //mutable
    private  DiscountPolicy discountPolicy;

    @Autowired
    public void setRepository(MemberRepository repository) {
        this.repository = repository;
    }

    @Autowired(required = false) //dependency is not necessarily required
    public void setDiscountPolicy(DiscountPolicy discountPolicy) {
        this.discountPolicy = discountPolicy;
    }
```

## 💡 Field dependency injection

- ⚠️ not recommended
- dependency injected directed into class field
- code looks very simple
- 👎🏻 however, field cannot be changed from outside this class
- 👎🏻 difficult to write test code
- 👎🏻 cannot use `final`

```java
@Component
public class OrderServiceImpl implements OrderService {

    @Autowired private  MemberRepository repository;
    @Autowired private  DiscountPolicy discountPolicy;
}
```

## 💡 Method dependency injection

- ⚠️ not used frequently
- dependency is passed as parameter
- used when dependency is only needed temporarily

## ✅ Lombok

- `annotation`을 통해서 자동으로 만들어준다.
- `constructor`, `getter`, `setter`, `toString` 등를 자동으로 만들어준다

- 👎🏻 **DI with constructor before using Lombok**

```java
@Component
public class OrderServiceImpl implements OrderService {
    private final MemberRepository repository;
    private final DiscountPolicy discountPolicy;

    //needed to code constructor
    public OrderServiceImpl(MemberRepository repository, DiscountPolicy discountPolicy) {
        this.repository = repository;
        this.discountPolicy = discountPolicy;
    }
}
```

- 👍🏻 **DI with constructor with Lombok**
- `@RequiredArgsConstructor`: create constructor with `final` fields

```java
@Component
@RequiredArgsConstructor //lombok creates constructor
public class OrderServiceImpl implements OrderService {
    private final MemberRepository repository;
    private final DiscountPolicy discountPolicy;
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
