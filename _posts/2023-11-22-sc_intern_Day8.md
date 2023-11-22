---
title: 2023.SEPT.22(WED) 슈퍼코딩 부트캠프 신입연수원 Day 8
categories: [TIL(Today I Learned), SuperCoding_신입연수원(주특기 선택 이전)]
tags: [todayilearned, til]
---

## ✅ Daily Report

### 📌 **TO-DO LIST**

- [ ] submit github blog post
- [x] 40
- [x] 41 CRUD 1
- [x] 42 CRUD 2
- [x] 43 CRUD 3
- [x] 44 CRUD 4
- [ ] 54 CRUD 5
- [ ] submit yesterday's js code
- [x] 1:1 meeting with director - CTO - 프로젝트 전체적 관리 - 팀원 본인이 맡은 바를 잘 해내는지 확인 - 기술적 질문 답변 이끌어주기 - yesterday's js code not working - how do I check my accomplishments? - 확인해주신다고 하셨음

- [ ] assigment: REST API
- [ ] assigment: class in python
- [ ] assigment: 채팅창에서 POST, GET할 수 있는 기능 구현
- [ ] assigment: 소켓이란

      <br>
      <br>

## ✅ Today I Learned

### **REST API**

> Representational State Transfer API

API 작동 방식에 대한 조건을 부과하는 소프트웨어 아키텍처  
웹 상에서 자원을 표현하고 상호작용하는 데 사용되는 인터페이스 설계 원칙  
딱 봐도 "아 이런 작업을 하는 API구나!" 알 수 있게 API를 짜야 한다는 의미  
REST API는 HTTP 요청을 통해 통신함으로써 리소스 내에서 레코드(CRUD 라고도 함)의 작성, 읽기, 업데이트 및 삭제 등의 표준 데이터베이스 기능을 수행

- resourse(균일한 인터페이스)
  서버가 표준 형식으로 정보를 전송  
  각 자원을 고유한 URI(Uniform Resource Identifier)로 표현  
   - URI(Uniform Resource Identifier): 고유한 리소스 식별자로, 각 리소스 식별(웹페이지를 방문하기 위해 브라우저에 입력하는 웹 사이트 주소와 유사)
  요청이 어디에서 오는지와 무관하게, 동일한 리소스에 대한 모든 API 요청은 동일
- stateless(무상태, 상태 없음)
  각 요청이 서버의 이전 상태를 참조하지 않고 독립적으로 처리된다  
  서버가 이전의 모든 요청과 독립적으로 모든 클라이언트 요청을 완료하는 통신 방법  
  이로 인해 서버와 클라이언트 간의 의존성이 낮아지고, 확장성과 유지 보수가 용이
- cacheable(캐시 가능)
  캐시 기능을 이용하여 응답 결과를 저장해두고 재사용 가능  
  서버 부하 ⬇️  
  응답 속도 ⬆️ 성능 향상
- client-server decoupling  
  클라이언트와 서버 분리 따라서 각각의 역할 명확  
  각각 독립적으로 발전, 유연한 시스템 구축  
   - 클라이언트 애플리케이션이 알아야 하는 유일한 정보는 요청된 리소스의 URI  
   - 서버 애플리케이션은 HTTP를 통해 요청된 데이터에 전달하는 것 말고는 클라이언트 애플리케이션을 수정하지 않아야
- layered System(게층화 구조)
  여러 계층으로 구성 가능  
  각 계층은 독립적으로 기능 수행
- method(표준화된 메소드)
  일반적으로 HTTP 메소드를 이용해 자원에 대한 조작을 수행  
  사용되는 메소드로는 GET, POST, PUT, DELETE 등

### **CRUD**

데이터를 처리하는 네 가지 기본 작업

- create
- read
- update
- delete

### **class in Python**

```python
class Me:
    def introduce_myself(self, name, age, job):
        self.name= name
        self.age= age
        self.job= job

sohee = Me("So Hee", 28, "programmer")

print("저의 이름은", sohee.name, "입니다.")
print("저는" sohee.age"살 입니다.")
```

```python
class Me:
    def introduce_myself(self, name, age, job):
        self.name= name
        self.age= age
        self.job= job

    def introduce_print(self):
        print(f"저의 이름은{self.name}입니다")
        print(f"저는{self.age}살 입니다. ")

sohee = Me("So Hee", 28)
sohee.introduce_print()
```

### **HTML 통신**

> 클라이언트의 요청이 있을 때 서버가 응답하는 방식, 단방향 통신

HTTP 통신은 클라이언트에서 서버로 요청을 보내고, 서버가 이에 응답

### **socket 통신**

> 클라이언트와 서버 양쪽에서 서로에게 데이터 전달을 하는 방식의 양방향 통신

소켓 통신에서는 서버와 클라이언트가 양방향 연결이 이루어진다.  
클라이언트만 서버로 요청을 보내는 것이 아니고, 서버도 클라이언트에게 요청을 보낼 수 ⭕️  
스트리밍이나 실시간 채팅같이 실시간으로 데이터를 주고 받아야 하는 경우 연결을 자주 맺고 끊는 HTTP 통신보다 소켓 통신을 직접적으로 사용하는 것이 적합  
소켓 통신은 계속해서 연결을 유지하고 있기에 HTTP 통신보다 연결/해제의 반복적 오버헤드가 줄어든다

## ✅ Trouble Shooting

### **🔴 Trouble** 422 Unprocessable Entity

`127.0.0.1:61773 - "POST /memos HTTP/1.1" 422 Unprocessable Entity`

#### **🟠 Mistakes I Made\_헷갈리거나 실수한 점**

id의 타입을 잘못 입력

```python
class Memo(BaseModel):
    id: str
    content: str
```

#### **🟢 What I learned\_알게된 점**

id 타입을 바꿔주면 해결!

```python
class Memo(BaseModel):
    id: int
    content: str
```

### **🔴 Trouble** memo is not defined

#### **🟠 Mistakes I Made\_헷갈리거나 실수한 점**

parameter로 받아온 값을 주어야 한다.

```javascript
function displayMemo() {
  const ul = document.querySelector(".memo_ul");
  const li = document.createElement("li");
  ul.appendChild(li);

  li.innerText = `id:${memo.id} content:${memo.content}`;
}
```

#### **🟢 What I learned\_알게된 점**

```javascript
function displayMemo(memo) {
  const ul = document.querySelector(".memo_ul");
  const li = document.createElement("li");
  ul.appendChild(li);

  li.innerText = `id:${memo.id} content:${memo.content}`;
}
```

---

## ✅ MENTORING

---

## ☑️ Summary of the Day <br>

Long Day today as well!  
I had to deal with some trouble shootings, which took me lots of time.
But better than last time, I could understand more of CRUD!
