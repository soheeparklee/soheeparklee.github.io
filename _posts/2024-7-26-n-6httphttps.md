---
title: HTTP/ HTTPS
categories: [Computer Science, Network]
tags: [] # TAG names should always be lowercase
---

## ✅ HTTP

> Hypertext Transport Protocol

## ✅ HTTP 요청, 응답 구조

### ☑️ HTTP 요청 message와 HTTP method

#### ✔️ HTTP 요청 message

method ➕ URI ➕ http version<br>
<br>
※ URL은 URI의 일종이다<br>

#### ✔️ HTTP method

- GET
- PUT
- POST
- DELETE

#### ✔️ 주요 Header

- Host: 요청하는 서버 주소 & 포트 domain, port, IP address
- Accept: 원하는 데이터 형식
- Connetion: 커넥션 유지 여부(연결성을 유지할 것인가? 선택할 수 있음)
- Content-type: 요청 데이터 포맷

#### ✔️ 응답 Message

- 응답 코드, 응답 메세지: 숫자에 따라 결과 보여줌
- Body: 응답 데이터
- Content-type: 응답 데이터 포맷

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
