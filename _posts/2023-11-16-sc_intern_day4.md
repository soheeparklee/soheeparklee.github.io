---
title: 2023.SEPT.16(THU) 슈퍼코딩 부트캠프 신입연수원 Day 4
categories: [TIL(Today I Learned), SuperCoding_신입연수원(주특기 선택 이전)]
tags:
  [
    todayilearned,
    til,
    책추천,
    book,
    테크블로그,
    carrotmkt,
    clonecoding,
    opacity,
    troubleshooting
  ]
---

## ✅ DAILY REPORT

### 📌 **TO-DO LIST**

- [x] submit blog post 중간보고, 일일보고
- [x] 슈퍼코딩 19, 20, 21, 22강
- [x] 18강: CarrotMkt header
- [x] 19강: footer
      <br>

## ✅ Today I Learned

### **Framework VS Library**

#### ☑️ Framework

> 클래스 + 인터페이스의 집합

framework is already **fixed** how to use  
애플리케이션 코드가 프레임워크에 의해 사용, 결정된다.  
프레임워크에 따라 사용자가 그 안에 필요한 코드 작성

- 앱/서버 구동
- 메모리 관리
- 이벤트 루프
- 소프트웨어의 설계, 구현을 재구성이 가능하게 하는 인터페이스

💡 Example of Framework

- **Spring** for JAVA
- **Django** for Python
- **Android** for android app

#### ☑️ Library

> 라이브러리는 개발에 필요한 것들을 미리 구현해 놓은 도구이다.  
> 재사용이 가능하도록 기능을 미리 구현해놓고 필요한 곳에서 호출해 사용한다.

프레임워크와는 다르게, 사용자가 라이브러리를 사용해 애플리케이션 흐름을 직접 제어

- 미리 작성된 코드
- 함수
- 클래스 등

💡 Example of Library

- Python pip로 설치한 패키지/모듈 (tensorflow, pandas, beautifulsoup 등등)
- C++의 표준 템플릿 라이브러리 (STL)
- Node.js에서 npm으로 설치한 모듈
- HTML의 클라이언트 사이드 조작을 단순화하는 JQuery
- 웹에서 사용자 인터페이스 개발에 사용되는 React.js

#### ☑️ IOC 제어의 역전

> Inversion of Control  
> 프레임워크와 라이브러리의 차이는 **제어흐름**이 어디에 있는가이다.  
> Who has the **flow** of the application?

- 어떤 일을 하도록 만들어진 `framework`에 의해 `control`권한을 위임하는 것
- 프레임워크에게 **제어의 흐름**을 넘겨서 개발자가 코드를 편하게 작성

- When you use a library, you are in charge of the flow of the application. You are choosing when and where to call the library.
- When you use a framework, the framework is in charge of the flow. It provides some places for you to plug in your code, but it calls the code you plugged in as needed.

`framework`는 `library`를 포함한다!
`프레임워크` 위에 사용자가 코드를 입력하다가 필요할 떄 `라이브러리`를 호출!

### **CarrotMkt Chat page**

당근마켓에서 채팅 페이지를 `HTML`, `CSS` 사용하여 만듦.

<img width="388" alt="스크린샷 2023-11-17 오전 1 53 20" src="https://github.com/soheeparklee/sc_FrontBackTryout/assets/97790983/978130f1-baae-499b-afff-b8f9e1bc4110">

<https://github.com/soheeparklee/sc_project_carrotMkt_improved.git>

## ✅ MENTORING\_멘토링

### **🐝 취업 관련 꿀팁**

1. 지원 사이트

- 로켓펀치
- 링크드인
- 원티드
- 사람인
- 더브이씨(투자 단계, 투자 받은 라운지, 투자 규모 파악하기)

2. 포지션, 테크 스택 키워드로 검색하기

3. 취업 카테고리

- 컨텐츠: SNS, Streaming, Portal, Information, Community
- 커머스: Delivery, Shopping, P2P Market(개인판매), Crowd Funding, Platform(결제포함)
- 핀테크: Pay/PG, Banking, Stock, P2P Lending(허가받은업체만투자하고싶은개인들이빌려주는대출플랫폼), Cryptocurrency(블록체인,암호화폐)
- 모빌리티: Mobility, Car Sharing, Navigation, Self-driving(자율주행)

### 코딩 공부 사이트

- 유데미
- 앙마코딩
- 패스트캠퍼스
- 중퇴한 영훈이
- 우아한 코스

> 테크 블로그(기술면접)

<https://gyoogle.dev/blog/>
<https://github.com/JaeYeopHan/Interview_Question_for_Beginner>

> Book recommendation for code-review

<https://product.kyobobook.co.kr/detail/S000031741573>

> Book for writing Blog

<https://www.yes24.com/Product/Goods/79378905>

> Book for CS

<https://product.kyobobook.co.kr/detail/S000003114660>
<https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=300406950>
<https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=277386060>

## ✅ Trouble Shooting

### **🔴 opacity:0 VS display:none**

