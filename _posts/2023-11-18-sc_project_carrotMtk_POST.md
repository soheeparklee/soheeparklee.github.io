---
title: CarrotMkt Clone Coding_POST
categories: [Project, Clone Coding]
tags:
  [clonecoding, project, html, css, javascript, frontend, fastapi, requestbody]
---

## ✅ Request Body

> When you need to send data from a client (let's say, a browser) to your API, you send it as a request body.

## ✅ **BE(PYTHON)** POST in backend

정보를 backend server에 올려두기

#### 1️⃣ HTML로 `form tag`그리고 안에 `input`을 만들어 user로부터 정보를 입력받는다.

- 이 때 database에 주었던 column명과 HTML의 title, id 일치하게

#### 2️⃣ 서버에 정보를 POST(업로드)

```python
@app.post('./경로')
    def 함수이름 (내가 받아오고 싶은 것):
```

```python
@app.post('./items')
    def create_item(image: UploadFile,
                    title: Annotated[str, Form()],
                    price: Annotated[int, Form()],
                    description: Annotated[str, Form()],
                    place: Annotated[str, Form()]
                    ):
```

## ✅ **FE(JS)** 받은 정보 FE에서 server로 전달

#### HTML에서 `submit`하면 JS에서 handleSubmit함수 실행

`form.addEventListener("submit", handleSubmit);`

`submit`이라는 이벤트는 제출 후 페이지를 reload
이를 방지하기 위해 `preventDefault()`

```javascript
event.preventDefault();
```

#### fetch

```javascript
const form = documet.getElementById("write-form");

const handleSubmit = async (evnet) => {
  event.preventDefault();
  const body = new FormData(form);
  await fetch("/itmes", {
    method: "POST",
    body: body
  });
};

form.addEventListener("submit", handleSubmit);
```

` const body= new FormData(form)`

- 여기서 `new FormData`는 JS 내장 객체
- POST의 body를 `FormData`로 묶어서 보낸다는 뜻
- form은 우리가 위에서 선언해 준 변수

## ✅ **BE(PYTHON)** SQL lite 연결하기

#### SQLITE settings

- 전체 문서에서 한 번만 하면 됨.

```python
con= sqlite3.connect("db.db", check_smae_thread= False)
cur= con.cursor()
```

## ✅ **BE(PYTHON)** 받은 정보 database에 저장 insert in database

#### 이미지(blob) 크기 떄문에 읽어올 시간 필요

```python
@app.post('./items')
    def create_item(image: UploadFile,
                    title: Annotated[str, Form()],
                    price: Annotated[int, Form()],
                    description: Annotated[str, Form()],
                    place: Annotated[str, Form()]
                    ):

    image_bytes= await image.read()
```

#### SQL문법을 사용해 BE에서 받아온 data를 SQLITE database에 `insert`

특히 이미지는 16진법으로 바꿔줌 주의!
`image_bytes.hex()`

```sql
    # 여기는 SQL문
    cur.execute(f"""
                INSERT INTO items(title, image, price, description, place, insertat)
                VALUES ("{title}", "{image_bytes.hex()}", {price}, "{description}", "{place}", {insertat})
    """)

    con.commit()
    print(image, title, price, description, place, insertat)
    return "200"
```

## ☑️ BE python code

```python
  @app.post("/items")
async def create_item(image:UploadFile,
                title: Annotated[str, Form()], #form형식으로 str으로 정보가 올 것이다.
                price: Annotated[int, Form()],
                description: Annotated[str, Form()],
                place: Annotated[str, Form()],
                insertat: Annotated[int, Form()]
                ):

    #image is very big, so time necessary to read
    image_bytes= await image.read()
    #insert in database
    #""""""is like backtick in js
    #hex는 16진법으로 바꿔주는 기능
    cur.execute(f"""
                INSERT INTO items(title, image, price, description, place, insertat)
                VALUES ("{title}", "{image_bytes.hex()}", {price}, "{description}", "{place}", {insertat})
                """)
    con.commit()

    print(image, title, price, description, place, insertat)
    return "200"
```

## ✅ **FE(JS)** backend의 응답 가져오기

방금 BE에서 `return "200"`했잖아

```javascript
    const data= await res.json();

if(data === "200")
    //응답이 200이면 다시 root로 돌리기
    window.location.pathname= "/";
    } catch (e){
        console.error(e);
```

## ☑️ FE JS code

```javascript
async function handleSubmitForm(event) {
  event.preventDefault();

  const body = new FormData(form);
  body.append("insertat", new Date().getTime());

  //try catch 구문 사용, try and if it doesnt work, e in catch
  try {
    //post item on server
    const res = await fetch("/items", {
      method: "POST",
      body: body
    });

    //to go back to root page after uploading item
    const data = await res.json();
    if (data === "200") window.location.pathname = "/login.html";
  } catch (e) {
    console.error(e);
  }

  console.log("submitted");
}

const form = document.getElementById("write-form");
form.addEventListener("submit", handleSubmitForm);
```
