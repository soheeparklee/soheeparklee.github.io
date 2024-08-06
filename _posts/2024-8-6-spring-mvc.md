---
title: MVC
categories: [JAVA, Spring]
tags: [] # TAG names should always be lowercase
---

## ✅ What happens in MVC when client request server through url?

<img width="502" alt="Screenshot 2024-08-06 at 11 36 50" src="https://github.com/user-attachments/assets/19bae240-3340-4495-a8ae-7fd211e46592">

1. When client requests url, web browser sends request to `spring` <br>
2. `Dispatcher Servlet` recieves this request, finds `controller` that controls that url with `Handler Mapping` <br>
3. Send request to `Controller`, and set `Model` that is required to send. <br>
4. `Model` accesses `database` to fetch data for page with query. <br>
5. Response `controller` with Model `information`, `Controller` completes `Model` and sends to `Dispatcher Servlet` <br>
6. `Dispatcher Servlet` recieves view file from `View resolver` that matches the request <br>
7. Send `Model` to `view page` file and complete the page to send to client <br>
8. Response `view file` to client <br>

## ✔️ Dispatcher Servlet

- manage all request
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
