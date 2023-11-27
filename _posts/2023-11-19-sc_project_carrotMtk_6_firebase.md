---
title: CarrotMkt Clone Coding_LogIn
categories: [Project, Carrot MKT Clone Coding]
tags: [clonecoding, project, html, css, javascript, password]
---

## ✅ **HTML**:

form형식으로 ID, password1 입력받는 형식 만들기  
`submit` BTN이 있어야 함.  
만든 form에 방식을 추가해줘야 함.

```html
<form id="login-form" action="/login" method="POST"></form>
```

## ✅ **BE(PYTHON)** login 정보 POST

### ✨ def login()

#### id, password 정보를 마찬가지로 form 형태로 넘겨받고

```python
@app.post("/login")
def login(id: Annotated[str, Form()],
            password: Annotated[str, Form()]
            ):
```

#### 로그인 해줄지 말지 조건문

> 유저의 id를 query_user()함수 확인했을 떄 없다면
>
> > 로그인 못함 raise InvalidCredentialsException
> > 유저의 비밀번호가 user["password"]와 일치하지 않는다면
> > 로그인 못함 raise InvalidCredentialsException

```python
user= query_user(id)
    print(user)
    #유저가 없으면 error메세지 보내라 = raise
    #elif password 틀리면 error raise
    if not user:
        raise InvalidCredentialsException
    elif password != user["password"]:
        raise InvalidCredentialsException
```

#### access token

유저의 정보를 서버에 저장해두기

```python
access_token= manager.create_access_token(data={
        "sub":{
            "id": user["id"],
        "name": user["name"],
        "email": user["email"]
        }
    })
    return {"access_token": access_token}

```

## ✅ **BE(PYTHON)** login 정보 GET

사용자가 login을 했을 떄, DB에 있는 사용자 정보와 비교한 다음  
같은 ID, pawword를 가진 사용자가 있고 일치하면 access token을 발급해 주어야 한다.

### ✨loginManager

fastapi의 library인 loginManager 불러오기  
@manager.user_loader() => user정보 가져오는 것이니 get

#### SECRET을 정해주어야 함

이 secret이 노출되면 나의 JVM이 decoding될 수 있기 떄문에 노출되지 않도록 조심해야 함!

```python
SECRET= "soheetheprogrammer"
manager= LoginManager(SECRET, "/login")

```

### ✨ def query_user():

FE에서 받아온 data가 id, name과 일치하면  
user정보 받아오기

```python
@manager.user_loader()
def query_user(data):
    WHERE_STATEMENT = f'id="{data}"'
    if type (data) == dict:
        WHERE_STATEMENT = f'name="{data["name"]}"'
```

#### SQLITE 문법 GET

```sql
con.row_factory= sqlite3.Row
    cur= con.cursor()
    user= cur.execute(f"""
                    SELECT * from users WHERE {WHERE_STATEMENT}
                    """).fetchone()
```

## ☑️ BE code

```python
@manager.user_loader()
def query_user(data):
    WHERE_STATEMENT = f'id="{data}"'
    if type (data) == dict:
        WHERE_STATEMENT = f'name="{data["name"]}"'

    con.row_factory= sqlite3.Row
    cur= con.cursor()
    user= cur.execute(f"""
                    SELECT * from users WHERE {WHERE_STATEMENT}
                    """).fetchone()
    return user
```

## ✅ **FE(JS)**: POST

### ✨ handleSubmit()

- HTML 에서 form 불러오기
- form에 addEventListener
- preventDefault()
- formData 형식으로 받을거임 `const formData= new FormData(form)`

```javascript
const form= document.querySelector("#login-form");

const handleSubmit= async (event) =>{
    event.preventDefault();
    const formData= new FormData(form);

    form.addEventListener("submit", handleSubmit);
```

#### sha256Password

formData 의 Password를 sha256Password로 바꾸어 저장

- get, set 사용

```javascript
const sha256Password = sha256(formData.get("password"));
formData.set("password", sha256Password);
```

#### fetch

```javascript
const res = await fetch("/login", {
  method: "post",
  body: formData
});
```

#### access token

```javascript
const data = await res.json();
const accessToken = data.acces_token;
window.localStorage.setItem("token", accessToken);
alert("login succeeded with access token");
```
