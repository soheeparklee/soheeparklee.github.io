---
title: CarrotMkt Clone Coding_Firebase
categories: [Project, Carrot MKT Clone Coding]
tags: [clonecoding, project, firebase]
---

## 🛠️ build hosting

configure files로 hosting
`Hosting: Configure files for Firebase Hosting and (optionally) set up GitHub Action deploys`

### public directory

dist에 우리가 원하는 자료들 넣으면 dist폴더에 있는 파일들이 배포가 될 것이다.

```
? What do you want to use as your public directory? dist
? Configure as a single-page app (rewrite all urls to /index.html)? Yes
? Set up automatic builds and deploys with GitHub? No
✔  Wrote dist/index.html
```

### 💡 vite라는 번들러로 build를 할 것이다.

vite는 자동으로 dist폴더에 있는 파일들을 build
`npm run build`
dist폴더에 가보면 js, css를 한 줄로 묶어서 build한 것을 볼 수 있음.

### 💡 배포

terminal ` firebase deploy`

### 💡 `npm run build` + ` firebase deploy` 를 한 번에 실행하고 싶다면?

pachage.json파일에 다음과 같은 코드 추가해주기

```
 "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview",
    "deploy": "npm run build && firebase deploy"
  },
```

## 📊 build, real time database

database를 만든 후, 공식 문서를 참고해가면서 연결
<https://firebase.google.com/docs/database/web/start?hl=ko&authuser=0>

### 실시간 데이터베이스 JS SDK 추가 및 실시간 데이터베이스 초기화

`firebase.js`라는 파일을 src폴더에 만들어 여기에다가 복사, 붙여넣기
이 코드에다가 나의 databaseURL을 또 넣기
`  databaseURL: "https://sc-carrot-mkt-improved-default-rtdb.asia-southeast1.firebasedatabase.app/",`

### main.js에 import firebase.js

`//firebase
import "../firebase.js"`

firebase없으니까 firebase도 설치
`npm i firebase`

## 🧮 데이타 읽기 & 쓰기

공식문서 따라가기
<https://firebase.google.com/docs/database/web/read-and-write?hl=ko&authuser=0>

### 우리는 write.svelte가 데이터 쓰는 페이지이니까 여기 javascript에 공식문서가 시키는 것 추가해주기

write.svelte의 javascript안에 우리가 입력받고 싶은 변수들을 만든다.  
값 받아와서 변할거니까 let이어야 한다.

```javascript
let title;
let price;
let description;
let place;
```

그리고 HTML안에 `bind:value`로 값을 연결해준다.

```html
<div>
  <label for="title">title</label>
  <input type="text" id="title" name="title" bind:value="{title}" />
</div>
```

### form submit이 제출되면, `writeUserData`함수를 실행한다.

💡 svelte에서는 매우 간단히 eventListener할 수 있음.
`on:click()`
form이 submit되었을 때 `writeUserData`함수
그리고 `eventListener`할 때 `preventDefault`했던 것도 HTML에 간단하게 추가 가능~

```javascript
<form id="write_form" on:submit|preventDefault= {writeUserData}>
```

### set아니고 push

❌ set은 id가 중복되면 값이 수정되어 버린다.  
"신발"이라는 이름으로 두 개의 item이 들어오게 되면, 나중에 들어온 값으로 치환되어 버린다!!

```javascript
function writeUserData(event) {
  const db = getDatabase();
  set(ref(db, "itmes/" + title), {
    title: title,
    price: price,
    description: description,
    place: place
  });
}
```

⭕️ push는 id가 중복되어도 다른 값으로 추가된다.

```javascript
function writeUserData(event) {
  const db = getDatabase();
  push(ref(db, "itmes/"), {
    title: title,
    price: price,
    description: description,
    place: place
  });
}
```
