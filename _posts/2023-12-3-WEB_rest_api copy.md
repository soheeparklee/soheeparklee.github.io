---
title: REST, API, MVC
categories: [Computer Science, WEB]
tags: [backend, requestbody, fastapi, path, query, api] # TAG names should always be lowercase
---

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

## ✅ Restful WEBAPI

- URI는 정보의 자원을 표현해야 한다.
- 자원에 대한 행위는 HTTP Method로 표현한다.

## ⭕️❌ 문제

| HTTP Method           | ⭕️❌                      |
| --------------------- | -------------------------- |
| GET /members/1        | ⭕️                        |
| GET /members/get/1    | ❌ 동사로 표현하면 안된다. |
| GET /members/add      | ❌                         |
| POST /members         | ⭕️                        |
| GET /members/update/1 | ❌                         |
| PUT /members/1        | ⭕️                        |
| GET /members/del/1    | ❌                         |
| DELETE /members/1     | ⭕️                        |

## ✅ 그 외 규칙

- 슬래시 `/`는 계층을 나타낼 때 사용
- URI는 마지막 문자로 `/`를 포함하지 않는다.
- 하이픈`-`은 가독성을 높일 때 사용한다.
- 언더바`_`는 사용하지 않는다.
- URI 경로로는 소문자만 사용한다.

## ✅ MashUp

> 서비스 업체들이 다양한 RestAPI를 제공함으로써, 이러한 RestAPI를 조합해 만든 어플리케이션 <br>
