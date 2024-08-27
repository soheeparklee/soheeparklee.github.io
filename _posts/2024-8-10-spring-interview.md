---
title: Interview_Spring/Springboot/MVC/AOP
categories: [JAVA, Spring]
tags: [interview] # TAG names should always be lowercase
---

## ✅ What is Spring?

- open source application framework for JAVA
- Java platform that provides comprehensive infrastructure support for developing Java applications
- can build applcations from POJOs
- uses AOP, DI

## Spring 🆚 Springboot

- Springboot: **sub project** to set up project in spring
- built on top of the conventional spring framework
- provides all features of spring + easier to use than spring
- everything is auto configured!
- very useful to develop **REST API**
- used to develop microservies, fast
- run in independent container
- embedded tomcat run automatically

💡 <https://www.geeksforgeeks.org/difference-between-spring-and-spring-boot/> <br>

## ✅ MVC Design Pattern?

- useful pattern for code reuseability
- Model, View, Controller
  - Model: buisness logic, database
  - View: show users
  - Controller: connect `Model` and `View` to exchange data

💡 <https://soheeparklee.github.io/posts/spring-mvc/> <br>

## MVC 1 🆚 MVC 2

- MVC1: JSP manages both controller & view
  - JSP안에서 로직 처리를 위해 자바 코드 사용
- MVC2: controller and view seperate
  - create Servelt to divide work
  - `JSP` manage `View`, `Servlet` manage `Controller`

## Filter 🆚 Interceptor

- Filter: filter HTTP request, response in servlet container
- Interceptor: after filter, filter pre-processing duties

## ✅ Dispatcher Servelt?

- front controller that handles all HTTP requests

## ✅ AOP?

- define cross cutting concerns into seperate unit called **aspect**
- can modularize
- for logging, transaction, security

- advice: when
- join point: where
- point cut: where
- weaving: apply aspect to target code

💡 <https://soheeparklee.github.io/posts/Spring_3DI_IOC/> <br>
