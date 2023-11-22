---
title: get answer from backend(FastAPI)
categories: [Project, Wordle Clone Coding]
tags: [clonecoding, project, html, css, javascript, frontend, backend, fastapi]
---

## ✅ **BE:PYTHON**

```python
answer= "HELLO"

@app.get("/answer")
def get_answer():
    return answer
```

## ✅ **FE:JS**

`fetch`는 javascript에서 BE로 요청을 보낼 떄 쓰는 함수이다.  
("/answer")라는 경로로 요청을 보내세요  
await 기다렸다가 res에 BE에서 받아온 값 업데이트 할래요  
res를 json으로 바꿔서 answer에 기다렸다가 업데이트 할게요
**json(javascript object notation)**: javascript에 어울리는 형식

이 코드를 handleEnter(정답 확인하는 함수)에 넣어주면 된다.

```javascript
//get answer from BE
const res = await fetch("/answer");
const answer = await res.json();
```
