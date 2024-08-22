---
title: URN/URI/URL
categories: [Computer Science, WEB]
tags: [web, api]
---

![Screenshot 2024-08-21 at 22 08 22](https://github.com/user-attachments/assets/d4642b8d-bd89-4dc7-bb75-52ede7d4323c)

> What is this? URL or URI? `https://www.google.com` <br>
>
> > answer: both <br>
> > but being precise, URL. <br>

## 📌 **URI**

> Uniform Resouce Identifier <br>

 <br>

- 리소스의 이름(식별자)
- 예시: `www.google.com`
- URI ⊃ URL, URN

## 📌 **URN**

> Uniform Resource Name

- 인터넷 상에서 자원을 가리키는 **식별자**
- 프로토콜, 리소스 위치, 호스트 등과는 상관 없이 각 자원의 이름 <br>
- 웹 문서의 물리적인 위치랑 상관 없이 웹 문서 그 자체<br>

- URN looks like this
  - urn:isbn:9788898392389
  - starts with `urn`
  - `isbn`: International Standard Book Numbers

## 📌 **URL**

> Uniform Resource **Locator** <br>
> protocol + URI <br>

- 인터넷 상에서 특정 시점 자원의 **위치**
- 특정 서버에 있는 문서 <br>
- 리소스의 이름 + 위치(어떻게 도달할 수 있는지) <br>
- 즉, protocol이 리소스에 어떻게 도달할 수 있는지 알려줌
- 예시: `https://www.google.com`

<img width="514" alt="image" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/1408de60-40e7-4ca5-9d49-9a1b6b007680">

## 💡 What happens if the location of a resource changes? What happens to URL?

- URL indicates location of a resource at a certain time
- What happens if the location changes?
- Then, with the old URL, we cannot identify the resource

> What are the disadvantages of URL, and how can we overcome? <br>
>
> > URL can change if the location of the resource changes. <br>
> > In order to be able to identify the resource no matter the location, <br>
> > we can use URN. <br>

- In order to identity resource regardless of location, use URN.
- URN gives a unique identifier forever to the resource
- Even if location of resource changes, can access resource if we know the URN

- URN looks like this `urn:isbn:9788898392389`
