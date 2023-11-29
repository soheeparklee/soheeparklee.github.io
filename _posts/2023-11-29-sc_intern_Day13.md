---
title: 2023.SEPT.29(WED) 슈퍼코딩 부트캠프 신입연수원 Day 13
categories: [TIL(Today I Learned), SuperCoding_신입연수원(주특기 선택 이전)]
tags: [todayilearned, til, sessionstorage, localstorage, cookie]
---

## ✅ Daily Report

### 📌 **TO-DO LIST**

- [x] submit github blog post
- [x] 71강까지
- [x] assigment: Access Token VS Refresh Token
- [x] assigment: Local storage VS Session Storage
- [x] assigment: 액세스 토큰을 쿠키에 저장시키도록 로직을 변경
- [x] assigment: 채팅 탭에서 채팅을 보내고(POST) 받을(GET) 수 있는 기능을 API로 구현

## ✅ Today I Learned

### 📥 Local storage VS Session Storage

#### 📫 Local storage

#### 📭 Session Storage

### 🍪 cookie

#### 1️⃣ 서버에서 쿠키 설정

#### 2️⃣ 클라이언트에서 쿠키 사용

#### 3️⃣ 서버에서 쿠키 읽기

### 🔨 SVELTE(web framework)

#### web framework가 왜 필요한가?

### CommonJS 모듈

### 🔨 Bundler Vite

### createChat BE

```python
class Message(BaseModel):
    id: int
    content: str

messages= []

@app.post("/messages")
def create_message(message:Message):
    messages.append(message)
    return "messag created successfully"

@app.get("/messages")
def read_message():
    return messages
```

## ☑️ Summary of the Day <br>

I feel the need to organize my blog better!
