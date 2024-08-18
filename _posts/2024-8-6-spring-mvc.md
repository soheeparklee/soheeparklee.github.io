---
title: MVC, MVC Design Pattern
categories: [JAVA, Spring]
tags: [] # TAG names should always be lowercase
---

## ✅ MVC Design Pattern

<img width="639" alt="Screenshot 2024-08-10 at 12 57 00" src="https://github.com/user-attachments/assets/9b6fd781-10f8-42dd-9b74-6e7e012e403e">

#### ✔️ Model

- business logic
- database
- respond to request for information from other components

#### ✔️ View

- Display data from Model to user
- output of request
- send user input to Controller

#### ✔️ Controller

- intermediary between Model and View
- application logic: input validation, data transformation

💡 <https://www.geeksforgeeks.org/mvc-design-pattern/> <br>

## MVC 1 🆚 MVC 2

#### ✔️ JSP

> Jakarta Server Pages <br>
> HTML code + Java code and create dynamic web page <br>

#### ✔️ MVC 1

<img width="621" alt="Screenshot 2024-08-10 at 13 07 22" src="https://github.com/user-attachments/assets/5db7fee8-9a39-4adf-b306-99d57155afdd">

- JSP manages **both** `View` and `Controller`
- inside JSP, both `HTML` and `Java` code are used
  👍🏻 easy implementation <br>
  👎🏻 when app starts getting bigger, reduce reusability and code readability <br>

#### ✔️ MVC 2 ➡️ Spring

<img width="629" alt="Screenshot 2024-08-10 at 13 08 44" src="https://github.com/user-attachments/assets/376b869e-5e18-4de2-97ea-9a423f066ff6">

- request sent to `Controller(Servlet)`
- `Controller` and `View` is **seperate**
  - JSP: only manage `View`
  - Servelt: manage `controller`
- can debug only the necessary component
- Spring Framework

## ✅ What happens in MVC when client request server through url?

<img width="502" alt="Screenshot 2024-08-06 at 11 36 50" src="https://github.com/user-attachments/assets/19bae240-3340-4495-a8ae-7fd211e46592">

<img width="634" alt="Screenshot 2024-08-10 at 13 17 31" src="https://github.com/user-attachments/assets/8c5dd835-c8e2-4914-be65-32039b0f3616">

1. When client requests url, web browser sends request to `spring` <br>
2. `Dispatcher Servlet` recieves this request, ask `Handler Mapping` to find `controller` that controls that url. <br>
3. Send request to `Controller`, and set `Model` that is required to send. <br>
4. `Model` accesses `database` to fetch data for page with query. <br>
5. `Controller` responds with `Model information`. `Controller` completes `Model` and sends to `Dispatcher Servlet`. `Controller` also tells `Dispatcher Servlet` what `view` has to be rendered. <br>
6. `Dispatcher Servlet` recieves view file from `View resolver` that matches the request <br>
7. Send `Model` to `view page` file and complete the page to send to client <br>
8. Response `view file` to client <br>

## ✔️ Dispatcher Servlet

- manage all request from HTTP protocol
- considered to be front controller
- centralized management of all requests through servelt container with http

## ✔️ Handler Mapping

- finds which `controller` should manage the `request url`, send it to `dispatcher servlet`
- for controller to `map` url, uses `@RequestMapping`
- the handler finds this url for `dispatcher servlet`

## ✔️ Controller

- backend controller for managing request
- return `model` result to `dispatcher servlet`

## ✔️ View Resolver

- decides `view` of controller result

## ✅ Filter

> java class that is executed by Servlet container
> check each incoming HTTP request and HTTP response

- associated with Servlet API

## ✅ HandlerIntercepter

- unique to spring
- operate after filter
- appropriate for pre-processing duties
  - authorization checks

### Filter 🆚 HandlerIntercepter

- filter 🆚 handler interceptor: difference in **when** it is operated
- but both **before** request going into controller
- both operate in **Dispatcher Servlet**
