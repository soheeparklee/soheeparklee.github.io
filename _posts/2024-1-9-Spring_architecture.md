---
title: Spring boot architecture, layers, DTO
categories: [JAVA, Spring]
tags: [web, service, repository, dto] # TAG names should always be lowercase
---

## ✅ Spring files

스프링부트에서는 스프링을 실행하는게 아니라 ❌ <br>
내장 톰캣서버를 실행하는 것이다. 🐈‍ <br>

![코딩공책-21](https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/b3629aa0-6f71-4e61-86b7-09a25d013431)

#### ✔️ yaml file

> application 설정을 도와주는 파일<br>

이제는 application.properties 파일 형식 아니고❌<br>
application.yaml을 사용할 것임⭕️<br>

👍🏻 .yaml 형식 장점
가독성, profile 사용하기 용이
![코딩공책-20](https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/8479e7fe-50ee-45d4-b037-02977432f6b0)

## ✅ Profile 설정

#### ✔️ 대표 개발 단계

개발 단계에 따라 profile을 분리해 관리할 필요가 있다. <br>
1️⃣ local: 개발자가 개발하고 있는 단계 <br>
2️⃣ dev: 여러 개발자들이 개발한 것을 합치고 있는 단계 <br>
3️⃣ prod: 사용자에게 제공되고 있는 서비스 <br>

그리고 이 개발 단계에 따라 profile을 분리하는데,
profile 별로 application.yaml 따로 구성해서 관리한다
![코딩공책-22](https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/768aa64c-2e00-451d-8c57-e6804a694916)

## ✅ Code architecture

> 코드 아키텍쳐: 소프트웨어의 구조/구성을 조직적으로 정리하는 것 <br>
> 코드를 효율적으로 관리하기 위함 <br>

#### ✔️ Code architecture 종류

- Clean architecture <br>
- Domain driven Development <br>
- 3 layer architecture <br>

## ✅ Spring code architecture: 3-layered 🟰 3 tier

> 3-layered: 전체를 3가지 논리적 계층으로 구성하고, 각 계층이 자신의 역할/책임을 가지는 구조 <br>
> 각 접점을 하나의 계층으로 빼고, 각 계층이 자기 역할을 한다. <br>

👍🏻 외부에서 수정 요청이 들어오면 그 계층만 수정하면 되니까<br>
👍🏻 괜히 코드 수정하다가 다른 부분은 건드리지 않도록<br>

<img width="790" alt="스크린샷 2024-01-09 오후 7 26 14" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/aa5f1517-4118-475a-972f-b07f61d18921">

### ✔️ Web layer(🟰Presentation Layer)

> 외부(client/dispatcher servlet)과 맞닿아 있는 레이어<br>

외부 요청/응답의 접점에 위치한다.<br>

### ✔️ Service layer

> 비즈니스 로직을 실제로 처리함<br>

### ✔️ Repository layer(🟰Data Access Layer)

> 데이터 베이스와 상호작용하는 레이어<br>

<img width="447" alt="스크린샷 2024-01-09 오후 7 34 35" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/c8d3ce15-bd41-42e8-853f-0ea848e96e71">

config는 web, service, respository 어디에도 속하지 않는 파일 넣으려고 만들었음<br>

## ⭐️ SpringBoot 직렬화: Jackson 라이브러리

> Jackson 라이브러리: DTO ↔️ JSON 직렬화/역직렬화 하는 라이브러리 <br>

Jackson이 getter을 사용해서 DTO를 JSON으로, JSON을 DTO로 바꿔준다. <br>
