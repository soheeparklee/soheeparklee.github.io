---
title: REST, API, MVC
categories: [WEB, WebBasics]
tags: [backend, requestbody, fastapi, path, query] # TAG names should always be lowercase
---

### **REST** <br>

`Representational State Transfer`

- 네트워크 아키텍쳐 스타일 중 하나
- 웹 서비스 간의 통신을 위한 구조적 졔약 조건
- RESTful 한 API

> ### **MVC** <br>

`Model / View / Controller`

- 소프트웨어 설계 패턴 중 하나
- 앱을 `모델`, `사용자 인터페이스`, `비즈니스 로직`으로 구분하여 개발

### **API**

> Application Protocol Interface

a way for two or more computer programs to communicate with each other  
application programming interface connects computers or pieces of software to each other  
FE와 BE가 통신을 하는 방법을 정해놓은 규약  
서비스의 요청과 응답에 대한 규칙  
이러한 요청과 응답을 처리하는 서비스(기능)

비유하자면, 한국에서 스페인으로 택배를 보낼 때 정해진 규칙이 있듯(우편주소, 보내는 방법), 컴퓨터끼리 또는 FE, BE끼리 통신할 때도 이런 규약이 있다.

**Interface**
tools and concepts of interaction between hardware and software components.

**User Interface**
user interface, which connects a computer to a person

### **비동기처리, Asynchronous processing**

프로그램이 여러 작업을 동시에 처리하도록 설계된 방식  
작업이 독립적으로 실행 => 이전 작업 안 끝나도 다른 작업 시작 가능  
병렬적으로 운영(Non-blocking)  
프로그램의 효율성⬆️

예를 들어,  
파일을 업로드하는데 동기 방식이면, 지금 파일이 업로드 완료된 후에야 다른 작업 가능(blocking, 작업 중단)
비동기 방식이면 파일 업로드가 진행되는 동안에도 사용자가 애플리케이션의 다른 부분 사용 가능

A synchronous process is a process that can be executed without interruption from start to finish.  
An asynchronous process is a process that the Workflow Engine cannot complete immediately because it contains activities that interrupt the flow.

**구현 방법**
자바스크립트와 같은 프로그래밍 언어에서 콜백 함수, 프로미스(Promise), async/await와 같은 기능을 통해 구현

- DOM event handler
- Timer function(setTimeout, setInterval)
- Ajax

### **REST API**

> Representational State Transfer API

API 작동 방식에 대한 조건을 부과하는 소프트웨어 아키텍처  
웹 상에서 자원을 표현하고 상호작용하는 데 사용되는 인터페이스 설계 원칙  
딱 봐도 "아 이런 작업을 하는 API구나!" 알 수 있게 API를 짜야 한다는 의미  
REST API는 HTTP 요청을 통해 통신함으로써 리소스 내에서 레코드(CRUD 라고도 함)의 작성, 읽기, 업데이트 및 삭제 등의 표준 데이터베이스 기능을 수행

- resourse(균일한 인터페이스)
  서버가 표준 형식으로 정보를 전송  
  각 자원을 고유한 URI(Uniform Resource Identifier)로 표현
  - URI(Uniform Resource Identifier): 고유한 리소스 식별자로, 각 리소스 식별(웹페이지를 방문하기 위해 브라우저에 입력하는 웹 사이트 주소와 유사)
    요청이 어디에서 오는지와 무관하게, 동일한 리소스에 대한 모든 API 요청은 동일
- stateless(무상태, 상태 없음)
  각 요청이 서버의 이전 상태를 참조하지 않고 독립적으로 처리된다  
  서버가 이전의 모든 요청과 독립적으로 모든 클라이언트 요청을 완료하는 통신 방법  
  이로 인해 서버와 클라이언트 간의 의존성이 낮아지고, 확장성과 유지 보수가 용이
- cacheable(캐시 가능)
  캐시 기능을 이용하여 응답 결과를 저장해두고 재사용 가능  
  서버 부하 ⬇️  
  응답 속도 ⬆️ 성능 향상
- client-server decoupling  
  클라이언트와 서버 분리 따라서 각각의 역할 명확  
  각각 독립적으로 발전, 유연한 시스템 구축
  - 클라이언트 애플리케이션이 알아야 하는 유일한 정보는 요청된 리소스의 URI
  - 서버 애플리케이션은 HTTP를 통해 요청된 데이터에 전달하는 것 말고는 클라이언트 애플리케이션을 수정하지 않아야
- layered System(게층화 구조)
  여러 계층으로 구성 가능  
  각 계층은 독립적으로 기능 수행
- method(표준화된 메소드)
  일반적으로 HTTP 메소드를 이용해 자원에 대한 조작을 수행  
  사용되는 메소드로는 GET, POST, PUT, DELETE 등
