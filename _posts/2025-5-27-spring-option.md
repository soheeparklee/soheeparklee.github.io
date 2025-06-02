---
title: SpringBean Annotations
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ Bean이 null인 경우 처리 방법

- to make bean null
- `@Autowired`히고
- SpringBean을 넣을지, 안 넣을지 정할 수 있다

### 💡 Required = false

- `Member`이 `null`이면 `setter`을 호출하지 않음

```java
@Autowired(required = false)
    public void setNoBean1(Member member1){
    }
```

### 💡 @Nullable

- `Member`이 `null`이면 `null`이라고 출력

```java
@Autowired
    public void setNoBean2(@Nullable Member member2){
    }
```

### 💡 Optional<>

- `Optional<>`로 감싸면 객체가 `null`일 수 있음
- `Member`이 `null`이면 `Optional.empty`로 출력

```java
@Autowired
    public void setNoBean3(Optional<Member> member3){
    }
```

## ✅ 같은 타입의 Bean이 여러 개 있을 때 우선순위

- To choose one bean out of several

- If there are two `DiscountPolicy`
  - `FixedDiscountPolicy`
  - `RateDiscountPolicy`
- I want to choose what `DiscountPolicy` bean to create

### 💡 @Autowired field name

- 필드명을 빈 이름으로 변경

```java
//before
@Autowired
private DiscountPolicy discountPolicy

//after
@Autowired
private DiscountPolicy rateDiscountPolicy //구체적인 이름 적기
```

- DI할 때 구체적인 이름 적어서 의존성 주입

```java
public OrderServiceImpl(MemberRepository repository, DiscountPolicy rateDiscountPolicy) {
        this.repository = repository;
        this.discountPolicy = rateDiscountPolicy;
    }
```

### 💡 @Qualifier

- `@Qualifier`: 추가 구분자
- 빈 등록 시 각 구체 클래스에 `@Qualifier` 이름 지정
- 제일 우선순위가 높다

```java
@Component
@Qualifier("mainDiscountPolicy")
public class RateDiscountPolicy implements DiscountPolicy {}

@Component
@Qualifier("fixDiscountPolicy")
public class FixDiscountPolicy implements DiscountPolicy {}
```

- 이후 어떤 빈을 DI할지 결정

```java
    public OrderServiceImpl(MemberRepository repository, @Qualifier("fixDiscountPolicy") DiscountPolicy discountPolicy) {
        this.repository = repository;
        this.discountPolicy = discountPolicy;
    }
```

### 💡 @Primary

- 빈 간의 우선순위 지정
- 이렇게 `@Primary` 붙이면 `RateDiscountPolicy`가 주입된다

```java
@Component
@Primary
public class RateDiscountPolicy implements DiscountPolicy{}
```

## ✅ Create my own annotation

- can also create my annotation

```java
@Target({ElementType.FIELD, ElementType.METHOD, ElementType.PARAMETER,
        ElementType.TYPE, ElementType.ANNOTATION_TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Qualifier("mainDiscountPolicy")
public @interface MainDiscountPolicy {

}
```

- use my own `MainDiscountPolicy` annotation

```java
@Component
@MainDiscountPolicy
public class RateDiscountPolicy implements DiscountPolicy{
```

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅
