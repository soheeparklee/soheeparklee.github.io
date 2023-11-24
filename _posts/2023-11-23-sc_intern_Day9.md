---
title: 2023.SEPT.23(THU) 슈퍼코딩 부트캠프 신입연수원 Day 9
categories: [TIL(Today I Learned), SuperCoding_신입연수원(주특기 선택 이전)]
tags: [todayilearned, til]
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

## ✅ Today I Learned

### **SQL**

**SQL Structured Query Language**  
관계형 데이터베이스 관리  
시스템에서 데이터를 관리하기 위해 사용되는 표준 프로그래밍 언어

### **ERD**

**Entity Relation Diagram**  
코드로 된 것을 그림(표)으로 보여주는 프로그램  
예를 들어 dBeaver

### **RDB 관계형 데이터베이스**

#### ☑️ 장점:

**1.구조화된 데이터:**  
RDB는 테이블 구조를 가지고 있어 데이터를 구조화하고 정규화할 수 있습니다. 이로 인해 데이터의 일관성과 무결성이 유지됩니다.
**2. 표준화된 질의 언어(SQL):**  
SQL을 통해 데이터를 쉽게 조회, 추가, 수정, 삭제할 수 있습니다. 또한 다양한 DBMS에서도 호환성이 좋습니다.
**3. 트랜잭션 지원:**  
RDB는 ACID(원자성, 일관성, 고립성, 지속성) 원칙을 지원하여 안정적인 트랜잭션 처리가 가능합니다.

#### ☑️ 단점:

**1. 확장성:**  
수직 확장(Scale-up)을 주로 지원하며, 수평 확장(Scale-out)에 대한 지원이 제한적입니다. 이로 인해 대용량 데이터 처리나 분산 환경에서의 성능 저하가 발생할 수 있습니다.
**2. 유연성 부족:**
고정된 스키마로 인해 데이터 구조의 변경이 어렵습니다. 새로운 데이터 타입이나 구조 변경이 필요할 경우, 추가 작업이 필요합니다.

### **NoSQL 비관계형 데이터베이스**

#### ☑️ 장점:

**1. 확장성:**  
NoSQL은 수평 확장(Scale-out)을 지원하여 대용량 데이터 처리와 분산 환경에서 뛰어난 성능을 보입니다.
**2. 유연성:**  
고정된 스키마가 없어 데이터 구조의 변경이 용이합니다. 다양한 데이터 타입과 구조를 저장할 수 있어 개발 시간을 단축할 수 있습니다.
**3. 다양한 데이터 모델:**  
 Key-Value, Document, Column-Family, Graph 등 다양한 데이터 모델을 지원하여 여러 상황에 적합한 솔루션을 선택할 수 있습니다.

#### ☑️ 단점:

**1. 일관성:**  
대부분의 NoSQL 데이터베이스는 확장성을 위해 일관성을 희생하는 경향이 있습니다. CAP 이론에 따라 일부 데이터베이스는 데이터의 일관성을 보장하지 않을 수 있습니다.
**2. 표준화된 질의 언어 부재:**  
NoSQL에는 표준화된 질의 언어가 없어 각 데이터베이스마다 사용하는 질의 언어가 다릅니다. 이로 인해 새로운 데이터베이스를 사용할 때마다 새로운 질의 언어를 학습해야 할 수 있습니다.
**3. 트랜잭션 지원 부족:**
NoSQL 데이터베이스 중 일부는 트랜잭션 처리를 지원하지 않거나 제한적으로 지원합니다. 따라서 복잡한 트랜잭션 처리가 필요한 경우 RDB보다 불리할 수 있습니다.

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

---

**💟 참조**