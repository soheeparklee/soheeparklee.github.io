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

그리고 마지막에는 main으로 가도록 hash 설정

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
function writeUserData() {
  const db = getDatabase();
  push(ref(db, "items/"), {
    title: title,
    price: price,
    description: description,
    place: place
  });
  window.location.hash = "/";
}
```

## 공통 components만들기 위해 module화

### footer 모듈화, where 해서 어디에서나 접근할 수 있도록

<Footer />이 공통으로 보이게 하고 싶다면, 별도의 svelte파일로 만들어 저장 후 불러온다.

`export let where;` 해서 위치 저장

`  import Footer from '../components/Footer.svelte';`

`<Footer where="main" />`

### svelte에서는 if문도 HTML사이에 넣을 수 있음

```svelte
<button class="footer-box" on:click={moveToMain}>
    <div class="footer-box-icons">
      {#if where === 'main'}
        <img src="./assets/home.svg" alt="home" />
      {:else}
        <img src="./assets/house_outline.svg" alt="house_outline" />
      {/if}
    </div>
    <div class="footer-box-title">홈</div>
  </button>
```

### style은 아래에 적용하면 그 모듈에만 적용되는 것

## 데이터 읽기

### 실시간 데이터베이스니까 onvalue

#### 반응형 변수 $

```svelte
//read data realtime database
  import { getDatabase, ref, onValue } from 'firebase/database';

  // let이 아닌 반응형 변수로 선언한다.
  // 반응형 변수란, DB에서 값을 받아서 값이 바뀌게 되면 이 변수를 렌더링하고 있는 태그에서 화면을 업데이트 한다.
  // items를 반응형 변수이자 빈 배열로 설정
  $: items = [];
  const db = getDatabase();
  const itemsRef = ref(db, 'items/');
  onValue(itemsRef, (snapshot) => {
    const data = snapshot.val();
    //json으로 정리해서 가지고 오는 방법
    const json = JSON.stringify(data);
    //obj로 감싸서 아이템들 list로 받아오기
    const obj = Object.values(data);

    //DB에서 값 받아와서 items반응형 변수이자 빈 배열에 넣으세요
    items = obj;
  });
```

### on.Mount() 화면 새로고침할 떄마다 함수 계속 실행

원래 JS는 화면이 처음 뜰 떄 한 번만 보여지지만,  
`on.Mount()`사용하면 화면이 렌더링 될 때마다 함수가 실행되어 새로운 값을 DB에서 받아오게 된다.

```svelte
 onMount(()=>{
    onValue(itemsRef, (snapshot) => {
    const data = snapshot.val();
    //json으로 정리해서 가지고 오는 방법
    const json = JSON.stringify(data);
    //obj로 감싸서 아이템들 list로 받아오기
    const obj = Object.values(data);

    //DB에서 값 받아와서 items반응형 변수이자 빈 배열에 넣으세요
    items = obj;
  });
  })
```

### HTML에 보이도록

먼저 item 들의 값을 `{item.title} 각각 받아온 후,   
예전에 지정해주었던 class를 추가해주어 css의 적용을 받게 한다.   
💡 `{#each items as item}`을 사용해 배열을 돌면서 값 받기

```svelte
{#each items as item}
    <div class="item-box">
      <div class="item-box-image">
        <!-- <div>{item.image}</div> -->
      </div>
      <div class="item-box-desc">
        <div class="desc-title">{item.title}</div>
        <div class="desc-price">{item.price}</div>
        <div class="desc-location">{item.place}</div>
        <div class="desc-description">{item.description}</div>
      </div>
    </div>
  {/each}
```

## firebase storage 이미지 가져오기

firebase DB에 url만 올려놓고 그때그때 이미지 가져오기
`firebase.js`에다가 또 공식문서가 시키는 대로 하기

### blob 또는 file에서 업로드

```svelte
  //get image
  import { getStorage, ref as refImage, uploadBytes } from 'firebase/storage';

  const storage = getStorage();
  const storageRef = refImage(storage, '/imgs');

  // 'file' comes from the Blob or File API
  uploadBytes(storageRef, file).then((snapshot) => {
    console.log('Uploaded a blob or file!');
  });
```

### get files

```svelte
  //get image
  import { getStorage, ref as refImage, uploadBytes } from 'firebase/storage';

  const storage = getStorage();
  const storageRef = refImage(storage, '/imgs');

  // 'file' comes from the Blob or File API
  uploadBytes(storageRef, file).then((snapshot) => {
    console.log('Uploaded a blob or file!');
  });

  let files;
  $: if (files) console.log("파일이 바뀌면 consolelog에 files보여줘봐", files);
  //submitBTn에 눌렸을 때 file의 url가져오도록

  const uploadFile= () =>{
    const file= files[0];
    uploadBytes(storageRef, file);
  }
```

file이름 정해주기,  
storageRef수정

```svelte
 //get image
  import { getStorage, ref as refImage, uploadBytes } from 'firebase/storage';

  const storage = getStorage();

  let files;

  const uploadFile = async () => {
    const file = files[0];
    const name = file.name;
    const res = await uploadBytes(refImage(storage, name), file);
  };
```

### HTML에 추가

```svelte
<div>
    <label for="image">image</label>
    <input type="file" id="image" name="image" bind:files />
  </div>
```

## 이미지를 조회

`import { getDownloadURL } from 'firebase`

### image url

```svelte
  const uploadFile = async () => {
    const file = files[0];
    const name = file.name;
    const imgRef= refImage(storage, name)
    const res = await uploadBytes(imgRef, file);
    const url= await getDownloadURL(imgRef);
```

## handleSubmit이란 함수를 만들기

on:submit이 되면,
url을 `uploadFile`에서 받아올 건데,
그 url을 `writeUserData`에게 넘겨서 item의 정보에 url을 추가한다.
그리고 나서 `writeUserData`을 호출해서 user데이터 업데이트

### script부분

```svelte
 //footer 가져오기
 import Footer from '../components/Footer.svelte';

 //get item
 import { getDatabase, ref, push } from 'firebase/database';
 let title;
 let price;
 let description;
 let place;

 const storage = getStorage();
 const db = getDatabase();

 function writeUserData(imgUrl) {
   push(ref(db, 'items/'), {
     title: title,
     price: price,
     description: description,
     place: place,
     insertAt: new Date().getTime(),
     imgUrl: imgUrl,
   });
   window.location.hash = '/';
 }

 //get image
 import {
   getStorage,
   ref as refImage,
   uploadBytes,
   getDownloadURL,
 } from 'firebase/storage';

 let files;

 const uploadFile = async () => {
   const file = files[0];
   const name = file.name;
   const imgRef = refImage(storage, name);
   const res = await uploadBytes(imgRef, file);
   const url = await getDownloadURL(imgRef);
   return url;
 };

 const handleSubmit = async () => {
   const url = await uploadFile();
   writeUserData(url);
 };
```

## url로 전송된 image가져오기

image정보 그리고 insertAt 시간 정보도 calcTime함수 가져와서 화면에 띄우기

```svelte
  {#each items as item}
   <div class="item-box">
     <div class="item-box-image">
       <img src={item.imgUrl} alt={item.imgUrl} />
     </div>
     <div class="item-box-desc">
       <div class="desc-title">{item.title}</div>
       <div class="desc-price">{item.price}</div>
       <div class="desc-time">{calcTime(item.insertAt)}</div>
       <div class="desc-location">{item.place}</div>
       <div class="desc-description">{item.description}</div>
     </div>
   </div>
 {/each}
```

### reverse<br>

`Main.svelte`파일에서 `onValue`에 item 있었음. <br>
배열로 받아온 값을 보여주기 전 `reverse` <br>
`items = obj.reverse();`
