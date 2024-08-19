---
title: HTTP/ HTTPS
categories: [Computer Science, Network]
tags: [] # TAG names should always be lowercase
---

## ✅ HTTP

> Hypertext Transport Protocol

- allow data transfer in `World Wide Web`
- transmit `HTML`, `CSS`, `JS`
- operates on TCP(HTTP3 operates on UDP)
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
  - client and server connection
- **OPTIONS**
- **TRACE**

### ☑️ HTTP request message format

<img width="723" alt="Screenshot 2024-08-19 at 23 54 09" src="https://github.com/user-attachments/assets/f96abe37-da66-4415-9be9-bf3f02e734e7">

- ASCII(human readable)
- first line is request line

- `request line`: HTTP version, HTTP method
- `Host`
- `User-Agent`
- `Accept-Language`
- `Accept-Encoding`
- `Accept-Charset`
- `Conection`
- `Keep-Alive`

## 📌 HTTP response(Status code)

- Status code

💡 <https://soheeparklee.github.io/posts/n-httpstatuscode/>

### ☑️ HTTP response message format

- `Status Line`
- `Date`
- `Server`
- `Last-Modified`
- `Content-Length`
- `Content-Type`

✔️ **주요 Header** <br>

- Host: 요청하는 서버 주소 & 포트 domain, port, IP address
- Accept: 원하는 데이터 형식
- Connetion: 커넥션 유지 여부(연결성을 유지할 것인가? 선택할 수 있음)
- Content-type: 요청 데이터 포맷

✔️ **응답 Message** <br>

- 응답 코드, 응답 메세지: 숫자에 따라 결과 보여줌
- Body: 응답 데이터
- Content-type: 응답 데이터 포맷

## ✅ Connectionless

> connectionles: once request and response is over, terminate connection <br>

- 👍🏻 Server does not have to keep connection with several clients
- 👎🏻 Server has to make new connections all the time, overhead ⬆️

- Non-persistent connection
  - Once TCP connection, one request and one response
  - over head for client and server
- persistent connection
  - Once TCP connection, can send several requests and responses
  - Keep connection even after response from server
  - terminate connection after certain time
  - default from HTTP/1.1

## ✅ Stateless

> HTTP is a stateless protocol <br>
> HTTP server does not remember the client request <br>
> thus, HTTP server cannot distinguish the client. <br>

- If there is need to remember the client, need to use `cookie` or `session`

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
