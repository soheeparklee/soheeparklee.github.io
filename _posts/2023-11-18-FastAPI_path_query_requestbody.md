---
title: Path, Query, RequestBody
categories: [WEB, API]
tags: [backend, requestbody, fastapi, path, query] # TAG names should always be lowercase
---

## ✅ PATH

어떤 리소스를 식별하고 싶으면 path  
user중에서 123번 아이디를 가진 user를 보내주세요  
딱 1명

```python
/users/123
```

## ✅ QUERY

정렬이나 필터링  
user중에 20살인 user가 있을 수도 있고, 없을 수도 있으며, 여러명일 수도 있음.

```python
/users?age=20
```

## ✅ PATH VS QUERY

### PATH

```python
fruits= ["apple", "banana", "grape"]

@app.get("/fruits")
def read_fruit():
    return fruit

```

과일 중에서 특정 아이디를 가지는 과일 return  
아이디는 int여야 하므로 int로 감싸준다.

```python
@app.get("/fruits/{id}")
def read_path_fruit(id):
    return fruit[int id]
```

fruit[0] 이면 apple

### QUERY

skip없이 10개까지 배열에서 뽑아내세요

```python
@app.get("/fruits")
def read_query_fruit(skip:int=0, limit:int=10):
    return fruit[skip:skip+limit]
```

## ✅ Request Body

get(어떤 값을 조회할 때) 요청 ❌
post(서버에 업로드) ⭕️
body에 담아서 서버로 보낸다. 그래서 class라는 형식을 꼭 지켜야 한다.

### 사용하기 위해서

`from pydantic import BaseModel`
먼저 class를 지정해주어야 한다. 그리고 딱 이 형식대로만 데이터를 받아올 수 있음

```python
class Fruit(BaseModel):
    id: int
    content: str
```

### 형식

```python
@app.post("/fruits")
def post_fruit(fruit:Fruit):
    fruits.append(fruit.content)
    return 성공했습니다.
```

이제 알겠다!!!  
`fruit:Fruit):` 의 저 뒤 Fruit는 앞서 지정해 준 class이름이었던 것이다!!!!!

### 내가 쉽게 설명함.

```python
@app.post("/FE에서 받아올 경로 이름 fruits")
def post_fruit(FE에서 받아온 값fruit:class이름Fruit):
    배열 이름fruits.append(FE에서 받아온 값 fruit.content)
    return 성공했습니다.
```
