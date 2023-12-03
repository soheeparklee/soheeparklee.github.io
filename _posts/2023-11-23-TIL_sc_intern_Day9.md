---
title: 2023.SEPT.23(THU) 슈퍼코딩 부트캠프 신입연수원 Day 9
categories: [TIL(Today I Learned), SuperCoding_신입연수원(주특기 선택 이전)]
tags: [sql, nosql, erd, rdb]
---

## ✅ Daily Report

### 📌 **TO-DO LIST**

- [x] submit github blog post
- [ ] 45
- [x] 46
- [x] 47
- [x] 48
- [x] 49
- [x] 51
- [x] 52
- [x] 53
- [x] 과제 다시 문의
- [x] assigment: 데이터베이스 없이 앱을 개발했는데 이로 인해 생길 수 있는 문제들
- [x] assigment: RDB와 NoSQ
- [x] assigment: QUERY
- 그러면 restAPI method중에 path, query는 get, requestbody는 post, 그러면 delete, put은?

      <br>
      <br>

## ✅ Trouble Shooting

### **🔴 Trouble** deleteBtn doenst work!!!

#### **🟠 Mistakes I Made\_헷갈리거나 실수한 점**

백엔드에서 메모 아이디 int로 받으라고 했고, 프론트에서도 잘 보냈으며
create, read, update까지, 그리고 post, put, read메소드는 문제가 없었는데 delete에서 삭제 버튼을 눌러 메모가 지워지지 않는 문제가 생김.

#### **🟡 What I tried\_스스로 시도해 본 것들**

- memos.pop을 pop말고 clear, remove 써봤지만 안됨
- memos.pop(index)에서 index말고 memo 등 다른 값 넣었지만 안 됨

#### **🟢 What I learned\_알게된 점**

메모 아이디 값을 int가 아닌 str으로 바꿔주기,  
BE에서도 아이디 값을 스트링으로 받아야 함.  
이렇게 했더니 해결이 되었고, 이제는 삭제 버튼을 누르면 메모가 잘 삭제된다.

```javascript
async function createMemo(value) {
  //post on server
  const res = await fetch("/memos", {
    method: "POST",
    headers: {
      "Content-Type": "application/json"
    },
    body: JSON.stringify({
      id: toString(new Date().getTime()),
      content: value
    })
  });

  readMemo();
}
```

```python
class Memo(BaseModel):
    id: str
    content: str
```

## ☑️ Summary of the Day <br>

Such a difficult day!  
Very difficult with mentoring...I have so little time to study!
