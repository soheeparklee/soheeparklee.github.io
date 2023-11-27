---
title: CarrotMkt Clone Coding_SignUp(POST, password sha256)
categories: [Project, Carrot MKT Clone Coding]
tags: [clonecoding, project, html, css, javascript, password]
---

## ✅ **HTML**:

form형식으로 ID, password1, password2, name, email 입력받는 form 형식 만들기  
`submit` BTN이 있어야 함.

```html
<form id="signup-form" action="/signup" method="POST"></form>
```

## ✅ **FE(JS)**: client data POST

### ✨ function handleSubmit()

- submit BTN이 눌렸을 떄 작동하는 함수

#### `preventDefault` 통해서 event 받아온 후 page reload ❌

```javascript
const handleSubmit = async (event) => {
  event.preventDefault();
};

form.addEventListener("submit", handleSubmit);
```

#### `formdata`형식으로 받을거임

`new FormData(from)` 안에 들어있는 form은 위에서 정의한 HTML에서 불러온 form  
`const form= document.querySelector("#signup-form")`

```javascript
const formData = new FormData(form);
```

#### POST 하는 형식

```javascript
const res = await fetch("/signup", {
  method: "post",
  body: formData
});
```

### 🔑 hash 함수: sha256 function

이 함수를 사용하면 비밀번호를 암호화해준다.  
client의 비밀번호를 알 수 없는 숫자, 문자들로 만들어 줌.  
sha256은 일방향 함수라서 암호화 된 숫자, 문자들을 다시 비밀번호로 바꿀 수는 없음.

#### formdata로 받아온 password를 `get`하여 sha256함수로 감싸준다.

`formData.get("password")`
그리고 바꾼 password를 `set`해서 저장

```javascript
//change form data password using sha256
//formdata의 get써서 password가져온 다음에, sha256 사용해서 암호화
const sha256Password = sha256(formData.get("password"));
formData.set("password", sha256Password);
```

### ✨ function checkPassword()

password 1 === pasword2 check function  
함수 `checkPassword`를 함수 `handleSubmit`안에 넣어 `submit`BTN이 눌렸을 때 함수 `checkPassword`가 실행되도록 할 것임.

#### 두 개의 비빌번호끼리 일치하는지 확인하는 함수

```javascript
//double check password
const checkPassword = () => {
  const formData = new FormData(form);
  const password1 = formData.get("password");
  const password2 = formData.get("password2");
  if (password1 === password2) {
    return true;
  } else return false;
};
```

#### 두 비밀번호가 일치하지 않았을 떄 보여지는 div

어디에 만들어야 할까? handleSubmit함수 안에

```javascript
//password 일치하지 않았을 때 보여지는 div
const div = document.querySelector("#passwordCheck");
```

### 💡 마지막으로, if문

- if문을 만들어 `checkpassword`함수가 true이면
  > 이 정보를 db에 업로드  
  > res를 json형식으로 만들기 `const data= await res.json();`
  - if db에 정보가 업로드 잘 되면, (return 200)
    > > 로그인 페이지로 가도록 pathname 설정 `window.location.pathname= "/login.html"`
- else, `checkpassword`함수가 false이면
  > password 일치하지 않았을 때 보여지는 div보이도록 하기

```javascript
if (checkPassword()) {
  const data = await res.json();
  if (data === "200") {
    alert("succeed in sign in, now you can log in");
    window.location.pathname = "/login.html";
  }
} else {
  div.innerText = "두 비밀번호가 일치하지 않습니다. ";
}
```

## ☑️ FE JS code

```javascript
const form = document.querySelector("#signup-form");

//double check password
const checkPassword = () => {
  const formData = new FormData(form);
  const password1 = formData.get("password");
  const password2 = formData.get("password2");
  if (password1 === password2) {
    return true;
  } else return false;
};

const handleSubmit = async (event) => {
  event.preventDefault();
  const formData = new FormData(form);
  //change form data password using sha256
  //formdata의 get써서 password가져온 다음에, sha256 사용해서 암호화
  const sha256Password = sha256(formData.get("password"));
  formData.set("password", sha256Password);

  //password 일치하지 않았을 때 보여지는 div
  const div = document.querySelector("#passwordCheck");

  //check password
  if (checkPassword()) {
    //POST on server
    const res = await fetch("/signup", {
      method: "post",
      body: formData
    });
    const data = await res.json();
    if (data === "200") {
      alert("succeed in sign in, now you can log in");
      window.location.pathname = "/login.html";
    }
  } else {
    div.innerText = "두 비밀번호가 일치하지 않습니다. ";
  }
};

form.addEventListener("submit", handleSubmit);
```

## ✅ **BE(PYTHON)**

### @app.post

```python
    @app.post("/signup")
def signup(id: Annotated[str, Form()],
            password: Annotated[str, Form()],
            name: Annotated[str, Form()],
            email: Annotated[str,Form()]
            ):
```

### DB에 signUp한 사용자 정보 저장

#### SQLITE 문법

```sql
    cur.execute(f"""
                    INSERT INTO users(id, name, email, password)
                    VALUES('{id}', '{name}', '{email}', '{password}')
                    """)
    con.commit()
```

## ☑️ BE code

```python
#signup page
@app.post("/signup")
def signup(id: Annotated[str, Form()],
            password: Annotated[str, Form()],
            name: Annotated[str, Form()],
            email: Annotated[str,Form()]
            ):
    cur.execute(f"""
                    INSERT INTO users(id, name, email, password)
                    VALUES('{id}', '{name}', '{email}', '{password}')
                    """)
    con.commit()
    return "200"
```
