---
title: HTTP
categories: [Computer Science, Network]
tags: [cs, network, supercoding] # TAG names should always be lowercase
---

## ✅ URL과 도메인

### URL

URL: Uniform Rerource Location <br>
**http:** 이 안에 프로토콜 저장<br>
**도메인:** IP주소는 너무 복잡하니까 읽기 쉬운 별칭으로 주소 지칭<br>
**DNS:** Domain Name System 서버<br>
DNS에서 도메인 보고 IP서버 받아와 정확한 장소로 연결<br>

## ✅ HTTP

**HTTP:** Hypertext Transfer Protocol <br>
브라우저 <-> 웹 서버 데이터 교환 프로토콜, 웹 페이지 요청/응답 처리 <br>
**HTTPS** 🟰 HTTP ➕ SSL <br>
**SSL:** 통신 암호화 <br>

- 서버 - 클라이언트 구조
- stateless(이전 요청을 기억하지 못한다. 항상 처음보는 연결처럼 대한다.)
- 데이터 유실률이 낮다(HTTP는 TCP전송의 한 종류이므로 정확성이 높다.)
- connectionless 지향(비연결성, 매번 새롭게 요청해야한다)
- 요청과 응답 메세지 가독성이 좋아 개발자가 알아보기가 쉽다.

## ✅ HTTP 요청, 응답 구조

### ☑️ HTTP 요청 message와 HTTP method

#### ✔️ HTTP 요청 message

method ➕ URI ➕ http version<br>
<br>
※ URL은 URI의 일종이다<br>

#### ✔️ HTTP method

- GET
- PUT
- POST
- DELETE

#### ✔️ 주요 Header

- Host: 요청하는 서버 주소 & 포트 domain, port, IP address
- Accept: 원하는 데이터 형식
- Connetion: 커넥션 유지 여부(연결성을 유지할 것인가? 선택할 수 있음)
- Content-type: 요청 데이터 포맷

#### ✔️ 응답 Message

- 응답 코드, 응답 메세지: 숫자에 따라 결과 보여줌
- Body: 응답 데이터
- Content-type: 응답 데이터 포맷

## ✅ XML, JSON

프런트엔드와 백엔드가 소통하기 위하여 통일된 데이터 포맷이 필요함<br>
언어와 독립적인 포맷<br>

- WEB page 포맷
  - HTML
  - CSS
  - JS
- media 포맷
  - JPEG
  - ZIP
- data 직렬화 포맷
  - XML
  - JSON

## ✅ WEB API 아키텍쳐 스타일

**WEB API:** 웹의 두 어플리케이션을 이어주는 다리<br>
<br>

**API 아키텍쳐 스타일:** HTTP를 사용하는 여러 가지 방법<br>

- GraahQL API: 요청할 때 POST
- REST API: 요청할 때 GET
  이런식으로 서로 방법이 다르지만 결국 WEB에서 정보 가져오는 기능

## ✅ REST

**REpresentational State Transfer**<br>
resouce를 요청하거나 업로드할 때 특정 방식(method)으로 표현해야 한다. <br>

- 자원: URI
- 방식: HTTP method(Get, Post, Put, Patch, Delete)
- 표현: JSON/ XML

### ☑️ REST API/ RESTful API

REST 철학을 최대한 활용한 API <br>

- URI는 정보의 자원을 표현해야 한다. <br>
- 자원에 대한 헹위는 HTTP method로 표현해야 한다. <br>
  RESTful API: REST 철학을 최대한 수용한^^ API <br>
