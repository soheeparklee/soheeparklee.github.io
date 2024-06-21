---
title: WEB API, HTTP.STATUS.VALUE
categories: [Computer Science, WEB]
tags: [web, api]
---

## ⭐️ 핵심 개념

- WEB API

## URN 🆚 URI 🆚 URL

💡 URN

> Uniform Resource Name

<br>
프로토콜, 리소스 위치, 호스트 등과는 상관 없이 각 자원의 이름 <br>
웹 문서의 물리적인 위치랑 상관 없이 웹 문서 그 자체<br>

💡 URI

> Uniform Resouce Identifier <br>

 <br>

리소스의 이름(식별자)
예시: `www.google.com`

💡 URL

> Uniform Resource Locator <br>
> protocol + URI <br>

 <br>
 
특정 서버에 있는 문서  <br>
리소스의 이름 + 위치(어떻게 도달할 수 있는지)  <br>
즉, protocol이 리소스에 어떻게 도달할 수 있는지 알려줌  <br>
예시: `https://www.google.com` <br>

<img width="514" alt="image" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/1408de60-40e7-4ca5-9d49-9a1b6b007680">

## ✅ WEBAPI

- URI는 정보의 자원을 표현해야 한다.
- 자원에 대한 행위는 HTTP Method로 표현한다.

## ✅ HTTP Method

- POST
- GET
- PUT
- DELETE

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

## ✅ HTTP STATUS

<https://m.boostcourse.org/web316/lecture/16741>
