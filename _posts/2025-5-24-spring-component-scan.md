---
title: Bean with Component Scan(2)
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## 💡 How to add Bean

- `@Bean`등록하는 방법
- 1️⃣ manual bean configuration with `@Configuration`
- 2️⃣ component scan with `@ComponentScan`, `@Autowired`
- 이 게시글에서는 2️⃣번 방법에 대해 설명

## ✅ Component Scan

- Spring does not magically know what to add as bean ➡️ scans your project marked as bean
- this scanning is called: `@Component Scan`

- `@Component Scan`은 `@Component` 어노테이션이 붙은 클래스는 모두 `Spring Bean`으로 알아서 등록한다.
  - `@Component`
  - `@Controller`
  - `@Service`
  - `@Repository`
  - `@Configuration`
- 의존성 주입: `@Autowired`
- `@Autowired`가 붙은 생성자는 자동으로 해당 `Spring Bean`을 찾아서 의존성을 주입한다.

- 1️⃣ **(before)manual bean configuration**
- `Bean`으로 등록하고 싶은 클래스들을 `AppConfig`에 명시해야 했음

```java
@Configuration
public class AppConfig {

    @Bean
    public MemberService memberService(){
        return new MemberServiceImpl(memberRepository());
    }

    @Bean
    public OrderService orderService(){
        return new OrderServiceImpl(
                memberRepository(),
                discountPolicy());
    }
}
```

- 2️⃣ **component scan with** `@ComponentScan`
- 이제 `config`피일은 텅텅 비었다!
- `@ComponentScan`은 `@Component`가 붙은 클래스를 찾아 spring bean으로 등록한다.

```java
@Configuration
@ComponentScan
public class AutoAppConfig {}
```

- 그리고 bean으로 등록하고 싶은 구체 클래스에 `@Component`를 붙인다.
- 그리고 `@Autowired`가 붙은 메소드를 자동으로 의존성을 주입한다.

```java
@Component //자동으로 spring bean등록
public class OrderServiceImpl implements OrderService {
    private final MemberRepository repository;
    private final DiscountPolicy discountPolicy;

    @Autowired //자동으로 의존성 주입
    public OrderServiceImpl(MemberRepository repository, DiscountPolicy discountPolicy) {
        this.repository = repository;
    }

@Component  //자동으로 spring bean등록
public class MemberServiceImpl implements MemberService{
    private final MemberRepository memberRepository;

    @Autowired //자동으로 의존성 주입
    public MemberServiceImpl(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }
}

@Component //자동으로 spring bean등록
public class OrderServiceImpl implements OrderService {
}
```

## ✅ Component Scan 범위 지정하기

- place `config file` in root of project file
- `basePackages`: search below this package
- `excludeFilters`: do not add this class as bean

```java
@Configuration
@ComponentScan(
        basePackages = "com.example.spring_basic",
        excludeFilters = @ComponentScan.Filter(type = FilterType.ANNOTATION, classes = Configuration.class )
)
public class AutoAppConfig { }
```

## ✅ Filter

- filter what/what not to include in component scan
- `includeFilters`
- `excludeFilters`

```java
@Configuration
@ComponentScan(
        includeFilters =  @ComponentScan.Filter(type = FilterType.ANNOTATION, classes = MyIncludeComponent.class),
        excludeFilters =  @ComponentScan.Filter(type = FilterType.ANNOTATION, classes = MyExcludeComponent.class))
static class ComponentFilterAppConfig{
    }
```

## ❓ Bean duplication, bean collision

- ❓ **What happens if bean names are identical?**
- 컴포넌트 스캔에 의해 자동으로 스프링 빈이 등록되는데, 그 이름이 같은 경우 스프링은 오류 발생 시킴
- 🔴 `ConflictingBeanDefinitionException` 예외 발생

- ❓ **What happens if bean is added both manually and auto with component scan?**
- There are two ways of adding bean
- 1️⃣ manual bean configuration with `@Configuration`
- 2️⃣ component scan with `@ComponentScan`
- 두 방법 모두으로 같은 bean이 두 번 등록된다면?

- 1️⃣ manual bean configuration **has priority**
- `manual bean` **overrides** `component scan`
- 🔴 그러나 권장하는 방법이 아니며, Springboot는 최근에 오류를 발생시키도록 바뀜

## ✅

## ✅

## ✅

## ✅

## ✅
