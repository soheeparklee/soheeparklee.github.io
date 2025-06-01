---
title: Singleton
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ Singleton

- create **only one** instance(object) of its kind
- and **share** among other code, providing a single point of access

```java
public class SingletonService {
    //create myself within myself
    private static final SingletonService instance = new SingletonService();

    //private constructor, cannot create from outside
    private SingletonService(){}

    //only accessible through getter
    public static SingletonService getInstance(){
        return instance;
    }
}
```

## ✅ Spring container is singleton

- When `@Bean` is added to `Spring container`,
- `Spring container` manages the `@Bean` as **singleton**
- Thus, creates **only one** bean, and **share** among all other codes

## ✅ Singleton container(🟰 Spring container)

- create singleton container `ApplicationContext`
- set `AppConfig.class` as DI metadata(information)
- now, all `@Beans` are **singleton**
- 👍🏻 so `memberService1 == memberService2`

```java
@Test
@DisplayName("springcontainer and singleton")
void singletonContainerTest(){
    ApplicationContext ac = new AnnotationConfigApplicationContext(AppConfig.class);

    MemberService memberService1 = ac.getBean("memberService", MemberService.class);
    MemberService memberService2 = ac.getBean("memberService", MemberService.class);

    assertThat(memberService1).isSameAs(memberService2);
    }
```

## ⚠️ Singleton 주의사항

- singleton class should be **stateless**
- singleton is **shared** by several codes
- should not be altered by a specific code

```
- orderService는 bean으로 등록되어 singleton으로 관리
- orderService는 상품 가격을 field로 가지고 있었음
- 주문자A가 1000원을 주문
- 주문자B가 2000원을 주문
- orderService는 singleton이므로 주문자A, 주문자B가 공유
- 그래서 주문자A가 주문내역을 봤더니 ➡️ ⚠️ 2000으로 가격이 찍힘!
- 💡 따라서 orderService는 상품 가격을 field로 가지고 있으면 안 됨
- 💡 singleton should be stateless
```

## ✅ @Configuration and singleton

- `@Configuration`가 붙어있는 클래스는 `Spring container`이 `DI`를 위한 설정 파일로 생각
- `@Configuration`클래스의 메소드를 `@Bean`에 등록한다.
- `@Bean`에 등록되면 `Spring container`가 manage, dependency inject
- create **only one** `@Bean` and **share**
- 같은 bean이 생성되는 메소드 코드가 여러번 있어도 **딱 한번만** bean생성, 공유
- ➡️ guarantee **singleton**
- `@Configuration`은 `CGLIB 라이브러리`를 이용해 설정 클래스를 상속받는 `프록시 객체`를 만들고, 이 프록시를 통해 `@Bean` 메소드 호출을 가로채서 싱글톤을 보장

## ✅

## ✅

## ✅

## ✅

## ✅
