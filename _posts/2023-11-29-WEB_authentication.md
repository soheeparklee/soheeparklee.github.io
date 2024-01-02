---
title: JWT, AccessToken, RefreshToken
categories: [WEB, Authentication]
tags: [jwt, session, localstorage, cookie, accesstoken, refreshtoken] # TAG names should always be lowercase
---

### 유저 인증 Authentication

#### Session

- session: 유저의 정보를 DB에 저장해두었다가 그떄그떄 가져와 쓰는 방식

#### JSON Web Token

- JWT: 토큰에 base 64로 인코딩해 두었다가 사용
  토큰을 조회하면 사용자의 정보를 모두 알 수 있음
  확장성이 좋다.
  보안성은 refresh token으로 높일 수 있다. (일정 시간 지나면 refresh token 전송)

### **JWT**: JSON Web Token

사용자 인증과 권한 부여를 위해 사용  
토큰에는 사용자의 인증 정보가 포함되어 있어 DB조회할 필요❌  
서버와 클라이언트 간 데이터를 주고받을 때 토큰을 사용해 사용자를 인증

### **JWT 인증 과정**

#### ☑️ SIGNUP

클라이언트가 자신의 정보(이름, 이메일, 아이디, 비밀번호)를 입력  
이 정보는 데이터 베이스에 저장되고,  
비밀번호는 단방향함수 hash(sha256)를 이용해 해시화하여 저장, 보안성⬆️

#### ☑️ LOGIN

클라이언트가 아이디, 비밀번호를 입력  
서버는 클라이언트가 입력한 아이디, 비밀번호를 가진 유저가 있는지 DB를 조회  
일치하는 유저가 있으면 ➡️ access token발급  
access token에는 사용자의 고유 정보(아이디, 이름)와 서버의 비밀키를 이용해 만들어짐  
클라이언트에게 전송, cash, local storage, session storage에 저장

#### 🔑 JWT

JWT 은 HTTP의 header에 포함되어 전송됨
클라이언트가 서버에 요청을 보낼 때마다 JWT 은 HTTP의 header에 포함되어 전송  
서버는 stateless하기 떄문에 유저가 누구인지 모르는데, JWT을 가지고 있으면 매번 확인하는 작업을 건너 뛸 수 있음  
JWT가 사용자의 인증과 권한 부여를 안전하고 효율적으로 처리

### 💟 **Access token**

인증 후 서비스를 사용할 수 있도록 발급되는 token <br>
HTTP의 header에 포함되어 전송됨 <br>
API에 요청을 보낼 때 사용 <br>
Access token을 이용해 사용자 인증 및 권한 확인 <br>
Access token에는 클라이언트의 아이디, 유효 기간, 권한 등이 포함되어 있음. <br>
<br>
Access token의 유효기간은 짧음. <br>
노출되었을 때 위험을 최소화하기 위해서 <br>

### 💟 **Refresh token**

Access Token이 만료되었을 때, 새로운 Access Token을 발급받기 위한 토큰 <br>
그래서 Refresh token을 사용하면 다시 로그인하지 않고 Access Token을 발급 가능 <br>
<br>
access token이 탈취되면 보안 위협이 생길 수 있음!! <br>
이를 보완하기 위한 수단으로 생긴 것이 바로 **Refresh token** <br>
<br>
Refresh token의 유효기간은 긴 편, 그 이유는 사용자 편의 <br>
그러나 Refresh token이 노출되면 보안 위협이 있으므로 안전하게 보관하는 것이 중요! <br>

#### 1️⃣ Refresh Token 발급

사용자가 처음 인증에 성공하면,  
access token과 함께 Refresh Token도 발급  
Refresh Token은 만료 시간을 가지며, access token을 재발급받는데 사용

#### 2️⃣ Refresh Token 저장

DB에 Refresh Token과 사용자 ID를 저장하는 테이블 생성해 DB에 저장

#### 3️⃣ Access Token 재발급 엔드포인트 생성

Access Token이 만료되었을 때, 이를 새로 발급받을 수 있는 엔드포인트를 생성  
클라이언트는 이 엔드포인트에 Refresh Token을 전달  
서버는 Refresh Token이 유효한지 확인한 후 새로운 Access Token을 발급

#### 4️⃣ Refresh Token 검증

Access Token 재발급 요청이 들어오면, Refresh Token이 유효한지 검증해야 함.  
이를 위해 아까 Refresh Token 저장해 둔 DB에서 Refresh Token 찾고  
Refresh Token이 만료되지는 않았는지 확인함.  
유효하다면, Access Token 재발급

#### 5️⃣ 로그아웃 로직 변경

사용자가 로그아웃하면, 발급된 Refresh Token도 폐기  
이를 위해 로그아웃 요청이 들어오면 DB에서 Refresh Token을 삭제하거나 만료시킨다.
