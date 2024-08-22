---
title: TLS/ SSL HandShake
categories: [Computer Science, Network]
tags: [] # TAG names should always be lowercase
---

## ✅ TLS/SSL

**SSL**

> Secure Socket Layer <br>

- provide network transport security <br>
- prevent eveasdropping, forgery of transport data of server-client <br>
- encrypt data over client-server <br>

> **TLS**
>
> > Transport Layer Security

> **Handshake**
>
> > Before client and server communicates in HTTTS, checks SSL for security

## ✅ TLS/SSL Handshake

![Screenshot 2024-07-27 at 09 51 45](https://github.com/user-attachments/assets/f5290ed5-caa2-4a68-9227-7dfa109a5ebd)

- SSL is created of three phases. `SSL handshake` - `Session` - `Terminate Session`
- HTTPS operates on SSL

### 1️⃣ SSL handshake(1~8)

- First, server and client decides which `algorithm` to use
- When `algorithm` is decided, create `symmetric key` and share

**1. Client Hello** <br>
Client sends `client hello` message to server <br>
`client hello` message holds such as `client random data`, `version`, `encryption algorithm` <br>
if server and client has had `SSL handshake`, send `session key` to reuse the `session` <br>

- `random data`: random dara
- `version`
- `encryption algorithm`: what kind of encryption algorithm the client can use

**2. Server Hello** <br>
Server recieves `client hello`, replies with `server hello` <br>
Server decides which `encryption algorithm` to use from the list of algorithms that the client sent <br>
`server hello` message includes `server random data`, `session ID`, `CA public key certificate` <br>

- `server random data`
- `CA public key certificate` holds public key <br>

**3. Client verify, create pre master secret(symmetric key)** <br>
Client checks if `CA public key certificate` is valid <br>
Then create `pre master secret`, also called `random key byte` <br>

- To check if `CA public key certificate` `digital signature` is valid, use `public key` from `CA`
- the certificate has Digital signature by `CA`
- If verified, the client will trust the server
- If `CA public key certificate` is valid, client creates `random key byte` also called `pre master secret`
- Client creates `symmetric key`, called `pre master secret`, combining `client random data` and `server random data`
- This `pre master secret` will be used as`symmetric key` for encryption in client-server communication
- This `random key byte` is used for symmetric key <br>

**4. Encrpyt `pre master secret` with `server's public key`** <br>

- Then, send to server <br>
- ⭐️ Assymetric key used<br>

**5. If in step 2, server required client certificate, send client cerfiticate** <br>

**6. Server checks `random key byte`, decrypts `random key byte`(`pre master secret`) with `server private key`.** <br>

- Server checks client certificate <br>
- ⭐️ Assymetric key used <br>

**7. Create master secret and session key** <br>

- Client sends `finished` message saying handshake is complete.
- Now, server and client will create `master secret` from `pre master secret`
- And use `master secret` to create `session key` <br>
- Hash the transmission messages then encrypts with `symmetric key` and sends to server. <br>

**8-1.** Server also hashes transmission messages and checks if they match. <br>

- If matches, server also sends `finished` message(encrypted with `symmetric key`). <br>

**8-2.**Client decrypts message and checks the server is safe, now two parties will share data with `symmetric key`. <br>

### 2️⃣ Session(9)

- Server and Client exchange messages
- messages are encrypted with `session key` which is a symmetric key
- decryption is also possible with `session key`

### 3️⃣ Terminate Session

- When transmission of data is over, server and client tells each other that the communication is over
- Then dispose `session key`

> 💡 **When is symmetric key used?** <br>
>
> > In level 3, using `pre-master-secret` which is a symmetric key <br>
> > During session, when server and client is exchanging messages with `session key` <br>

> 💡 **When is asymmetric key used?** <br>
>
> > In level 4, to send `pre-master-secret` to the server, encrypt the secret with `server's public key` <br>
> > In level 6, server will decrypt `pre-master-secret` using its `private key` <br>

> 💡 **When is digital signature used?** <br>
>
> > In level 3, when client verifies the certification from server <br>
> > the server certificate has digital signature by CA <br>

> 💡 **Why not only use public key?** <br>
>
> > - 👎🏻 public key uses a lot of computer power
> > - If lots of traffic occur on public key using server, the server will have high cost <br>

> 💡 **Why not only use symmetric key?** <br>
>
> > - In order to use `private key`, the server and client needs to share the `private key` <br>
> > - Cannot share `private key` without encryption ➡️ need to encrypt with` public key` <br>

## ✅ Why use SSL/TLS over HTTP?

![Screenshot 2024-08-21 at 18 11 19](https://github.com/user-attachments/assets/c373758a-425c-41a4-ac80-eaa5c0646cae)

- HTTP exchanges message with plain text
- 👎🏻 easy to steal data
- HTTPS is a secure version of HTTP, which is HTTP on SSL/TLS
- every HTTP message that is sent on HTTPS is encrypted, decrypted by SSL/TLS
