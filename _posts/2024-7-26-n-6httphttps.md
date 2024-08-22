---
title: HTTP/ HTTPS
categories: [Computer Science, Network]
tags: [] # TAG names should always be lowercase
---

## ✅ HTTP

> Hypertext Transport Protocol

- allow data transfer in `World Wide Web`
- transmit `HTML`, `CSS`, `JS`
- operates on `TCP`(HTTP3 operates on UDP)
- use port `80`

> **What are the two types of HTTP messages?**
>
> > - request <br>
> > - response <br>

## ✅ Cient-Server Model

- HTTP is consisted of `client` and `server`
- when client sends `HTTP request`, server responds with `HTTP response`

> **What are examples of HTTP client?** <br>
>
> > - chrome <br>
> > - Internet explorer <br>
> > - Firefox <br>

## 📌 HTTP Request(Method)

<img width="724" alt="Screenshot 2024-08-03 at 10 17 19" src="https://github.com/user-attachments/assets/51d678f1-9060-4b5f-a51b-d8ad6e586784">

- HTTP supports requests that is called HTTP methods
- method ➕ URI ➕ http version<br>
-

- **GET**
- **HEAD**
  - simmilar to get
  - request for document ❌
  - request for header(information of document) ⭕️
  - body: empty
  - only header information
- **POST**
- **PUT**
  - update resource
- **PATCH**
  - to update, but update _part_ of resource
- **DELETE**
- **CONNECT**
  - request http URL
  - establish tunnel to the server with URI
- **OPTIONS**
  - find server supports which request method
  - communicate with whole server? or with particular URL?
- **TRACE**
  - echo back to server whatever string is sent for debugging

### ☑️ HTTP request message format

<img width="569" alt="Screenshot 2024-08-20 at 00 10 08" src="https://github.com/user-attachments/assets/8447c8a7-738b-4ff3-a2a5-856f54500669">

- ASCII(human readable)

1. **Status line**

- `request line`:
  - HTTP Protocol version
  - HTTP method
  - Request target: URL

2. **Header**

- `Host`: server domain address
- `User-Agent`: user web browser type, version

- `Accept-Language`: What language the browser can accept
- `Accept-Encoding`: What encoding browser can accept(컨텐츠 압축 방식)
- `Accept-Charset`: What charset browser can accept(문자 인코딩 방법)
- `Conection`: (default) keep-alive, use persistent connection
- `Keep-Alive`: persistent connection duration time(연결 지속 시간)

3. **Body**

- 본문

## 📌 HTTP response(Status code)

- 1xx
- 2xx
- 3xx
- 4xx
- 5xx

💡 <https://soheeparklee.github.io/posts/n-httpstatuscode/>

### ☑️ HTTP response message format

<img width="497" alt="Screenshot 2024-08-20 at 00 06 18" src="https://github.com/user-attachments/assets/cd744615-2edd-4423-b5e1-73e9d8095130">

1. **Status Line**

- `Status Line`
  - HTTP version
  - response code
  - reason phase: status text(response code in text, `example: OK`)

2. **Headers**
   > decide how data should be used

- `Date`
- `Server`: server that sent the response
- `Last-Modified`
- `Content-Length`
- `Content-Type`: image/jpg

3. **Body**

- 본문

## 💡 HTTP keep-alive

> feature of HTTP/1.1 <br>
> header to set a **timeout**, **maximum of requests** <br>

- only used in HTTP1
- header `connection`, `keep-alive` is prohibited on HTTP2, HTTP3

- **timeout**: time in seconds that the host will **allow idle connection open** before it is closed
  - idle connection: no data sent/recieved by host
  - 주고받는 데이터 없어도 `timeout초` 동안은 connection 열어두기
  - connection이 최소한 얼마나 열려있을 것인가
- **max**: number of requests that can be sent on this connection before closing
  - used to limit pipelining

```
HTTP/1.1 200 OK
Connection: Keep-Alive
Content-Encoding: gzip
Content-Type: text/html; charset=utf-8
Date: Thu, 11 Aug 2016 15:23:13 GMT
Keep-Alive: timeout=5, max=1000
Last-Modified: Mon, 25 Jul 2016 04:32:39 GMT
Server: Apache

(body)
```

## ✅ Evolution of HTTP

### ☑️ HTTP/1.0

- TCP
- **Non-persistent** connection
- one connection one request, one response
- 👎🏻 when many request is needed, need to create several connection, overhead

### ☑️ HTTP/1.1

- **persistent** connection
- **pipelining**

<img width="585" alt="Screenshot 2024-08-20 at 15 12 15" src="https://github.com/user-attachments/assets/1b219801-03b7-40e0-884f-b32ae8d2be1e">

### ☑️ HTTP/2

<img width="704" alt="Screenshot 2024-08-20 at 15 35 24" src="https://github.com/user-attachments/assets/6a95e559-b8f3-4162-b720-cdc90e2aeefb">

- **multiplexing**: multiple request and responses sent over a single TCP connection **concurrently**
- parallel processing: run parallel requests in same connection
- 👍🏻 no need for multiple connections, reduce latency
- **server push**:

  - server proactively sends resource even before client explicitly requests them
  - save data in client cache
  - client doesnt have to make additional requests
  - (example: server push JS and CSS too when client only asked for HTML, client doesnt have to request for JS, CSS now)

