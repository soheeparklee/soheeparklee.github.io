---
title: Spring Container and Bean with configuration class
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ Spring Container and Bean

- ✔️ Spring container: manage object creation and `DI` and overall flow of the application
  - Spring container 🟰 `ApplicationContext`
- ✔️ `Bean`: Object that is added to `Spring container`

  - Java object that is managed by the Spring container
  - special object that Spring takes care for you - creates, manages dependencies, manage life cycle

- add annotation `@Configuration`
- Spring container will use `@Configuration` as `DI information/metadata`

- Spring container wil call all methods with `@Bean` and add it to spring container
- only creates the `@Bean` **once**

## 💡 How to add Bean

- `@Bean`등록하는 방법
- 1️⃣ manual bean configuration with `@Configuration`
- 2️⃣ component scan with `@ComponentScan`, `@Autowired`
- 이 게시글에서는 1️⃣번 방법에 대해 설명한다

- 1️⃣ **Create Spring container `@Configuration` class**

```java
@Configuration
public class AppConfig {
}
```

```java
ApplicationContext applicationContext = new AnnotationConfigApplicationContext(AppConfig.class);

//get memberService from AppCofig called by Spring container
MemberService memberService = applicationContext.getBean("memberService", MemberService.class);

```

<img width="507" alt="Image" src="https://private-user-images.githubusercontent.com/97790983/446997503-dbfb212a-a97c-4286-a3f7-42cc0d92208a.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDgwMDA5MzQsIm5iZiI6MTc0ODAwMDYzNCwicGF0aCI6Ii85Nzc5MDk4My80NDY5OTc1MDMtZGJmYjIxMmEtYTk3Yy00Mjg2LWEzZjctNDJjYzBkOTIyMDhhLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA1MjMlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwNTIzVDExNDM1NFomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWE0NmJlOTExMzVhNTU4MjJmNWQ0NTVmMTkwZjY1NDI0YzIzNGEwMjhlN2Y5MGJiNTNmYzFhNGZlZDZhZTZlMTkmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.WR4MnLil8cJ54yWgvEkMxH7j3XKaO8gEp0LAJTbUAFw" />

- 2️⃣ **Add beans to Spring container**
- add `@Bean` as Spring bean to Spring container

```java
@Configuration
public class AppConfig {

    @Bean
    public MemberService memberService(){
        return new MemberServiceImpl(memberRepository());
    }
```

<img width="495" alt="Image" src="https://private-user-images.githubusercontent.com/97790983/446997883-0f4b2d10-dc9d-40bf-a12e-a0304bfc24d7.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDgwMDEwMDMsIm5iZiI6MTc0ODAwMDcwMywicGF0aCI6Ii85Nzc5MDk4My80NDY5OTc4ODMtMGY0YjJkMTAtZGM5ZC00MGJmLWExMmUtYTAzMDRiZmMyNGQ3LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA1MjMlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwNTIzVDExNDUwM1omWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTc2NDNiNzc3OGI3ZDhjZmJiMDFhYWEwYTJjMGQ3YmVhYTkxMzc5NWNkMGMzYzZjNGJjODQwZmE0ODE0MmZiYjImWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.6LC3UQvFOdcBqW9hDfL2Oxq16aYVQ3bpvOu5yDxpHpg" />

## ✅ Get beans in test code

```java
AnnotationConfigApplicationContext ac = new AnnotationConfigApplicationContext(AppConfig.class);

//print all beans
String[] beanDefinitionNames = ac.getBeanDefinitionNames();

//find bean by name
MemberService memberService = ac.getBean("memberService", MemberService.class);

//find bean by type
//이 때 type아래 여러개 있으면 에러
MemberService memberService = ac.getBean(MemberService.class);

//type아래 있는 모든 bean 다 find
Map<String, MemberRepository> beansOfType = ac.getBeansOfType(MemberRepository.class);
```

- 부모 type으로 `bean`을 찾아오면 부모 ➕ 그 자식들도 모두 찾아온다
- bean not found: `NoSuchBeanDefinitionException`
- 하나의 클래스 안에 bean이 여러개: `NoUniqueBeanDefinitionException`

## ✅ Bean Factory

> `ApplicationContext` implements ➡️ Bean Factory(interface)

- ✔️ `Bean Factory`: manage and find beans

  - `getBean()`, `getBeansOfType()` 메소드 등 모두 Bean Factory의 기능이다

- Spring container인 `ApplicationContext`은 `Bean Factory`를 상속받아
- `Bean Factory`의 기능들에 자신의 기능들을 추가해서 Spring container를 구현한다.
