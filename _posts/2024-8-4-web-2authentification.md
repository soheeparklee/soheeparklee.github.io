---
title: Authentification progression
categories: [Computer Science, WEB]
tags: [] # TAG names should always be lowercase
---

## ✅ API key

1. User issues API key <br>
2. To use certain API, send key with request <br>
3. When requested, Application authenticated user information with key <br>
4. Respond to user with information from key <br>

#### 👎🏻

- If key is leaked? Difficult to fix <br>
- To prevent key leak, frequent update neccessary <br>

## ✅ OAUTH2

1. Application sends user to Oauth service to login <br>
2. Oauth authenticates user <br>

#### 👎🏻

- need to verify token
- token expires

## ✅ JWT

JWT carries verification with itself, so no need for requesting for verification of the token

#### 👎🏻

- token carries lots of sensitive data <br>
