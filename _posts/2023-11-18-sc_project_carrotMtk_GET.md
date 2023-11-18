---
title: CarrotMkt Clone Coding_GET
categories: [Project, Clone Coding]
tags: [clonecoding, project, html, css, javascript, frontend]
---

## ✅ **FE(JS)**:`GET`해서 가지고 온 정보를 frontend에 보이게 하기

### 각 아이템들 `array`로 받아올 것

#### array를 빙글빙글 돌면서 각각에 대해 실행

`for each()`

#### 가장 최근에 쓴 게시물이 위에 보이게 하기

`reverse()`  
`data.reverse().forEach(async(obj) => { 어쩌고 어쩌고`

### 함수의 `parameter`을 `obj`로 해서 `obj`의 title, price 등 받아오기

```javascript
descTitle.innerText = obj.title;
descMeta.innerText = obj.place + " " + calcTime(obj.insertat);
descPrice.innerText = obj.price;
```

### 사진 불러오는 척

사진은 특별하다 왜냐하면 사진은 커서 불러오는데 시간이 걸리니까  
그리고 blob도 다시 그림으로 바꿔줘야 한다.

    ```javascript
    const res= await fetch(`/images/${obj.id}`)
    const blob= await res.blob();
    const url= URL.createObjectURL(blob);
    ```

### 받아온 정보 HTML에 `append` 하면서 HTML div 순서 정해주기

### ☑️ 여기까지 한 code

```javascript
    const renderData= (data) =>{
    //여기서 data가 array임
    //배열 내부의 값을 하나씩 돌면서 다음 명령을 수행 => for each
    // 가장 처음 올린 것이 밑으로, 마지막에 올린 것이 위로 => reverse
    //함수의 `parameter`을 `obj`로 해서 `obj`의 title, price 등 받아오기
    data.reverse().forEach(async(obj) => {
        //함수의 `parameter`을 `obj`로 해서 `obj`의 title, price 등 받아오기
        //받아온 정보 HTML에 div만들고 `append` 하면서 HTML div 순서 정해주기
        });


```

## ✅ **FE(JS)** '몇 초/분/시간 전' 시간 보이기

#### 지금 시간 가져오기 `new Date().getTime()`

지금 시간 **빼기** 백엔드에서 받아온 게시물 입력한 시간

```javascript
const curTime = new Date().getTime();
const time = new Date(curTime - timestamp);
```

#### UTC 시간 한국 시간으로 바꾸기 -9

`const curTime= new Date().getTime() -9*60*60*1000;`

### ☑️ 여기까지 한 code

```javascript
const calcTime = (timestamp) => {
  const curTime = new Date().getTime() - 9 * 60 * 60 * 1000;
  const time = new Date(curTime - timestamp);
  const hour = time.getHours();
  const min = time.getMinutes();
  const sec = time.getSeconds();

  if (hour > 0) return `${hour}시간 전`;
  else if (min > 0) return `${min}분 전`;
  else if (sec >= 0) return `${sec}초 전`;
  else return "방금 전";
};
```

## ✅ **BE(PYTHON)** GET 서버에서 정보 가져오자

### GET item정보

#### access token 추가, 인증되어야지만 아래 명령 보내줄거야

`async def get_items(user= Depends(manager)):`

#### SQLITE 문법으로 DB에 있는 정보 가져오기

```sql
    cur= con.cursor()
    rows= cur.execute(f"""
                    SELECT * from items;
                    """).fetchall()
```

#### JSON응답을 정리 => dict

`return JSONResponse(jsonable_encoder(dict(row) for row in rows))`

#### ☑️ 여기까지 한 code

```python
@app.get("/items")
# access token 추가, 인증되어야지만 아래 명령 보내줄거야
async def get_items(user= Depends(manager)):

    # SQLITE
    # bring column name(각 값들이 무엇을 의미하는지 알기 위해)
    con.row_factory= sqlite3.Row
    # bring data, in form of array
    cur= con.cursor()
    rows= cur.execute(f"""
                    SELECT * from items;
                    """).fetchall()
    # add (dict) to make response neatly organized
    return JSONResponse(jsonable_encoder(dict(row) for row in rows))
```

### GET item image

#### SQLITE 문법으로 DB에 있는 image 가져오기

```sql
    cur= con.cursor()
    rimage_bytes= cur.execute(f"""
                            SELECT image from items WHERE id= {item_id}
                            """).fetchone()[0]
```

#### 16진법을 우리가 보는 이미지로 바꾸기

`return Response(content= bytes.fromhex(image_bytes))`

#### ☑️ 여기까지 한 code

```python
@app.get("/images/{item_id}")
async def get_img(item_id):

    cur= con.cursor()
    image_bytes= cur.execute(f"""
                            SELECT image from items WHERE id= {item_id}
                            """).fetchone()[0]
    #change 16진법 to 우리가 보는 이미지
    return Response(content= bytes.fromhex(image_bytes))

```

```javascript

```

```python

```
