---
title: Memo App CRUD
categories: [Project, Memo]
tags: [project, crud]
---

## ✅ POST

### **☑️ FE: JS**:

### 📌 function handleSubmit

when clicked, call function `handleSubmit`  
submit automatically reloads page, so prevent reload default

```javascript
function handleSubmit(event) {
  //submit reloads page automatically, so prevent reload default
  event.preventDefault();
}
```

#### get input of the client

client input.value has to be `let`, as it will be changed

```javascript
const clientInput = document.querySelector(".memo_input");
let clientInputValue = clientInput.value;
```

#### get input value, then send it to createMemo function

and clear the input tag

```javascript
createMemo(clientInputValue);
clientInputValue = "";
```

### 📌 function createMemo

#### POST method

```javascript
body: JSON.stringify({
            id: new Date().getTime(),
            content: value;
        }),
```

값을 ``로 감싸줘야 한다.  
그 이유는 통신을 할 때는 문자열로만 할 수 있기 떄문이다.

### **CODE**

```javascript
async function createMemo(value) {
  //post on server
  const res = await fetch("/memos", {
    method: "POST",
    headers: {
      "Content-Type": "application/json"
    },
    body: JSON.stringify({
      id: new Date().getTime(),
      content: value
    })
  });
  const jsonRes = await res.json();
}
```

### **☑️ BE: PYTHON**

#### class 미리 설정해 두어야 한다.

아까 JS에서도 이렇게 정의해주기로 했음.

```python
class Memo(BaseModel):
    id: str
    content: str
```

#### array를 하나 만들어 안에 memo넣을 것임

```python
memos= []

@app.post("/memos")
def create_memo(memo):
    memos.append(memo)
    return "memo created successfully"
```

### 📌 def create_memo

#### @app.post("/memos")

memos라는 경로로 받을 건데, memo로 받을 거야.

### **CODE**

```python
class Memo(BaseModel):
    id: str
    content: str

memos= []

@app.post("/memos")
def create_memo(memo:Memo):
    memos.append(memo)
    return "memo created successfully"
```

## ✅ GET

### **☑️ FE: JS**:

### 📌 function readMemo

디폴트로 가는 건 GET요청
이 함수는 언제 실행되어야 할까?
(1) 페이지가 처음에 로딩되었을 떄
(2) 새로운 메모를 추가했을 때 createMemo

### **CODE**

```javascript
async function readMemo() {
  const res = await fetch("/memos");
  const jsonRes = await res.json();
}
```

### **☑️ BE: PYTHON**

### **CODE**

```python
@app.get("/memos")
def read_memo():
    return memos
```

### **☑️ FE: JS**:

### forEach

BE에서 memos를 array로 내려주면
FE createMemo 함수에서는 그것을 받아 배열 안에서 빙글빙글 돌면서 하나하나 받아 화면에 보여줘야 한다.
그러기 위해 displayMemo 함수에 배열에서 받은 것을 전달함.
이 코드는 createMemo 함수안에서 일어나야 함을 주의!

```javascript
async function readMemo() {
  const res = await fetch("/memos");
  const jsonRes = await res.json();

  jsonRes.forEach(displayMemo);
}
```

### 📌 function displayMemo

#### 먼저 보여줄 li, ul을 만들어야 함

read한 memo를 화면에 보여주기  
먼저 보여줄 li, ul을 만들어야 함.

```javascript
const ul = document.querySelector(".memo_ul");
const li = document.createElement("li");
ul.appendChild(li);
```

#### 그리고 li의 innerText를 memo.content로 정의

```javascript
li.innerText = `id:${memo.id} content:${memo.content}`;
```

### **CODE**

이 때 memo를 parameter로 받아와야 함 주의!

```javascript
function displayMemo(memo) {
  const ul = document.querySelector(".memo_ul");
  const li = document.createElement("li");
  ul.appendChild(li);

  li.innerText = `id:${memo.id} content:${memo.content}`;
}
```

