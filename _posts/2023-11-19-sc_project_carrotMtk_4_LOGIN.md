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

#### sql문으로 DB에서 column명 가져오기

그리고 `cur=con.cursor();`으로 위치 업데이트

```python
        con.row_factory= sqlite3.Row
        cur=con.cursor();
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
        con.row_factory= sqlite3.Row
        cur=con.cursor();
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
@app.post("/login")
def login(id: Annotated[str, Form()],
          password: Annotated[str, Form()]
          ):
     user= query_user(id)
     print(user)
     if not user:
          raise InvalidCredentialsException
     elif password != user["password"]:
          raise InvalidCredentialsException
     return "200"
```

## ✅ **FE(JS)**: submit BTN이 눌렸을 떄 작동하는 함수

기본적으로 signIN함수랑 비슷함.  
post 하는 함수는 이렇게 생겼었음.  
(data를 BE에서 받아와 json값으로 바꿔 data가 200이면 ~한다. )

```javascript
const res = await fetch("/login", {
  method: "post",
  body: formData
});

const data = await res.json();
if (data === "200") {
  alert("successfully logged in! Now you can write");
  window.location.pathname = "/write.html";
}
```

#### 그런데 res의 status를 바로 받아볼 수도 있음.

```javascript
if (res.status === 200) {
  alert("successfully logged in! Now you can write");
  window.location.pathname = "/write.html";
} else if (res.status === 401) {
  alert("login failed. Check your ID or password again!");
}
```

#### ☑️ code

```javascript
const form = document.querySelector("#login-form");

async function handleSubmit(event) {
  event.preventDefault();
  const formData = new FormData(form);

  const sha256password = sha256(formData.get("password"));
  formData.set("password", sha256password);

  const res = await fetch("/login", {
    method: "post",
    body: formData
  });
  const data = await res.json();

  if (res.status === 200) {
    alert("successfully logged in! Now you can write");
    window.location.pathname = "/write.html";
  } else if (res.status === 401) {
    alert("login failed. Check your ID or password again!");
  }
}

form.addEventListener("submit", handleSubmit);
```

어쨌든 이대로 안할거임. 왜냐하면 우리는 accesstoken을 받을거니까!

### ✅ **BE**: access token

만약 session방식이라면, DB를 조회해서 user의 정보를 가져와야 함.  
session에는 아무런 정보가 없음.  
access token은 DB를 조회할 필요가 없음!  
왜냐하면 access token안에 user의 정보가 모두 들어있기 떄문! 😁  
그래서 처음 한 번만 조회하면, 그 뒤에는 DB를 조회할 필요가 없음.

#### access token 발급

access token은 login manager이 발급해준다.  
token방식은 token안에 있는 정보를 가져오기 때문에 data={}값을 받아올 수 있다.

```python
access_token= manager.create_access_token(data=  {어떤 데이터 받을거야???})
```

#### access token안에 login정보 넣고 access token을 return 하도록

sub안에다가 객체를 만들어 id, name, email을 access token에 넣는다.

```python
# access token안에 login정보 넣고
access_token= manager.create_access_token(data= {
        "sub": {
                "id": user["id"],
                "name": user["name"],
                "email": user["email"]
                }
    })
# access token을 return 하도록
    return {"access_token": access_token}
```

### ✅ **FE**: access token

#### access token을 저장

access token이 없으면 401error을 내려주는 기능  
**stateless** 서버는 frontend랑 한번 연결(요청, 접속)이 된 후 연결을 끊어버린다.  
내가 누구인지 알려주기 위해 access token을 보내준다.  
이 access token은 header에 넣어서 보내야 한다.
그러면 서버는 header에 담긴 access token을 보고 내가 누구인지 알 수 있다.

그러면 FE에서는 access token을 받아 저장

#### access token을 어디에 저장할 수 있을까?

##### 쿠키

서버로 요청을 보낼 때 자동으로 전송되는 작은 데이터 파일  
자동으로 가다보니 보안이 취약할 수 있지만, XSS, CSRF등으로 공격을 방지할 수 있다.

##### local storage

브라우저 내부에 있는 저장소로, 클라이언트 측에서도 조정이 가능! 우리가 여기에 무언가를 저장할 수 있다는 말.  
로컬 스토리지에 접근해 삭제, 저장할 수 있음.

##### session storage

local storage와 마찬가지로 브라우저 내부에 있는 저장소이지만,  
브라우저가 닫히면 초기화된다.
브라우저 닫았다 열었을 때마다 로그인하라고 하고 싶으면 session storage쓰면 된다.

```javascript
const data = await res.json();
const accessToken = data.access_token;
window.localStorage.setItem("token", accessToken);
alert("login succeeded with token");
```

### ✅ **BE**: access token있을 떄만 get_items함수 실행할래

