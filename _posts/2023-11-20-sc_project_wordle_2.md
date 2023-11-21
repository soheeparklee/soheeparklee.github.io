---
title: clock, timer, padStart, toString, setInterval, setTimeout, newDate()
categories: [Project, Wordle Clone Coding]
tags: [clonecoding, project, html, css, javascript, frontend]
---

## ✅ setInterval VS setTimeout

> setInterval
> `setInterval(function, n초마다 호출)`

- 주기적 호출
- n초마다 계속 호출됨

> setTimeout

- 1회성 호출
- 1번 하고 끝
- 재귀형식으로 setInterval처럼 사용 가능

## ✅ new Date()

```javascript
new Date().getFullYear();
// 2023
new Date().getDate();
// 20일
new Date().getDay();
//1
new Date().getMinutes();
new Date.getSeconds();
```

## ✅ 시계만들기

```javascript
function clockFunction(){
const clock= document.querySelector(".clock");

const time= new Date();
const minutes= time.getMinutes().toString().padstart(2, "0")

const seconds= time.getSeconds().toString().padstart(2, "0")

clock.innerText= minutes ":" seconds
}

setInterval(clockFunction, 1000)

```

## 💡 padstart()

2개의 문자로 보여주는데, 1개 밖에 없을 떄는 0붙여주세요.  
padStart는 문자열에만 적용되기 때문에 문자열로 바꿔줘야 한다.

```javascript
.padstart(2, "0")
2개의 문자로 보여주는데, 1개 밖에 없을 떄는 0붙여주세요.
padStart는 문자열에만 적용되기 때문에 문자열로 바꿔줘야 한다.
// 1 = > 01

```

## 💡 문자열로 바꿔주는 toString()

```javascript
.toString();
문자열로 바꿔주기

```

## ✅ 연도, 달, 날짜까지 표현되는 시계 만들기

## ✅ 타이머 만들기

```javascript
const startTime= new Date();

function timerFunction(){
const clock= document.querySelector(".timer");

const currentTime= new Date();
const passedTime= new Date(currentTime- startTime)

const minutes= passedTime.getMinutes().toString().padstart(2, "0")
const seconds= passedTime.getSeconds().toString().padstart(2, "0")


timer.innerText= minutes ":" seconds
}

setInterval(timerFunction, 1000)

```

`const passedTime= currentTime- startTime`
이렇게만 하면 엄청난 숫자열만 나옴.  
이를 사람이 알아볼 수 있는 시간으로 나타내기 위해 `new Date();`으로 감싼다.
