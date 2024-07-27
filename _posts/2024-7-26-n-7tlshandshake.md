---
title: TLS/ SSL HandShake
categories: [Computer Science, Network]
tags: [] # TAG names should always be lowercase
---

## ✅ TLS/SSL

> TLS
>
> > Transport Layer Security

> SSL
>
> > Secure Socket Layer

> Handshake
>
> > Before client and server communicates in HTTTS, checks SSL for security

## ✅ TLS/SSL Handshake

![Screenshot 2024-07-27 at 09 51 45](https://github.com/user-attachments/assets/f5290ed5-caa2-4a68-9227-7dfa109a5ebd)

1. Client sends `client hello` message to server <br>
   `client hello` message holds such as `version`, `encryption algorithm` <br>
2. Server recieves `client hello`, replies with `server hello` <br>
   `server hello` message includes `session ID`, `CA public key certificate` <br>
   `CA public key certificate` holds public key <br>
3. Client checks if `CA public key certificate` is valid <br>
4. If `CA public key certificate` is valud, client creates `random key byte` and encrpyts with `server's public key` <br>
   This `random key byte` is used for symmetric key <br>
5. If in step 2, server required client certificate, send client cerfitivate and `random key byte` encrypted with client private key <br>
6. Server checks client certificate, decrypts `random key byte` with `private key`. <br>
7. Client sends `finished` message saying handshake is complete. Hash the transmission messages then encrypts with `symmetric key` and sends to server. <br>
8. Server also hashes transmission messages and checks if they match. If matches, server also sends `finished` message(encrypted with `symmetric key`). <br>
9. Client decrypts message and checks the server is safe, now two parties will share data with `symmetric key`. <br>