access token 추가, 인증되어야지만 아래 명령(get_items함수) 보내줄거야
아주아주 오래전에 만들었던 함수 `get_items`에다가 `user= Depends(manager)`를 parameter로 준다
그러면 서버에서는 유저가 인증되어야만 `get_items`함수 실행하고, 인증 안 되면 401error

FE에는 access token을 let으로 저장해두었다가 받아오기

```python
@app.get("/items")

async def get_items(user= Depends(manager)):
```

### ✅ **FE**: accessToken있으니까 버튼 누르면 item보여줘

#### 서버와 계속 연결 유지하기 위해 header안에 access token넣기

- BE에서 accessToken발급받고 유저인증 받은 다음,
- FE에서 `handleSubmit`함수 실행
- 함수 내에서 버튼 만들어
- 이 버튼 누르면 아이템 fetch 할 수 있도록 ` const res= await fetch ("/items",`
- 근데 서버와 계속 연결을 유지해야하므로
- header안에 access token을 넣는다. `headers:{Authorization: `Bearer ${accessToken}`, },`
- 만얃 header안에 access token이 없으면, item들이 보이지 않을 것이다.

```javascript
const infoDiv = document.querySelector("#info");
infoDiv.innerText = "login succeed";

const btn = document.createElement("button");
btn.innerText = "get item";
btn.addEventListener("click", async () => {
  const res = await fetch("/items", {
    //add access token to header
    headers: {
      Authorization: `Bearer ${accessToken}`
    }
  });
  const data = await res.json();
  console.log(data);
});
infoDiv.appendChild(btn);
```

### ✅ **BE**: login manager에서 id를 DB에서 찾아오는 방식을 바꿔야 함.

data가 dict(객체)형태로 넘어오기 때문에 `WHERE_STATEMENT` 사용해서 id찾아야 한다.  
dict란 `login`함수에서 쓴 다음과 같은 형식을 말한다.

```python
    access_token= manager.create_access_token(data= {
        "sub": {
                "id": user["id"],
                "name": user["name"],
                "email": user["email"]
                }
    })
```

```python
@manager.user_loader()
def query_user(data):
        WHERE_STATEMENT= f'id="{data}"'
        if type(data) ==dict:
                WHERE_STATEMENT= f'name="{data["name"]}"'

        con.row_factory= sqlite3.Row
        cur=con.cursor();
        user= cur.execute(f"""
            Select * from users WHERE {WHERE_STATEMENT}
            """).fetchone()
        return user
```

### ✅ **FE**: accessToken있으면 root페이지로 이동

#### `index.js`파일의 `fetchList`함수

> res.status가 401이라면
>
> > 로그인 하세요! 로그인 페이지로 이동시키기

```javascript
async function fetchList() {
  const res = await fetch("/items");
  const data = await res.json();
  if (res.status === 401) {
    window.location.pathname = "/login.html";
  }

  renderData(data);
}
fetchList();
```

#### accessToken 받아오기

```javascript
const accessToken = window.localStorage.getItem("token");
```

그리고 그걸 header안에 넣어야

```javascript
const res = await fetch("/items", {
  headers: {
    Authorizaiton: `Bearer ${accessToken}`
  }
});
```

#### ☑️ CODE

```javascript
async function fetchList() {
  const accessToken = window.localStorage.getItem("token");

  const res = await fetch("/items", {
    headers: {
      Authorization: `Bearer ${accessToken}`
    }
  });

  if (res.status === 401) {
    alert("로그인이 필요합니다!");
    window.location.pathname = "/login.html";
    return;
  }
  const data = await res.json();
  renderData(data);
}
fetchList();
```

### ✅ **BE**: backend에도 "accessToken있을 때만"이라는 조건 주기

#### `python`파일의 `get_items`함수에다가 조건 주어야 한다.

```python
#GET item
@app.get("/items")

async def get_items(user= Depends(manager)):
```

### ✅ **FE**: final code of login.js

```javascript
const form = document.querySelector("#login-form");

async function handleSubmit(event) {
  event.preventDefault();
  const formData = new FormData(form);
  const sha256Password = sha256(formData.get("password"));
  formData.set("password", sha256Password);

  const res = await fetch("/login", {
    method: "post",
    body: formData
  });
  const data = await res.json();
  const accessToken = data.access_token;
  console.log(accessToken);
  if (accessToken) {
    window.localStorage.setItem("token", accessToken);
    window.location.pathname = "/";
  }

  if (res.status === 200) {
    alert("successfully logged in! Sending you to main page...");
    window.location.pathname = "/";
  } else {
    alert("login failed. Check your ID or password again!");
    window.location.pathname = "/login.html";
  }
}

form.addEventListener("submit", handleSubmit);
```

### 💟 파이썬 hashlib

백엔드에서도 비밀번호 저장 전 암호화

```python
import hashlib

def hash_password(password):
    return hashlib.sha256(password.encode()).hexdigest()
```
