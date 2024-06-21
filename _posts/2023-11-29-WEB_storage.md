---
title: Local storage, Session Storage, Cookie
categories: [Computer Science, WEB]
tags: [jwt, session, localstorage, cookie, accesstoken, refreshtoken] # TAG names should always be lowercase
---

### 📥 Local storage VS Session Storage

#### 📫 Local storage

1. Lifespan: 영구적인 저장소 <br>
   사용자가 의도적으로 데이터를 삭제하거나 브라우저 캐시를 지우지 않는 이상 영구적으로 보관
   로그아웃 후에도 데이터 남아 있음 <br>
2. Scope: 도메인 별로 저장 <br>
   도메인별로 저장되며, 동일한 도메인에서만 데이터 접근 가능 <br>
   shared across all tabs/windows from the same orgin(same protocoal, domain, port) <br>
   accessible in another tab/window from the same orgin <br>v
3. Storage Limit: 용량 <br>
   대부분 브라우저 Local storage 용량은 5~10MB <br>

#### 📭 Session Storage

1. Lifespan: 일시적인 저장소 <br>
   브라우저의 탭, 창을 닫으면 자동으로 데이터 삭제 <br>
   일시적인 데이터 저장에 적합 <br>
2. Scope: 탭별로 저장, page session <br>
   각 브라우저 탭별로 저장 <br>
   each brower tab or window has its own session storage and is not accessible in another tab/window <br>
3. Storage Limit: 용량 <br>
   대부분 브라우저 Session storage 용량 마찬가지로 5~10MB <br>

### 🍪 cookie

#### 1️⃣ 서버에서 쿠키 설정

서버에서 사용자가 인증이 되면, JWT 토큰을 생성하고 이를 쿠키에 저장 <br>
`token = jwt.encode({"user_id": user_id}, SECRET_KEY, algorithm="SH256")`<br>
쿠키도 마찬가지로 HTTP 응답 헤더에 Set-Cookie를 설정하여 토큰을 전달 <br>
`response.set_cookie()` <br>
`response.set_cookie(key="access_token", value=token)  <br>
`

#### 2️⃣ 클라이언트에서 쿠키 사용

클라이언트에서는 서버로부터 받은 쿠키를 사용하여 토큰을 저장 <br>
쿠키는 브라우저에 의해 자동으로 저장 <br>
서버로 요청을 보낼 때마다 쿠키가 자동으로 포함 <br>

#### 3️⃣ 서버에서 쿠키 읽기

서버에서는 클라이언트로부터 받은 요청의 쿠키를 확인하여 JWT 토큰을 추출하고 인증 <br>
`Request` <br>
`async def get_token(request: Request): return request.cookies.get("access_token")` <br>

#### 💡 주의!

단, 쿠키를 사용할 때 HttpOnly와 Secure 플래그를 설정하여 쿠키의 보안을 강화해야 한다. <br>

```python
from fastapi import FastAPI, Response, Request, Depends
import jwt

app = FastAPI()

@app.post("/login")
async def login(response: Response):
    # 사용자 인증 로직
    # ...

    # JWT 토큰 생성
    token = jwt.encode({"user_id": user_id}, SECRET_KEY, algorithm="SH256")

    # 응답 헤더에 쿠키 설정
    response.set_cookie(key="access_token", value=token)
    return {"message": "로그인 성공"}

async def get_token(request: Request):
    return request.cookies.get("access_token")

@app.get("/protected")
async def protected_route(token: str = Depends(get_token)):
    # 토큰 검증 및 인증 로직
    # ...

```
