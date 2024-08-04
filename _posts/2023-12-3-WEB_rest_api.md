---
title: REST, API, MVC
categories: [Computer Science, WEB]
tags: [backend, requestbody, fastapi, path, query, api] # TAG names should always be lowercase
---

## ✅ **MVC**

`Model / View / Controller`

- 소프트웨어 설계 패턴 중 하나
- 앱을 `모델`, `사용자 인터페이스`, `비즈니스 로직`으로 구분하여 개발

## ✅ **API**

> Application Programming Interface <br>
> An **Interface** needed for **Programming** an **Application** <br>
> rules and protocols that allow one software application to interact with another <br>

운영 체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스 <br>
예시: 자바 언어가 제공하는 클래스, 인터페이스, 패키지(java.util, java.io) 등 <br>

a way for two or more computer programs to communicate with each other <br>
application programming interface connects computers or pieces of software to each other <br>
FE와 BE가 통신을 하는 방법을 정해놓은 규약 <br>
서비스의 요청과 응답에 대한 규칙 <br>
이러한 요청과 응답을 처리하는 서비스(기능) <br>
<br>

비유하자면, 한국에서 스페인으로 택배를 보낼 때 정해진 규칙이 있듯(우편주소, 보내는 방법), 컴퓨터끼리 또는 FE, BE끼리 통신할 때도 이런 규약이 있다. <br>

#### examples of APIs

- ArrayList <br>
- input/output <br>
- JDBCs <br>

## ✅ Interface

> a common set of methods that can be implemented by multiple classes <br>
> enables ⭐️ **polymorphism** and ⭐️ **abstraction** <br>
> tools and concepts of interaction between hardware and software components. <br> > <br>

💡 **User Interface** <br>
user interface, which connects a computer to a person <br>

## API 🆚 Interface

- an API can include interfaces <br>
  -Interfaces are a way to achieve abstraction and define contracts. <br>
- APIs, on the other hand, encompass rules and protocols for application interaction. <br>

## ✅ **REST**

<img width="442" alt="Screenshot 2024-08-03 at 10 40 49" src="https://github.com/user-attachments/assets/ce17eee4-75dc-4a19-8a05-030eed9d166e">

> Representational State Transfer <br>

- 네트워크 아키텍쳐 스타일 중 하나 <br>
- 웹 서비스 간의 통신을 위한 구조적 졔약 조건<br>
- RESTful 한 API<br>

## ✅ **REST API**

> Representational State Transfer API
> HTTP프로토콜로 제공하는 API<br>
> 따라서 핵심 컨텐츠 및 기능을 외부 사이트(핸드폰, 웹, 크롬, 사파리 등)에서 활용할 수 있도록 제공되는 인터페이스 <br>
> REST APIs are widely used for building web services that allow different software applications to communicate over the internet <br>

API 작동 방식에 대한 조건을 부과하는 소프트웨어 아키텍처 <br>
웹 상에서 자원을 표현하고 상호작용하는 데 사용되는 인터페이스 설계 원칙 <br>
딱 봐도 "아 이런 작업을 하는 API구나!" 알 수 있게 API를 짜야 한다는 의미 <br>
REST API는 HTTP 요청을 통해 통신함으로써 리소스 내에서 레코드(CRUD 라고도 함)의 작성, 읽기, 업데이트 및 삭제 등의 표준 데이터베이스 기능을 수행 <br>

### ✔️ RestAPI 특징

- **Uniform Interface** <br>
  - 서버가 표준 형식으로 정보를 전송, 그래서 어떤 기술도 가능한 interface <br>
  - 각 자원을 고유한 URI(Uniform Resource Identifier)로 표현 <br>
  - URI(Uniform Resource Identifier): 고유한 리소스 식별자로, 각 리소스 식별(웹페이지를 방문하기 위해 브라우저에 입력하는 웹 사이트 주소와 유사) <br>
  - 요청이 어디에서 오는지와 무관하게, 동일한 리소스에 대한 모든 API 요청은 동일 <br>
- **stateless(무상태, 상태 없음)** <br>
  - 각 요청이 서버의 이전 상태를 참조하지 않고 독립적으로 처리된다 <br>
  - 서버가 이전의 모든 요청과 독립적으로 모든 클라이언트 요청을 완료하는 통신 방법 <br>
  - 이로 인해 서버와 클라이언트 간의 의존성이 낮아지고, 확장성과 유지 보수가 용이 <br>
- **cacheable(캐시 가능)** <br>
  - 캐시 기능을 이용하여 응답 결과를 저장해두고 재사용 가능 <br>
  - 서버 부하 ⬇️ <br>
  - 응답 속도 ⬆️ 성능 향상 <br>
- **client-server decoupling** <br>
  - 클라이언트와 서버 분리 따라서 각각의 역할 명확 <br>
  - 각각 독립적으로 발전, 유연한 시스템 구축 <br>
    - 클라이언트 애플리케이션이 알아야 하는 유일한 정보는 요청된 리소스의 URI <br>
    - 서버 애플리케이션은 HTTP를 통해 요청된 데이터에 전달하는 것 말고는 클라이언트 애플리케이션을 수정하지 않아야 <br>
- **layered System(게층화 구조)** <br>
  여러 계층으로 구성 가능 <br>
  각 계층은 독립적으로 기능 수행 <br>
- **method(표준화된 메소드)** <br>
  일반적으로 HTTP 메소드를 이용해 자원에 대한 조작을 수행 <br>
  사용되는 메소드로는 GET, POST, PUT, DELETE 등 <br>

### ✔️ RestAPI가 지켜야 하는 스타일

- client-server
- stateless
- cache
- uniform interface
- layered system
- code-on-demand(optinal)

### ✔️ 지키기 어려운 uniform interface

- 리소스가 URI로 식별되어야 한다.
- 리소스를 생성, 수정, 추가하고자 할 때 HTTP에 표현을 해서 전송해야 한다.
- 메세지는 스스로를 설명할 수 있어야 한다. self-descriptive message
- 애플리케이션의 상태는 hyperlink를 통해 전송되어야 한다. HATEOAS

여기서 self-descriptive message 부분과 HATEOAS는 API로 구현하기가 쉽지 않다. <br>
그래서 WEB API 또는 HTTP API를 사용하기도 한다. <br>
그래서 Rest라고 하면서 Rest의 모든 것을 지키지 않거나, WEB API 또는 HTTP API를를 Rest라고 부르기도 한다. <br>

## ✅ MashUp

> 서비스 업체들이 다양한 RestAPI를 제공함으로써, 이러한 RestAPI를 조합해 만든 어플리케이션 <br>