`opacity: 0`을 주었더니 `opacity:1`로 만들었을 때도 화면이 클릭되지 않았다.
`button`들을 클릭할 수 없어 난감했다.

#### **🟡 What I tried\_스스로 시도해 본 것들**

`button`에 문제가 있는 줄 알고 `div`로 바꿨다가, `a`tag으로 바꿨다가...난리부르스

#### **🟢 What I learned\_알게된 점**

`opccity: 0`은 화면을 클릭할 수 없게 만든다.  
화면을 띄우지 않게 만드는 다른 방법은 `display: none;`

---

### **🔴 css사용해 item을 어딘가에 붙여버리기**

> CarrotMkt의 `footer`을 만드는데 `footer`을 페이지 밑에 붙여야했다! 근데 방법을 모름.

#### **🟡 What I tried\_스스로 시도해 본 것들**

`align-itmes: end`로 해결해보려고 했으나 안 됨!

#### **🟢 What I learned\_알게된 점**

item의 위치를 어딘가로 딱! 정해버릴 떄는 `position`을 사용한다.

```css
position: fixed;
bottom: 0;
```

#### **🔵 I should work on\_ 부족한 점**

- css positions를 더 자주 project에 적용하며 써봐야겠다.
- 아니면 `margin-top`을 줘서 아래로 내리거나.
  <br>

---

### **🔴 css item이 잘려보임!!!**

> CarrotMkt의 `footer` 끝이 잘려보이는 문제
> `footer`을 밑에 붙였는데 끝이 잘린다! 왜 그러지?
> <img width="213" alt="스크린샷 2023-11-17 오전 1 56 42" src="https://github.com/soheeparklee/sc_FrontBackTryout/assets/97790983/5b4c0a27-db41-49a1-9886-4545d6d81e50">

#### **🟡 What I tried\_스스로 시도해 본 것들**

`margin-right: 20px;`  
`padding-right: 20px;`  
`width: 100vw;`  
`width: auto;`  
`width: 100%;`

다 해 보았으나 계속 잘림! 그리고 `footer`이 이상한 곳으로 막 이동함.
`position`속성 때문에 그런 것 같음.

```css
width: 95%;
justify-content: space-between;
```

- `width: 95%;`로 해결을 해 두었음.

#### **🟢 What I learned\_알게된 점**

- how to reset CSS
  <br>

---

### **🔴 가려졌으면 하는 부분들이 안 가려지고 스크롤을 내리면 보임**

<img width="288" alt="스크린샷 2023-11-17 오전 1 56 11" src="https://github.com/soheeparklee/sc_FrontBackTryout/assets/97790983/6aef8488-e987-42b9-b3b9-c81a5afe5378">

`@media screen`을 사용해 크기 조절을 했는데,
보이지 않았으면 하는 부분들이 보임

#### **🟢 What I learned\_알게된 점**

`<div class="size-adjust">사이즈를 조정해 주세요</div>`
`@media screen` 을 적용할 `div`를 HTML가장 아래에 두기

<img width="667" alt="스크린샷 2023-11-17 오전 1 55 21" src="https://github.com/soheeparklee/sc_FrontBackTryout/assets/97790983/ecc788da-682c-4f85-a227-d8ea3bc3dbf3">

그럼에도 불구하고 `scroll`을 하면 아래 `footer`이 보임 ㅠㅠ  
`<div class="size-adjust">사이즈를 조정해 주세요</div>`  
이 `div`를 `position: fixed`로 준다.  
그러면 cursor을 내려도 div가 cursor을 따라옴.

#### **🔵 I should work on\_ 부족한 점**

- CSS `position` 으로 할 수 있는 기능들이 많다.
  <br>
  <br>

---

### **🔴 특정 class안에 또 특정 class에만 효과를 주고 싶음**

> `icon`에 마우스 `hover`했을 때는 아이콘에 `transform`적용되는데, `text`에 `hover`하면 아이콘 반응 없음.

#### **🟠 Mistakes I Made\_헷갈리거나 실수한 점**

> 기존 코드

```css
footer-box-icons:hover {
  transform: scale(1.2);
  transition: all 1s ease;
}
```

#### **🟢 What I learned\_알게된 점**

```css
.footer-box:hover .footer-box-icons {
  transform: scale(1.2);
  transition: all 1s ease;
}
```

> X 가 `hover`되었을 때, Y 에 `animation`, `transform`효과 주는 방법
> 글자는 안 커져서 더 좋음.
> <br>

**만약 글자까지 커지게 하고 싶으면?**

> 글자까지 포함된 `div`에 `hover`기능 추가하면 되지.

```css
.footer-box:hover {
  transform: scale(1.2);
  transition: all 1s ease;
}
```

## ☑️ Summary of the Day <br>

I managed to Debug and Post a lot today.  
My first clone-coding project in Super Coding as CarrotMkT was successful.  
However, my time-management was not so efficient...  
I am going to bed at 2am!!

 <br>
 <br>

**💟 참조**  
Framework VS Library
<https://www.freecodecamp.org/news/the-difference-between-a-framework-and-a-library-bd133054023f/>
