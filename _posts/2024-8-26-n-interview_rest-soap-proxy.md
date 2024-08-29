---
title: Interview_
categories: [Computer Science, Network]
tags: [interview] # TAG names should always be lowercase
---

## 📌 SOP, CORS, XXS, CSRF, SQL injection, XML injection

<details>
<summary>✅ What is origin?</summary>
- protocol ➕ host ➕ port <br>
</details>

<br>

<details>
<summary>✅ What is SOP?</summary>
- Same Origin Policy <br>
- resource can be shared only between same server/same domain/same origin <br>
</details>

<br>

<details>
<summary>✅ What are the benefits of SOP?</summary>
- prevent from malicious attacks such as XXS, CSRF, SQL injection <br>
</details>

<br>

<details>
<summary>✅ What is XXS? And how can we prevent? </summary>
- Cross Site Scripting  <br>
- malicious scripts into web pages <br>
- steal data, impersonate the user, or manipulate the webpage's content <br>
- steal cookies, session tokens, credentials  <br>
<br>
💊 input validation <br>
💊 output encoding <br>
💊 CSP: content security policy <br>
💊 중요 cookie HTTP ONLY <br>

</details>

<br>

<details>
<summary>✅ What is CSRF? And how can we prevent? </summary>
- Cross Site Rquest Forgery <br>
- web-based attack 
- trick a user into performing an unwanted action on a website where they are already authenticated <br>
- transfer funds, change passwords, or perform other actions without the user’s consent. <br>
 <br>
💊 CSRF token <br>
💊 cookie `SameSite` only header <br>
💊 CAPTCHA <br>

</details>

<br>

<details>
<summary>✅ What is SQL injection? And how can we prevent? </summary>
- insert malicious SQL code <br>
- Use URL parameter, form fields, cookies, POST data, HTTP headers <br>
- like delete user <br>
 <br>
💊 input validation <br>
💊 sanitiza user data <br>
💊 WAF <br>

</details>

<br>

<details>
<summary>✅ What XML injection? And how can we prevent? </summary>
- insert malicious code to trusted site <br>
- XML bomb <br>
- XXE <br>
 <br>
💊 input validation <br>
💊 sanitiza user data <br>
💊 WAF <br>

</details>

<br>

<details>
<summary>✅ What is CORS?</summary>
- Cross Origin Resource Sharing <br>
- for frontend, backend to communicate <br>
</details>

<br>

<details>
<summary>✅ How can we prevent CORS error?</summary>

1. browser extension <br>

2. proxy server <br>

3. backend settings: add `Access-Control-Allow-Origin` to `HTTP response header` <br>
</details>

<br>

## 📌

<details>
<summary>✅ What is proxy?</summary>

- Proxy between client and server as intermediary<br>
- Proxy server will allow resource shared between different origin<br>
- solution to CORS error <br>

</details>

<br>

## 📌 REST, SOAP

<details>
<summary>✅ What is SOAP? When is it used? </summary>
- Simple Object Access Protocol <br>
- Protocol to exchange structured information <br>
- exchange XML messages <br>
 <br>
👍🏻 transaction, more secure <br>
👍🏻 ACID(Automicity, Consistency, Isolation, Durability) <br>
👎🏻 complex message <br>
👎🏻 so strict! more rules. <br>

</details>

<br>

<details>
<summary>✅ What is REST? </summary>
- Representational State Transfer <br>
- architectural structure to create APIs <br>
- state: HTTP Status code <br>
- HTTP URI, HTTP Method <br>
</details>

<br>

<details>
<summary>✅ What is a Restful API? What are the conditions? </summary>
- API that follows the REST architecture <br>
- HTTP CRUD 특징을 많이 가진다.  <br>
<br>
- client-server <br>
- statelessness <br>
- cache <br>
- layered system <br>
- uniform interface <br>
    - URI  <br>
    - self-descriptive message  <br>
    - HATEOAS  <br>
- code-on-demand(optional) <br>
</details>

<br>

<details>
<summary>✅ How is the maturity level of REST?</summary>
- URI <br>
- HTTP Methods <br>
- HATEOAS<br>

- L0: single URI, single verb<br>
- L1: multiple URIs, single verb<br>
- L2: multiple URIs, multiple verbs<br>
- L3: HATEOAS<br>
</details>

<br>

## URI 🆚 URN 🆚 URL

<details>
<summary>✅ Difference between URI, URN, URL? </summary>
- URI ⊃ URL, URN <br>
</details>

<br>

<details>
<summary>✅ Why do we need URN, when we have URL?</summary>
- location of the resource can change <br>
- URL can change <br>
- URN will remain fixed <br>
</details>

<br>

<details>
<summary>✅ </summary>
- <br>
</details>

<br>

<details>
<summary>✅ </summary>
- <br>
</details>

<br>

<details>
<summary>✅ </summary>
- <br>
</details>

<br>

## 📌 Web Cache

<details>
<summary>✅ </summary>

</details>

<br>

<details>
<summary>✅ </summary>

</details>

<br>

<details>
<summary>✅ </summary>

</details>

<br>

<details>
<summary>✅ </summary>

</details>

<br>

<details>
<summary>✅ </summary>

</details>

<br>

<details>
<summary>✅ </summary>

</details>

<br>

<details>
<summary>✅ </summary>

</details>

<br>

<details>
<summary>✅ </summary>

</details>

<br>
