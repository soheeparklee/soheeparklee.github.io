---
title: Developing Web
categories: [Backend, 김영한JavaSpring입문]
tags: [backend, spring, 김영한, java] # TAG names should always be lowercase
---

# 정적 컨텐츠

- 그냥 HTML띄워주는 기능
- /static 안에 HTML넣기
- hello.html 넣은 후 [localhost:8080/hello.html](http://localhost:8080/hello.html) 하면 페이지 뜬다.

# MVC 템플릿 엔진

**MVC= model, view, controller**

- view를 찾아 template engine을 사용해 화면을 렌더링해서 html을 웹 브라우져에 넘겨주기
- viewResolver
- HTML + template engine
- get parameter and show it on HTML, thus more interaction
- example of template engine is THYMELEAF

# API

- view 없음
- 내가 입력한 문자가 그대로 내려간다.
- repsonse body: HTTP의 body에 이 내용을 직접 넣어주겠다.

## API 객체변환

- API는 view가 없으니까 viewResolver ❌
- HTTP Message Converter ⭕️
- 객체처리할 때는 Mapping JAckson 2
- 객체json으로 처리하는 converter 다양한데 spring에서는 jackson 사용

`{key: value}`

> JSON= javascript object notation

- 임시데이터 전송에 좋음
- 많은 데이터를 반환 및 표시해야 하는 웹서비스의 경우 json이 효과적
