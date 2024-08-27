---
title: Interview_HTTP/HTTPS/Digital Signature/TLS/SSL/DNS/JWT
categories: [Computer Science, Network]
tags: [interview] # TAG names should always be lowercase
---

## 📌 HTTP

HTTP, HTTPS 정리글 <https://soheeparklee.github.io/posts/n-6httphttps/> <br>

<details>
<summary>✅ What is HTTP?</summary>

Hypertext Transport Protocol <br>
<br>

- allow data transfer in WWW <br>
- client-server <br>
  <br>
- HTTP request: method <br>
- HTTP response: status code <br>
- message: status line + header + body <br>
  <br>
- connectionless <br>
- stateless: cookie, session <br>
  <br>
- HTTP 1.0: non-persistent <br>
- HTTP 1.1: persistent, pipelining <br>
- HTTP 2: multiplexing, server push <br>
- HTTP 3: UDP <br>
- pipelining 🆚 multiplexing <br>

</details>

<br>

<details>
<summary>✅ How is the request of HTTP? And its message format? </summary>
- HTTP requst: method  <br>
  <br>
- GET  <br>
- POST  <br>
- HEAD  <br>
- PUT  <br>
- PATCH  <br>
- DELETE  <br>
- CONNECT  <br>
- OPTIONS  <br>
- TRACE  <br>
 <br>
- message format: status line + header + body  <br>
- header: host, user-agent, accept-languge, encoding, charset  <br>
</details>

<br>

<details>
<summary>✅ What is inside status line?</summary>
- HTTP version, HTTP method(request) or status code(response) <br> 
</details>

<br>

<details>
<summary>✅ What is the difference between GET and POST?</summary>
- GET: fetch data from server, data on HTTP packet header  <br>
- POST: send client data to server, data on HTTP packet body  <br>
</details>

<br>

<details>
<summary>✅ Why is data on header for GET and body for POST?</summary>
- visibility: data in header(GET) are part of URL parameters <br>
- security: header visible in URL param ➡️ less secure, shows <br>
- length limitation: URL has limit <br>
- GET on header will be cacheable <br>
- data in POST will be secure in body <br>
</details>

<br>

<details>
<summary>✅ What is the difference between PUT and PATCH?</summary>
- PUT: change all data on server  <br>
- PATCH: change part of data on server  <br>
</details>

<br>

<details>
<summary>✅ How is the response of HTTP? And its message format? </summary>
- HTTP response: status code <br>
 <br>
- 200: get success <br>
- 201: post success <br>
- 3xx: redirect <br>
- 4xx: client error <br>
- 400: bad request <br>
- 401: unauthorized <br>
- 404: cannot find resource <br>
- 5xx: server error <br>
- 500: internal server error <br>
- 502: gateway error <br>
 <br>
- message format: status line + header + body <br>
- header: data, server, last-modified, content-type <br>

</details>

<br>

<details>
<summary>✅ What is HTTP header?</summary>
- Part of HTTP request, response message with information about the message <br>
- Request: host, user-agent, keep-alive, accept language, charset, encoding that browser can accept  <br>
- Response: date, server, last modified, content-type, cache-control <br>
</details>

<br>

<details>
<summary>✅ What is HTTP keep-alive?</summary>
- HTTP is connectionless  <br>
- HTTP connection: persistent, non-persistent  <br>
- HTTP/1.0: non-persistent  <br>
- From HTTP/1.1: can keep connection  <br>
  <br>
- keep-alive: feature of HTTP/1.1  <br>
- header to set timeout, maximum of requests(limit pipelining)  <br>
</details>

<br>

<details>
<summary>✅ What is pipelining? Benefits and disadvantages?</summary>
- From HTTP/1.1  <br>
- persistent connection  <br>
- do not have to wait for response, can send several request  <br>
- however, recieve response in order (123 ➡️ 123)  <br>
- 👍🏻 network latency lower  <br>
- 👎🏻 head of line blocking  <br>
</details>

<br>

<details>
<summary>✅ What is multiplexing?</summary>
- From HTTP/2  <br>
- like pipelining, but dont have to recieve in order (123 ➡️ 준비되는 response부터 받음)  <br>
</details>

<br>

<details>
<summary>✅ Evolution of HTTP?</summary>
- HTTP/1.0: TCP, non-persistent  <br>
- HTTP/1.1: persistent, pipelining  <br>
- HTTP/2: multiplexing, server push  <br>
- HTTP/3: UDP  <br>
</details>

<br>

<details>
<summary>✅ What is HTTP/2 server push?</summary>
- server proactively sends resource even before client requests!  <br>
</details>

<br>

<details>
<summary>✅ What is HTTP stateless?</summary>
- HTTP server will not remember the client request  <br>
- need session, cookie  <br>
</details>

<br>

<details>
<summary>✅ What is a cookie, session?</summary>

<strong>Cookie: </strong>

<ul>
  <li>track user behavior</li>
  <li>client holds cookie</li>
  <li>👎🏻 Malicious user can alter, forge cookie</li>
