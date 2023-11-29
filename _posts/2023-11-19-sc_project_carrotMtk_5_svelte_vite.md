---
title: CarrotMkt Clone Coding_Svelte, Vite
categories: [Project, Carrot MKT Clone Coding]
tags: [clonecoding, project, firebase, svelte, vite]
---

## ✅ Svelte

### git

firebase를 이용할 branch하나 만들기

### npm을 위해 node.js를 다운받아야

node.jsd안에 npm이 내장되어 있다.  
npm으로 vite, svelte(framework)를 terminal에서 설치  
서버 없이 vite만으로 페이지를 로컬 호스트에서 띄울 수 있다.

package.json안에 프로젝트에 관한 정보 있음  
프로젝트 관련 설정들을 여기서 바꿀 수 있다.  
프로젝트 이름, 타입, 버전, 의존성 등...

README 우리 프로젝트에 대한 설명을 쓴다.

### svelte구조

app.svelte파일 안에 위에는 js, 가운데는 html, 아래에는 css

```svelte
<script>
//JAVASCRIPT
</script>

<main>
//HTML
</main>

<style>
// CSS
</style>
```

### routing HTML

routing `npm i svelte-spa-router`
<Router routes= {routes}/>

`app.svelte` js안에 routes라고 해서 경로를 만들어준다. <br>
routes안에 우리가 원하는 페이지(index, write, signup, login)의 svelte파일을 만들어준다. <br>
이것이 바로 **모듈 방식**! 페이지 각각 만들고 나중에 번들러로 합치는 방식. <br>
모듈 방식으로 각각 svelte파일 import<br>

router도 import<br>
` import Router from "svelte-spa-router"`

```javascript
import Main from "./pages/Main.svelte";
import Login from "./pages/Login.svelte";
import Signup from "./pages/Signup.svelte";
import Write from "./pages/Write.svelte";
import Notfound from "./pages/Notfound.svelte";
import Router from "svelte-spa-router";

const routes = {
  "/": Main,
  "/login": Login,
  "/signup": Signup,
  "/write": Write,
  "*": Notfound
};
```

### svelte에서는 JS요소를 HTML로 쉽게쉽게 불러올 수 있다.

```javascript
<script>
let time= "20:12"
</script>

<header>
<div class="info-bar__time"> {time} </div>
```

```javascript
<script>
  let hour = new Date().getHours();
  let min = new Date().getMinutes();
</script>

<header>
  <div class="info-bar">
    <div class="info-bar-time">{hour}:{min}</div>
```

### import CSS

app.svelte에다가 css도 `  import './css/style.css';`해서 바로 적용 가능~

### assets(icons)

이런 assets는 public 파일로 옮겨주면 됨.

### 글쓰기 버튼 눌렸을 때 경로 수정해주기

기존

```html
<main>
  <a class="write-btn" href="write.html"> + 글쓰기</a>
</main>
```

수정 후

```html
<a class="write-btn" href="#/write"> + 글쓰기</a>
```

💟 마지막으로, 자바스크립트는 firebase에서 추가!
