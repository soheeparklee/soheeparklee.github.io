---
title: CarrotMkt Clone Coding_LogIn
categories: [Project, Carrot MKT Clone Coding]
tags: [clonecoding, project, html, css, javascript, password]
---

> 회원가입 정보를 DB에 저장해두었다가
> 사용자가 login하면 id, password를 DB에 조회하여 일치하면
> access token을 발급해서 사용자에게 내려준다.

> login은 POST이다

## ✅ **HTML**:

form형식으로 ID, password1 입력받는 형식 만들기
`submit` BTN이 있어야 함.
만든 form에 방식을 추가해줘야 함.

```html
<form id="login-form" action="/login" method="POST"></form>
```

## ✅ **BE(PYTHON)**

사용자가 login을 했을 떄, DB에 있는 사용자 정보와 비교한 다음  
같은 ID, pawword를 가진 사용자가 있고 일치하면 access token을 발급해 주어야 한다.

### ✨ fastapi의 library인 loginManager 불러오기

`from fastapi_login import LoginManager`

#### SECRET을 정해주어야 함

secret이 내가 access token을 어떻게 encoding할지 정하는 방법이다.  
이 secret이 노출되면 나의 JVM이 decoding될 수 있기 떄문에 노출되지 않도록 조심해야 함!  
`LoginManager(SECRET, "/token이 발급될 경로")`

```python
SECRET= "soheetheprogrammer"
manager= LoginManager(SECRET, "/login")
```

### ✨ def query_user

같은 ID, pawword를 가진 사용자가 DB에 있는지 확인하는 함수

#### login manager에서 key를 조회하기 떄문에 @manager 불러와야 함

```python
@manager.user_loader()
def query_user(id):
```

#### sql문으로 DB에서 아이디 일치하는 user 찾기

return **user**

```sql
        user= cur.execute(f"""
            Select * from users WHERE id= "{id}"
            """).fetchone()
        return user
```

#### ☑️ code

```python
@manager.user_loader()
def query_user(id):
        user= cur.execute(f"""
            Select * from users WHERE id= "{id}"
            """).fetchone()
        return user
```

### ✨ def login POST

#### post 하는 기본 함수

```python
# POST user (Login)
@app.post("/login")
def login(id: Annotated[str, Form()],
          password: Annotated[str, Form()]
          ):
```

#### 앞선 query_user에서 받아온 user

```python
     user= query_user(id)
     print(user)
     return "200"
```

#### ☑️ code

```python
@app.post("/login")
def login(id: Annotated[str, Form()],
          password: Annotated[str, Form()]
          ):
     user= query_user(id)
     print(user)
     return "200"
```

#### 로그인 시켜줘도 될까? 조건문

> user id가 DB에 있는가?
>
> > 없다면, `raise InvalidCredentialsException`
> > id가 있더라도, password가 일치하는가?
> > 없다면, `raise InvalidCredentialsException`

#### ☑️ code

```python

```

## ✅ **FE(JS)**: submit BTN이 눌렸을 떄 작동하는 함수
