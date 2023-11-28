---
title: 2023.SEPT.28(TUE) 슈퍼코딩 부트캠프 신입연수원 Day 12
categories: [TIL(Today I Learned), SuperCoding_신입연수원(주특기 선택 이전)]
tags: [todayilearned, til]
---

## ✅ Daily Report

### 📌 **TO-DO LIST**

- [x] submit github blog post
- [x] 68
- [x] 69
- [x] 70
- [x] 71
- [x] assigment: JWT
- [x] assigment: JWT를 이용한 회원 가입과 로그인 과정에 대해 설명
- [x] assigment: hashlib
- [x] assigment: refresh token

## ✅ Today I Learned

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

## 🐛 Trouble Shooting

### **🔴 Trouble**

WHERE_STATEMENT in python, SQLite

#### **🟠 Mistakes I Made\_헷갈리거나 실수한 점**

여기서 WHERE_STATEMENT이 어려웠다.  
특히 `id="{data["id"]}"`부분을 잘못 입력해 한동안 오류에 시달렸다.

```python
@manager.user_loader()
def query_user(data):
        WHERE_STATEMENT= f'id="{data}"'
        if type(data) ==dict:
                WHERE_STATEMENT= f'''id="{data["id"]}"'''

        con.row_factory= sqlite3.Row
        cur=con.cursor()
        user= cur.execute(f"""
                Select * from users WHERE {WHERE_STATEMENT}
                """).fetchone()
        return user
```

## ☑️ Summary of the Day <br>

라이브 코딩을 듣지 않는대신, 강의에 집중하기로...
