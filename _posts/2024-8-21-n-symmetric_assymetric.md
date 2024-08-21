---
title: Symmetric/ Asymmetric key algorithm
categories: [Computer Science, Network]
tags: [] # TAG names should always be lowercase
---

[8. Cryptographic Solutions.pdf](https://github.com/user-attachments/files/16688547/8.Cryptographic.Solutions.pdf)

## ✅ Symmetric key algorithm

1. A sends message encrypted with B’s `public key` <br>
2. B recieves and decrypts with B’s `private key` <br>
3. B sends message encrypted with A’s `public key` <br>
4. A recieves and decrypts with A’s `private key` <br>

- **Private key** encryption
- Same key for encryption, decryption
- 👍🏻 faster
- 👎🏻 lack non-repudiation
- 👎🏻 large scale use
- 👎🏻 easy to decrypt

#### ☑️ Symmetric algorithm

- **DES**: Data Encryption Standard
- 3DES
- **IDEA**: International Data Encryption Algorithm
- **AES**: Advanced Encryption Standard
- Blowfish
- Twofish
- **RC Cipher suite**
  - RC4: Stream cipher, SSL, WEP(wired equivalent privacy)

## ✅ Asymmetric key algorithm

- **Public key** encryption
- different key for encryption and decryption
- 👍🏻 solve key distribution challenge
- 👎🏻 slower
- ⭐️ public key: encryption
- ⭐️ private key: decryption

- asymmetric algrithm can be done in two ways

#### ☑️ Asymmetric algorithm

- **Diffie-Hellman**

  - key exchange over internet
  - VPN tunnel
  - IPSec
  - 👎🏻 on path attacks
  - 👎🏻 person-in-the-middle attacks

- **RSA**

  - key exchange= key distribution
  - Encryption
  - Digital Signature
  - Prime numbers
  - Trapdoor function

- **ECC**: Ellipic Curve Cryptography

  - modible device
  - require less processing power
  - more efficient that RSA

### 1️⃣ Encrypt: public key, decrypt: private key

<img width="676" alt="Screenshot 2024-08-21 at 10 34 10" src="https://github.com/user-attachments/assets/9a4981e0-1047-42b0-bffd-cef2c4985a3c">

- public key: encrypt
  - shared with everyone
- private key: decrypt
  - only host can have the key

### 2️⃣ Encrypt: private key, decrypt: public key

<img width="632" alt="Screenshot 2024-08-21 at 10 36 33" src="https://github.com/user-attachments/assets/b160c376-dd07-4ec0-bed9-16e04059da4a">

- public key: decrypt
  - shared with everyone
- private key: encrypt

  - only host can have the key

- **Digital Signature**: used to verify oneself
  - that it is me who encrypted this file(who made the signature)
- everyone with `public key` can verify that it is you who signed the file

## ✅ Hybrid Encryption

1. A creates `symmetric key` <br>
2. A encrypts and sends `symmetric key` with B’s `public key` <br>
3. B recieves `symmetric key` and decrypts with B’s `private key` <br>
4. B sends message encrypted with A’s `public key` <br>
5. A recieves and decrypts with A’s `private key` <br>
6. Now A and B can communicate using the `symmetric key` <br>

## ✅ Digital Signature

<img width="861" alt="Screenshot 2024-08-21 at 10 57 58" src="https://github.com/user-attachments/assets/4089b670-9d92-4127-9765-9492d9cddadb">

- Digital Signature is consisted of three algorithm steps
- Key Creation Algorithm `G`: create `public, private key pair` of host
- Signature Creation Algorithm `S`: `message m` and `private key` to create `signature σ`
- Verify Signature Algorithm `V`: use `message m`, `public key`, `signature σ` to verify host

- 👍🏻 can verify the host who wrote the message
- 👍🏻 can function like a signature of the host
- 👍🏻 non-repudiation
- 👍🏻 operate against forgery
- 👍🏻 data integrity(checksum will be different)

#### ☑️ Digital Signature Algorithm

- DSA: Digital Security Algorithrm
- RSA
