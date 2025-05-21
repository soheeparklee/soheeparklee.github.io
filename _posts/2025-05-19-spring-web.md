---
title: Developing Web
categories: [JAVA, 김영한]
tags: [mvc, api] # TAG names should always be lowercase
---

# ☑️ Spring

- Spring: allows to create web with `OOP`

# ☑️ Spring-boot-starter-web

- `gradle`: build 자동화, 의존성 관리
- `tomcat`: localhost 8080에 올리게 도와주는 `웹서버`
- `spring-webmvc`
- `thymeleaf`: html에 view를 도와주는 library
- `spring-boot-starter-logging`: 로그를 남기기 위해 사용되는 library, `logback`, `slf4j`

![Image](https://github.com/user-attachments/assets/677e5939-bbea-488b-a317-4af7255ce88a)

<img width="512" alt="Image" src="https://github.com/user-attachments/assets/89f7c2ef-7aec-480b-b88d-37f7808a1e66" />

# ☑️ Test library

- `junit`, `mockito`, `assertj`, `spring-test`: test code를 위해 필요한 library

# ✅ 정적 컨텐츠

- 그냥 정적인 HTML 파일을 웹브라우저에 전달, 화면에 띄워주는 기능
- `/static` 안에 HTML넣기
- `/static` 파일 안에 hello.html 넣은 후 `[localhost:8080/hello.html]`하면 정적 페이지가 뜬다.
- ➡️ 가공되지 않은 파일 그대로 반환

# ✅ MVC 템플릿 엔진

> **MVC** = model, view, controller

- model: data structure, `user cart data`
- view: UI, `user clicks add to cart button`
- controller: 백엔드 뒷단 코드 `update user cart ++`
- 👍🏻 역할(관심사)을 분리하여 코드의 유지보수성을 높인다

- view: 화면을 보여주기
- view를 찾아 template engine을 사용해 **화면을 렌더링**해서 html을 웹 브라우져에 넘겨주기
- viewResolver가 존재한다
- HTML + template engine(`THYMELEAF`)
- get parameter and show it on HTML, thus more interaction
- example of template engine is `THYMELEAF`
- ➡️ 가공된/처리된 HTML반환

# ✅ API

- view 없음
- 내가 입력한 문자가 그대로 내려간다.
- `repsonse body`: HTTP의 body에 이 내용을 직접 넣어주겠다.
- ➡️ 데이터 반환

# ✅ API 객체변환

- API는 view가 없으니까 viewResolver ❌
- 기본 문자처리: viewResolver 대신에 HTTP Message Converter ⭕️
- 객체처리: Mapping Jackson 2
- 객체`json`으로 처리하는 converter 다양한데 spring에서는 jackson 사용

`{key: value}`

> JSON= javascript object notation

- 임시데이터 전송에 좋음
- 많은 데이터를 반환 및 표시해야 하는 웹서비스의 경우 json이 효과적
- 👍🏻 클라이언트에게 구조화된 데이터만 전달