- not text protocol anymore, binary protocol
- compress header

### ☑️ HTTP/3

- do not use TCP anymore, use QUIC, UDP
- QUIC: Quick UDP Internet Connections
- built in TLS: data encryption
- multiplexing
- server push

## 💡 HTTP Pipelining

> feature of HTTP/1.1 <br>
> allow HTTP **requests** to be sent over a **single** TCP connection <br>
> without **waiting** for corresponding response <br>

<img width="296" alt="Screenshot 2024-08-20 at 14 49 19" src="https://github.com/user-attachments/assets/173b6365-1698-40d0-b3f5-a1127bbd05a6">

- 👍🏻 network latency ⬇️, as do not need to wait for resposne
- 👎🏻 Head of line blocking: last response will be delayed
- HTTP pipelining was replaced by **Multiplexing** in HTTP/2

## ✅ Connectionless

> HTTP client and server makes TCP connection <br>
> connectionless: once request and response is over, terminate connection <br>

- 👍🏻 Server does not have to keep connection with several clients
- 👎🏻 Server has to make new connections all the time, overhead ⬆️

- HTTP 1.0 adds `KeepAlive header` to persist HTTP connection

### ☑️ Non-persistent connection **(HTTP/1.0)**

- Once TCP connection, one request and one response
- for new request, need new connection
- overhead for client and server

### ☑️ persistent connection **(HTTP/1.1)**

- Once TCP connection, can send **several** requests and responses
- Keep connection even after response from server
- terminate connection after certain time
- default from HTTP/1.1
- 👎🏻 need to keep connection even when there is no request, response
- 👎🏻 DDoS attack

## ✅ Stateless

> HTTP is a stateless protocol <br>
> HTTP server **does not remember** the client request <br>
> thus, HTTP server cannot distinguish the client. <br>

- If there is need to remember the client, need to use `cookie` or `session`

💡 Cookie, Session, JWT <https://soheeparklee.github.io/posts/Spring_cookie_session_jwt/>

## ✅ HTTPS

> Hypertext Transport Protocol SSL <br>
> to safely encrypt data sent on network <br>
> assymetric encryption <br>

1. A makes `private key` and `public key` for **HTTPS** <br>
2. A asks CA to safely guard his `public key` <br>
3. CA will make a certificate based on A's name, `public key` and encryption method, <br>
   and encrpyt the certificate using the CA's private key. <br>
4. A has encrypted certificate. <br>
5. When A has request that is not HTTPS, gives this cerficiate to the client. <br>
6. Client decrypts, now has A's public key. <br>
7. Client creates `pre-master-key(symmetric key)` and encrypts using A's public key. <br>
8. A recieves the `pre-master-key(symmetric key)` and decrypts using his private key. <br>
9. For connection, A and client uses the `pre-master-key(symmetric key)` <br>

## ✅ Symmetric Key, Assymetric Key, Digital Signature

💡 <https://soheeparklee.github.io/posts/n-symmetric_assymetric/>

## ✅ SSL/TLS

💡 <https://soheeparklee.github.io/posts/n-7tlshandshake/>

## ✅ HTTPS scheme

- HTTP scheme: `http://`
- HTTPs scheme: `https://`
- when client such as web browser is requested for a web resource, check `URL scheme`
- If `URL scheme` has `http`, port number `80` and request for `HTTP`
- If `URL scheme` has `https`, port number `443` and request for `HTTPS`, does SSL handshake

## ✅ How HTTPS works

<img width="536" alt="Screenshot 2024-08-21 at 18 20 38" src="https://github.com/user-attachments/assets/9a6fd500-aaa7-4538-9623-720f1aaafc35">

#### ☑️ HTTP

- client opens `TCP` connection with web server `port 80`
- send HTTP request
- reviece HTTP response from server
- close TCP connection

#### ☑️ HTTPS

- client opens `TCP` connection with web server `port 443`
- SSL handshake: encrypt algorithm, `pre master secret`
- when SSL connection is complete, client send HTTP request to SSL layer
- client HTTP request is encrypted by SSL layer before sending it to TCP layer

## ✅ Digital Certificate

> certificate with host information, issued by CA

- During SSL handshake, client verifies server with server's certificate
- server's certificate has `digital signature` from the `CA`

- **Certificate carries information** such as

  - web site name
  - web site host name
  - web site public key
  - CA name
  - CA digital signiture

- **Types of digital certificate** are

  - Wildcard certificate: same root
  - SAN field: Subject Alternative Name, dont have same root
  - Single, Double sided:
    - single: only server has to be validated
    - double: both server, client has to validate each other
  - Self signed certificate
  - Third Party certificate

- Client connects to server via HTTPS
- server sends certificate to client
- client verifies this certificate with `digital signature by CA`
- if CA is trusted, client will have `CA public key`
- verify the `certificate`(more precisely, `digital signature` on certificate) using `CA's public key`

<img width="1445" alt="Screenshot 2024-08-21 at 19 41 35" src="https://github.com/user-attachments/assets/ffcb4204-10b8-4446-b7e3-d29e17e7b1b7">
