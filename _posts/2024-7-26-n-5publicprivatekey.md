---
title: Symmetric Key, Asymmetric Key
categories: [Computer Science, Network]
tags: [] # TAG names should always be lowercase
---

## ✅ Symmetric Key

> same key for encryption, decryption

👍🏻 fast <br>
👎🏻 easy to decrypt <br>

## ✅ Asymmetric Key

1. A sends message **encrypted** with **B's public key** <br>
2. B recieves and **decrypts** with **B's private key** <br>
3. B sends message **encrypted** with **A's public key** <br>
4. A recieves and **decrypts** with **A's private key** <br>

## ✅ Hybrid Encryption

1. A creates `symmetric key` <br>
2. A encrypts and sends `symmetric key` with **B's public key** <br>
3. B recives `symmetric key` and **decrypts** with **B's private key** <br>
4. B sends message **encrypted** with **A's public key** <br>
5. A recieves and **decrypts** with `symmetric key` <br>
6. Now A and B can communicate using the `symmetric key` <br>
