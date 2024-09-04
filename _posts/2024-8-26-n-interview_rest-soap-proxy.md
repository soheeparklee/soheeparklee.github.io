---
title: Interview_SOP/ CORS/ REST/ SOAP/ cache/ proxy/load balancing
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
<summary>✅ Input validation 어떻게 구현하는지? </summary>
- 폼 데이터 <br>
- Script tag 걸러주기 <br>
- 인풋에 특수문자 삭제하기, 일반 문자로 바꾸기<br>
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
💊 sanitize user data <br>
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
- 자원을 이름으로 구분(URI), 자원의 상태를 주고받기 <br>
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

## 📌 Web cache

<details>
<summary>✅ What is web cache? What are the benefits of using cache? </summary>
- copied data to remember frequent request<br>
👍🏻 reduce network bottleneck  <br>
👍🏻 bandwidth ⬆️ <br>
</details>

<br>

<details>
<summary>✅ What is cache hit, miss? </summary>
- cache hit: find request in cache <br>
- cache miss: do not find request in cache, need to go to original server<br>
</details>

<br>

<details>
<summary>✅ What is cache revalidation?</summary>
- check if cache data is identical to original server data<br>
</details>

<br>

## 📌 Proxy server

<details>
<summary>✅ What is proxy server?</summary>
- intermediary between server-client <br>
- connect application using same protocol <br>
</details>

<br>

<details>
<summary>✅ Forward proxy server? </summary>
- 클라이언트 앞에  <br>
- exit point from client to server <br>
- outbound traffic <br>
- protect client information <br>
</details>

<br>

<details>
<summary>✅ Reserse proxy server? </summary>
- 서버 앞에  <br>
- entry point to server <br>
- inbound traffic
- protect server <br>
</details>

<br>

<details>
<summary>✅ What are some functions of a proxy server?</summary>
- load balancing <br>
- security <br>
- caching <br>
- SSL termination <br>
- filtering <br>
- access control<br>
- surrogate: reverse proxy<br>
- contents router <br>
- transcoder <br>
- anoymizer <br>
</details>

<br>

<details>
<summary> Proxy 🆚 Gateway </summary>
- proxy: connect application using same protocol <br>
- gateway: connect application using different protocol  <br>
</details>

<br>

<details>
<summary> Proxy 🆚 VPN </summary>
- proxy: handle network traffic <br>
- VPN: encrypt transmitted data <br>
</details>

<br>

<details>
<summary>✅ Is WAF a reverse proxy?</summary>
- YES. intercept traffic before reaching server <br>
</details>

<br>

## 📌 Load Balancing

<details>
<summary>✅ What does a level 4 load balancer do?</summary>
- route traffic based on IPs and TCP, UDP ports <br>
- packet level load balancing <br>
- unable to make routing decisions based on contet, media type, localization rules <br>
- ASIC <br>
</details>

<br>

<details>
<summary>✅ What does a level 7 load balancer do?</summary>
- routing decisions based on IP, TCP, UDP, ports, HTTP<br>
- makes content based routing decisions <br>
- acts as a proxy: contain two TCP connections <br>
   (one with client, another with server)<br>
</details>

<br>

## 📌 Request timeout

<details>
<summary>✅ Why do we use timeout? </summary>
- networks are unreliable <br>
- set a max wait time on request <br>
- client: how long client will wait for response <br>
- server: how long to maintain connection <br>
</details>

<br>

<details>
<summary>✅ What is a connection timeout? </summary>
- how long the client will wait for a connection to establish <br>
- TCP 연결 확립이 수행되는데 걸리는 최대 시간  <br>
</details>

<br>

<details>
<summary>✅ What is a write timeout? </summary>
- how long connection will wait while the client tries to send a data, like POST <br>
</details>

<br>

<details>
<summary>✅ What is a read timeout? </summary>
- time it takes to recieve response back from the server <br>
- 요청과 응답이 수행되는데 걸리는 최대 시간  <br>
</details>

<br>