#### 그런데 여기까지 하면 새로 메모를 추가할 때마다 새롭게 메모를 전체 다 불러오는 문제 발생

<img width="248" alt="스크린샷 2023-11-22 오후 10 50 42" src="https://github.com/soheeparklee/sc_CRUDmemo/assets/97790983/cb0c3311-d2ff-42de-b876-fb5fb5d5c7c3">

이를 해결하기 위해 readMemo에 read할 때마다 ul지우도록 명령.

```javascript
async function readMemo() {
  const res = await fetch("/memos");
  const jsonRes = await res.json();
  const ul = document.querySelector(".memo_ul");
  ul.innerHTML = "";
  jsonRes.forEach(displayMemo);
}
```

## ✅ PUT(update)

### **☑️ FE: JS**

#### 클릭되면 수정하는 버튼, `displayMemo`함수 안에 만들 것

```javascript
const updateBtn = document.createElement("button");
updateBtn.innerText = "update";
li.appendChild(updateBtn);

updateBtn.addEventListener("click", updateMemo);
```

#### 어떤 메모의 updateBtn이 클릭되었는지 알아야되니까 memo의 id를 받아와야 한다.

이를 위해서 `displayMemo`함수안에 updateBtn의 dataset의 id를 memo.id로 설정

```javascript
updateBtn.dataset.id = memo.id;
```

### 📌 function updateMemo

#### updateMemo 함수에서 memo.id받기

eventListener은 항상 event값을 return하니까 이를 받아와 memo id 받아오기
` const id= event.target.dataset.id;`

#### 수정할 값 입력받기

💡 prompt
`const updateContent= prompt("How would you like to change your memo?")`

#### 수정할 값 받아오기 => request body => PUT

### **CODE**

```javascript
    async function updateMemo(event){
    //get ID of memo to know which memo update btn was clicked
    //eventlistener은 항상 event를 return하니까.
    const id= event.target.dataset.id;
    //뭐라고 수정할지 값 입력받기
    const updateContent= prompt("How would you like to change your memo?")
    const res= await fetch(`./memo/${id}`, {
        method: "PUT",
        headers: {
            "Content-Type: "application/json",
        },
        body: JSON.stringify({
            id: id,
            body: updateContent,
        }),
    })
}

```

### **☑️ BE: PYTHON**

### 📌 def update_memo

FE에서 put, request body로 보냈으니까 받아야 함.  
`@app.put("/memos/{memo_id}")`  
여기서 `memos`는 FE에서 설정해 준 경로이다.
`{memo_id}`는 `PATH`해서 받아올 그 값! 을 의미

**for문**을 사용해  
memos라는 array를 빙글빙글 돌면서 item인 memo를 하나씩 꺼내본다.
`for memo in memos:`
**if문**을 사용해  
`memo.id`(array에 있는 memo id가) FE에서 받아온 메모의 id `req_memo.id`와 같다면,
`memo.content`(array에 있는 memo content)를 FE에서 받아온 수정 값 `req_memo.content`으로 바꾸세요.

```javascript
for memo in memos:
        if memo.id ==req_memo.id:
            memo.content= req_memo.content
            return "Update Succeeded"
    return "No such Memo"
```

#### 내가 쉽게 설명해 본 코드

```javascript
@app.put("/FE에서 설정한 경로memos/{memo_id}")
def update_memo(updateRequestedMemo:Memo):
    #memos라는 배열을 쭉 돌면서 for문
    for arrayItemMemo in memosArray:
        if arrayItemMemo.id ==updateRequestedMemo.id:
            arrayItemMemo.content= updateRequestedMemo .content
```

### **CODE**

```javascript

@app.put("/memos/{memo_id}")
def update_memo(req_memo:Memo):
    #memos라는 배열을 쭉 돌면서 for문
    for memo in memos:
        if memo.id ==req_memo.id:
            memo.content= req_memo.content
            return "Update Succeeded"
    return "No such Memo"

```

## ✅ DELETE

### **☑️ FE: JS**:

### **CODE**

### **☑️ BE: PYTHON**

### **CODE**
