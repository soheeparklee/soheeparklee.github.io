---
title: Bean Scope
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ Scope

> **how many instances of a bean** Spring should create <br>
> and **how long** they should live

- 빈이 존재부터 언제까지 존재하는지 `존재할 수 있는 범위`
- ✔️ **singleton**: default. One instance per Spring container.
- ✔️ **prototype**: new instance every time it is requested. bean exists until spring container creates beans, inject dependency, then expires
- web
  - ✔️ **request**: one instance per HTTP request
  - ✔️ **session**: one instance per HTTP session
  - ✔️ **application**: one instance per ServletContext
  - ✔️ **web socket**

## 💡 Singleton scope

- one single bean
- always return the **same** instance bean
- bean exists from when spring container is created until the end
- longest bean scope

## 💡 Prototype scope

- create new bean instance when it is requested
- always return **new** instance bean when requested
- 🆚 singleton: always return same instance bean when requested
- Spring container **does not manage** created beans, does not call `@PreDestroy`
- client must manage the prototype beans, 직접 bean 종료해주어야 한다
- 요청이 오면 ➡️ bean 생성, DI ➡️ 사용 ➡️ 끝나면 삭제 ➡️ 관리 안 함 ➡️ 또 요청오면 새로 생성

```java
@Component
@Scope("prototype")
public class MyBean {
    public MyBean() {
        System.out.println("MyBean created");
    }
}
```

## ✅ ObjectFactory, ObjectProvider, Provider

- 지정한 bean을 container에서 대신 찾아주는 기능 제공
- singleton안에서 prototype빈을 만들면 같은 bean을 계속 참조함
- 우리가 원하는 prototype빈은 매번 새롭게 생성되길 원함
- ObjectProvider을 사용하면 prototype빈 request할 때마다 새로 만들게 하기

## 💡 Web scope

- ✔️ **request**: one instance per HTTP request
- ✔️ **session**: one instance per HTTP session
- ✔️ **application**: one instance per ServletContext
- ✔️ **web socket**

```java
@Component
@Scope(value = "request", proxyMode = ScopedProxyMode.TARGET_CLASS)
public class MyLogger {
}
```

- `request scope`일 때 처음 application을 실행하면, 당연히 request가 아직 없으니 `MyLogger bean`이 생성되지 않음
- 그래서 DI에 오류 발생
- 💊 `proxyMode = ScopedProxyMode.TARGET_CLASS`를 붙여줌
- 그러면 스프링 컨테이너는 `CGLIB`라는 라이브러리 사용
- `MyLogger`을 상속받은 `가짜 proxy 객체`를 생성
- 아직 request는 없지만, `가짜 proxy 객체`로 DI가 가능해진다.

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅
