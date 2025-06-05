---
title: Bean Life cycle callback
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ Bean Life cycle

> steps Spring goes through to manage a bean: from **creation** to **destruction**

- 객체 생성 먼저 ➡️ 이후 의존관계 주입(setter)
- constructor로 DI할 때는 객체 생성할 때 의존관계 주입

- ✔️ **Bean Life cycle**
- 스프링 컨테이너 생성
- ➡️ 스프링 빈 생성
- ➡️ 의존관계 주입
- ➡️ 초기화 콜백(의존관계 주입 끝났어 알려주기)
- ➡️ 사용
- ➡️ 소멸 전 콜백(소멸되기 직전에 알려주기)
- ➡️ 스프링 종료

## ✅ 빈 생명주기 콜백 방법

- 초기화 콜백(의존관계 주입 끝났어 알려주기)
- 소멸 전 콜백(소멸되기 직전에 알려주기)
- 어떻게 알려줄까?

### 💡 add annotation

- 👍🏻 recommended method
- add annotation `@PostConstruct` and `@PreDestroy`

- `@PostConstruct`: code runs after bean is created and dependencies are set
- `@PreDestroy`: code that runs before bean is destroyed(only for singleton)

```java
public class NetworkClient {
    @PostConstruct
    public void init() { //의존관계 주입이 끝나면 호출
        System.out.println("afterPropertiesSet ");
        connect();
        call("initialization mesage");
    }


    @PreDestroy //빈 소멸 전 이 메소드 호출
    public void close()  {
        System.out.println("destroy");
        disconnect();
    }
}
```

### 💡 add method to bean

- create init, close method
- and add the method to bean

```java
public class NetworkClient {
    public void init() { //의존관계 주입이 끝나면 호출
        System.out.println("afterPropertiesSet ");
        connect();
        call("initialization mesage");
    }


    public void close()  { //빈 소멸 전 이 메소드 호출
        System.out.println("destroy");
        disconnect();
    }
}
```

- add to spring bean

```java
@Configuration
static class LifeCycleConfig{
    @Bean(initMethod = "init", destroyMethod = "close")
    public NetworkClient networkClient(){
        NetworkClient networkClient = new NetworkClient();
        networkClient.setUrl("http://hello.com");
        return networkClient;
    }
}
```

### 💡 implement InitializingBean, DisposableBean

- ⚠️ old method, not used frequently
- `InitializingBean, DisposableBean`을 implement하면
- 두 가지 메소드를 override

```java
public class NetworkClient implements InitializingBean, DisposableBean {

    @Override
    public void afterPropertiesSet() throws Exception { //의존관계 주입이 끝나면 이 메소드 호출
        System.out.println("afterPropertiesSet ");
        connect();
        call("initialization mesage");
    }

    @Override
    public void destroy() throws Exception { //빈 소멸 전 이 메소드 호출
        System.out.println("destroy");
        disconnect();
    }
}
```