</ul>
<br>

<strong>Session:</strong>

<ul>
  <li>authenticate user</li>
  <li>saved on server DB, memory</li>
  <li>👍🏻 Can kickout user if maicious behavior </li>
  <li>👎🏻 Difficult to scale server</li>
  <li>👎🏻 Burden on server(need to save user session)</li>
</ul>

</details>

<br>

<details>
<summary>✅ What is JWT?</summary>
- issued by server with digital signature(with server's private key)  <br>
- user shows this JWT everytime requesting to server  <br>
- server verifies JWT with public key  <br>
</details>

<br>

<details>
<summary>✅ How is JWT structure? </summary>
- Header.Payload.Signature  <br>
- Header: algorithm, type, key for digital signature  <br>
- Payload: JWT information(claim) client information, token created date...  <br>
- Signature: encode [Header+Payload] and sign with private key  <br>
</details>

<br>

<details>
<summary>Session 🆚 Cookie 🆚 JWT</summary>

<a href="https://soheeparklee.github.io/posts/Spring_cookie_session_jwt/"> 🔗 session, cookie, token</a>

</details>

<br>

---

## 📌 HTTPS, SSL/TLS

<details>
<summary>✅ What is HTTPS?</summary>
- HTTP over SSL  <br>
- send data encrypted  <br>
- use symmetric, assymetric encryption  <br>
</details>

<br>

<details>
<summary>✅ How does HTTPS work?</summary>
- server asks CA to issue digital certificate <br>
- CA issues digital certificate with server's public key <br>
- client has CA's public key <br>
- client asks server for server's certificate and decrypts with CA's public key  <br>
- now client has server's public key <br>
- ⭐️ when verified, client creates symmetric key and encrypts with server's public key <br>
- server decrypts symmetric key with server's private key <br>
- now server and client can communicate with symmetric key <br>

</details>

<br>

<details>
<summary>✅ What is symmetric key? Algorithm? </summary>
- same key for encryption, decryption <br>
- private key <br>
- DES, IDEA, AES, RC Cipher Suite <br>
</details>

<br>

<details>
<summary>⭐️ What is asymmetric key? Two ways to use asymmetric keys? Algorithm? </summary>
- public key, private key <br>
- encrypt with public key, decrypt with private key: when sharing symmetric key in HTTPS <br>
- encrypt with private key, decrypt with public key: digital signature <br>
 <br>
- Diffie Hellman, RSA, ECC <br>
</details>

<br>

<details>
<summary>✅ What is digital signature? Benefits? Algorithm? </summary>
- non-repudiation: it is me who encrypted this file!  <br>
- data integrity <br>
 <br>
- DSA, RSA <br>

<a href="https://soheeparklee.github.io/posts/n-symmetric_assymetric/">🔗 Symmetric, assymetric, digital signature</a>

</details>

<br>

<details>
<summary>✅ What is TLS/SSL?</summary>
- provide network transport security <br>
- operate at session layer(layer 5) <br>
- TLS: improved SSL <br>
- handshake, use CA, certificate, symmetric, assymetric encryption, digital signature
</details>

<br>

<details>
<summary>✅ What is TLS/SSL handshake?</summary>
- client hello <br>
- server hello <br>
- client verify, create symmetric key <br>
- client encrypt symmetric key with server's public key <br>
- server decrypts symmetric key with private key <br>
- create master secret and session key <br>
- communication encrypted with session key <br>

<a href="https://soheeparklee.github.io/posts/n-7tlshandshake/">🔗 TLS/SSL</a>

</details>

<br>

<details>
<summary>✅ Why not only use assymetric/public key? </summary>
- public key uses a lot of computer power <br>
</details>

<br>

<details>
<summary>✅ Why not only use symetric/private key?</summary>
- client and server needs to share private key <br>
- in order to do this, need encryption, thus need public key <br>
</details>

<br>

<details>
<summary>✅ Why use SSL/TLS over HTTP? </summary>
- HTTP: application layer <br>
- SSL/TLS: sesison layer <br>
- HTTP exchange data with plain text <br>
- SSL, TLS encrypt data <br>
</details>

<br>

<details>
<summary> ✅ Cases where digital signature is used? </summary>

- HTTPS authentication <br>
- <strong>DKIM</strong>(Domain Keys Identified Mail): <br>
  &emsp; - Add digital signature to email header <br>
  &emsp; - can verify sender of the email <br>
- code signing <br>

</details>

<br>

---

## 📌 DNS

https://soheeparklee.github.io/posts/n-6httphttps/

<details>
<summary>✅ What is domain name?</summary>
- IP address in human readable format <br>
</details>

<br>

<details>
<summary>✅ What is DNS?</summary>
- Domain Name System: domain name ➡️ IP address <br>
- distributed database, has hierarchy <br>
- application layer <br>
- UDP <br>
- port 53 <br>
</details>

<br>

<details>
<summary>✅ What are the benefits of DNS being hierarchical, distributed?</summary>
- manage requests more efficiently <br>
- more scalable <br>
</details>

<br>

<details>
<summary>✅ What is the benefit of one domain name being corresponded to several IP addresses?</summary>
- can distribute the load <br>
</details>

<br>

<details>
<summary>✅ Why does DNS operate with UDP?</summary>
- prioritize speed over reliability <br>
- DNS has lots of users! lots of request <br>
- DNS requests are small enough to fit in UDP <br>
</details>

<br>

<details>
<summary>✅ How is DNS hierarchy?</summary>
- Root DNS server <br>
- Top Level Domain server (.com) <br>
- Authoritative Domain server (google, apple) <br>
</details>

<br>

<details>
<summary>✅ What is DNS recursor? Local DNS server?</summary>
- recursive recursor <br>
- server that responds wo DNS query <br>
- ask another DNS server for IP address <br>
- local DNS server <br>
</details>

<br>

<details>
<summary>✅ Types of DNS service? </summary>
- Recusive DNS resolver <br>
- Authoritative DNS server <br>
</details>

<br>

<details>
<summary>✅ Types of DNS queries? Disadvantages of recursive query?</summary>
- Non-recursive query <br>
- Recursive query: 👎🏻 DNS resolver burden ⬆️ <br>
- Iterative query <br>
</details>

<br>

<details>
<summary>✅ What is DNS record?</summary>
- information on database that linkes URL to IP address <br>
- A, AAA, CNAME, TXT
</details>

<br>

<details>
<summary>✅ What is DNS cache? Benefit? </summary>
frequently visited site IP address saved on device <br>
- 👍🏻 speed up DNS request <br>
- 👍🏻 reduce bandwidth <br>
</details>

<br>

<details>
<summary>✅ How does DNS work?</summary>
- request domain name <br>
- check local DNS cache <br>
- contact DNS resolver <br>
- recursive server lookup <br>
- query root name server <br>
- query TLD name server <br>
- query authoritative name server <br>
- get IP address <br>
- client access website <br>

</details>

<br>

---

## 📌 URI/URN/URL

<details>
<summary>✅ What is difference between URI, URL, URN?</summary>
- URI ⊃ URL, URN <br>
- URL = protocol + URI
</details>

<br>

<details>
<summary>✅ What are the disadvantages of URL, and how can we overcome? </summary>
- when location of resource changes, URL will change  <br>
- URN will remain fixed   <br>
</details>

<br>

---

## 📌 What happens when I type URL in web browser?

<details>
<summary>✅ What happens when I type URL in web browser?</summary>
- type URL, enter
- browser translate, encode URL
- check if HTTPS is needed on HSTS list
- check local cache for IP address
- If cache does not have, get IP address of domain name from DNS 
- get MAC address from IP address with ARP
- browser initiate TCP connection
- If HTTPS needed, make SSL/TLS handshake
- send HTTP request to server
- server sends response
- browser rendering, show response to user: DOM tree
</details>

## <br>

## 📌 VPN/ SSL/TLS encryption

<details>
<summary>✅ VPN and SSL/TLS both serves encryption. How are they different?</summary>
- VPN: enables encryption between computer and private network
(remote access to company network from home)
- use various types of tunneling protocols

- SSL/TLS: encryption between applications
- use symmetric, assymetric encryption in SSL handshake
</details>

<br>

---

## 📌 Session

<details>
<summary>✅ What is session in OSI 7 Layer? and what is session to remeber the user? </summary>
- although name session is same, they serve different functions

- session in OSI 7 Layer: controls connection between two computers
- web application session: as HTTP is statelss, use session to remember the user
</details>

<br>

---

## 📌 TLS

<details>
<summary>✅ On what OSI7 layer does TLS function, and why? </summary>
- Although TLS has name transport layer, 
- TLS is used on OSI session layer(layer 5)
- as it's job is to encrypt session between client and server

- OSI transport layer(layer 4): reliable transport of data between client and server(TCP, UDP)
</details>

<br>

<details>
<summary>✅ 23/Aug Feedback </summary>
소희님
9:44 ~ 9:59

- 보완 질문

* 대칭키 비대칭키 -> 답변을 조금 정리하면 좋을 것 같습니다!
* 개발자로서의 단점

- 좋은 점

* 톤 앤 매너 100점
* 긴장하지 않고 편안하게 말하는 점은 본 받고 싶습니다.
* 질문에 대한 답변만 준비한 것이 아니라 체내화한 지식을 기반으로 답변하는 것 같아 매우 똑똑해보입니다.
* 개발자가 되려는 이유 답변 구성이 좋았습니다.
* (사고를 할 수 있는 인재라는 느낌을 받아서 채용하고 싶었습니다)

- 쪼금 보완하면 좋을 점

* 조금만 천천히 말씀하셔도 좋을 것 같습니다!
* 관련 개념에 대해서 자세하게 설명해주신 점은 강의를 듣는 것처럼 정말 좋았지만
  면접이라는 상황을 고려하면 답변을 조금 줄여도 괜찮을 것 같습니다!

</details>

<br>
