---
title: Svelte, Vite
categories: [Web, Tools]
tags: [svelte, vite] # TAG names should always be lowercase
---

### 🔨 SVELTE(web framework)

React를 쓰기 위해서는 새로운 문법, 원리를 이해해야하므로 SVELTE로 연습  
SVELTE는 HTML, CSS, JS 문법 그대로 사용함

#### web framework가 왜 필요한가?

JS의 경우 코드의 자유로움이 존재, 딱히 규격이 없음. 이는 장점이자 단점이 된다.  
일정한 제한을 두어 그 안에서 제한하게 하므로서 서로의 코드 이해 ⬆️

- react

  - jsx하는 리액트만의 문법이 존재
  - SPA single page appplication
  - 많은 js라이브러리와 호환
  - 가상 DOM
  - 패키지가 크다. 빌드되었을 떄 크다.

- svelte
  - HTML, CSS, JS 문법 그대로 사용, 배우기가 쉬움
  - complier(가상 DOM이 존재하지 않는다. )
  - 다만, 생태계가 부족(typescript, IDE 지원 미흡)
  - 패키지가 작아 빨리빨리 작동, 로딩이 빨리빨리 된다.

### CommonJS 모듈

여러 개의 파일로 나눠서 개발하는 **모듈**방식  
(하나의 파일에 모든 코드를 작성하면...유지, 관리, 확장이 힘듦 ㅠㅠ)  
`npm`으로 library 가져오기  
**CommonJS** `npm`의 등장으로 모듈을 모두가 공유할 수 있는 환경 조성
그런데 파일이 너무 많아지면 그 파일들을 가져오는 시간 ⬆️

### 🔨 Bundler Vite

그러면 그 파일들을 묶어주면 되잖아! 배포할 때는 파일들을 모두 bundle하여 배포
거대한 프로그램을 만들 떄 묶어주기  
빌드 후 하나로 만드는 과정이 필요해지면서 수정시마다 새롭게 빌드하는 시간이 너무 오래 걸린다. => 더 빠른 프로그램의 필요성  
따라서 Vite개발
