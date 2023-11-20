---
title: 2023.SEPT.20(MON) 슈퍼코딩 부트캠프 신입연수원 Day 6
categories: [TIL(Today I Learned), SuperCoding_신입연수원(주특기 선택 이전)]
tags: [todayilearned, til, resume, setinterval, settimeout, getday]
---

## ✅ Daily Report

### 📌 **TO-DO LIST**

- [x] submit blog post 중간보고, 일일보고
- [x] 슈퍼코딩28, 29, 30, 31강
- [x] Team Meeting 9PM
      <br>
      <br>

## ✅ Today I Learned

### **How to check the client reply and the answer**

일단 for문을 만들어 i가 index의 수만큼 반복되도록 한다.  
answer[i]로 해서 i번째 알파벳을 받아온다.  
사용자가 입력한 답변을 `data-index`로 받아온다.  
그러면 client reply와 answer의 i번째 알파벳끼리 비교할 수 있게 된다.

```javascript
const clientReply = document.queryselector(
  `.box[data-index="${attempts}${i}"]`
);
clientReply === answer[i];
```

그리고 client reply에 맞는 알파벳이지만, 위치가 잘못되었을 수도 있다.
이 때는 `includes`함수를 사용한다.
`answer.includes(clientReply)`

### **getDay() in JS**

JS에서 요일을 가져오면 1,2,3...등 숫자로 나타난다.  
그래서 요일을 배열로 미리 만들어주고, 이 배열의 순서대로 가져오는 코드를 짠다.

```javascript
const weekday = ["일", "월", "화", "수", "목", "금", "토"];
const time = new Date();
const day = weekday[time.getDay()];
```

### **setInterval VS setTimeout**

두 함수는 각각 1회성, 주기성이라는 차이가 있다.  
근데 `setTimeout`을 사용해서도 `setInterval`과 같은 효과를 낼 수 있다.  
다음은 각각을 이용하여 console에 1초마다 내용이 뜨도록 만든 것이다.

> setInterval

```javascript
function setIntervalFunction() {
  console.log("I repeat using setInterval");
}
setInterval(setIntervalFunction, 1000);
```

> setTimeout

함수 안에서 자기 자신을 부르는 것을 **재귀함수**라고 한다.

```javascript
function setTimeoutFunction() {
  console.log("I repeat using setTimeout");
  setTimeout(setTimeoutFunction, 1000);
}
setTimeoutFunction();
```

## ☑️ Summary of the Day <br>

I finally finished my Wordle Clone coding project!!!  
Today took longer than expected because I was organizing how to clone Wordle.  
Organizing takes a lot of time.  
I also became CTO of team3!  
Such exciting and beneficial days.
