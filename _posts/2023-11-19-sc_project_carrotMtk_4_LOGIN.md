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

## ✅ **BE(PYTHON)**

사용자가 login을 했을 떄, DB에 있는 사용자 정보와 비교한 다음  
같은 ID, pawword를 가진 사용자가 있고 일치하면 access token을 발급해 주어야 한다.

### fastapi의 library인 loginManager 불러오기

#### SECRET을 정해주어야 함

이 secret이 노출되면 나의 JVM이 decoding될 수 있기 떄문에 노출되지 않도록 조심해야 함!

```python
SECRET= "soheetheprogrammer"
manager= LoginManager(SECRET, "/login")
```

### SQLITE 문법

```sql

```

## ☑️ BE code

```python

```

## ✅ **FE(JS)**: submit BTN이 눌렸을 떄 작동하는 함수
