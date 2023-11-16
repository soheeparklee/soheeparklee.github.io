---
title: transition, transform, animation
date: 2023-11-15
categories: [Frontend, CSS]
tags: [html, css, transition, transform, animation]
# TAG names should always be lowercase
---

## ✅ transition

> to change property of item with **duration**

- css 값이 변화할 때 프로퍼티 값이 duration에 걸쳐 일어나도록 하는 것이다.
- duration을 부여해 속도를 조절한다.
- 왜 ❓ css 스타일 변경을 부드럽게 표현하기 위해!!
- 몇 초 동안 바뀔건지, 어떻게 자연스럽게? (둔탁하지 않게) 어떤 요소들을 바꿀까?

- cubic-beizer
  <img width="556" alt="스크린샷 2023-11-17 오전 1 59 26" src="https://github.com/soheeparklee/sc_FrontBackTryout/assets/97790983/1d3269b7-645d-4980-9884-e1cb244bd2a0">

```css
div {
  transition: all 2s ease-in-out;
}

div:hover {
  background-color: pink;
}
```

**hover 했을 때**
`div`의 전체를, 2초동안, `ease-in-out`방식으로 자연스럽게, `background-color: pink`하게 바꾸세요.

#### 💡 `transition` VS `animation`?

- `transition` 이 더 제한적인 효과
- `transition`: 어떤 property값이 다른 값으로 변화할 때
- `transition`은 자동으로 발동되지 않아 `pseudo class`와 함께 사용 `:hover`
- `animation` 은 `@keyframes`를 만들어 시간, 반복재생 가능, `pseudo class` 필요 없음

## ✅ transform

> 회전, 크기 조절, 기울이기, 이동 효과

#### 💡 what can you do with `transform`?

- rotate
- scale: 크기 바꾸기
- translate: 이동하여 자리 바꾸기(앞, 뒤로 이동)
- skew: 비틀기  
  <br>

#### 💡 `transform` VS `animation`?

- 애니메이션 효과가 있는게 아님 ❌
- 따라서 **변화된 형태**로 화면에 표시됨  
  (예를 들어, 사진을 뒤집어 표현하고 싶다면 `transform: scaleX(-1);`)
- 그래서 `transform`에 `animation`을 추가하면 변하는 모습을 나타낼 수 있는 것임.

## ✅ animation

> animation, transform을 함께 사용

- `@keyframes`를 구성하여 `@keyframes` 내에서 움직임을 시간 흐름 단위로 제어
- alternate: 갔다가 돌아오기

```css
//animation
@keyframes moving-fish {
  from {
    transform: translateX(-50px);
  }
  to {
    transform: translateX(50px);
  }
}
img {
  animation: moving-fish 1s infinite linear alternate;
}
```

앞뒤로 왔다갔다 하는 물고기 이미지

### ✅ media-query

> 핸드폰에서 보이는 화면(작은 화면에서)

```css
div {
  opacity: 0;
}

@media screen and (max-width: 300px) {
  div {
    opacity: 1;
  }
}
```

```html
<div>화면이 300px보다 작습니다. 화면 크기를 키워주세요.</div>
```
