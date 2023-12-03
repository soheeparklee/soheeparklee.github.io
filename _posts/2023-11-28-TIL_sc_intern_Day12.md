---
title: 2023.SEPT.28(TUE) 슈퍼코딩 부트캠프 신입연수원 Day 12
categories: [TIL(Today I Learned), SuperCoding_신입연수원(주특기 선택 이전)]
tags: [todayilearned, til, refreshtoken, accesstoken, jwt]
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

### **JWT 인증 과정**

### 💟 **Access token**

### 💟 **Refresh token**

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
