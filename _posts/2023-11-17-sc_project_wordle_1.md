---
title: Wordle Clone Coding
categories: [Project, Clone Coding]
tags: [clonecoding, project, html, css, javascript, frontend]
---

## ✅ HTML

`class`외에도 `data-index`라는 것을 주어서 그 박스를 찾아가기 쉽도록 만들어 놓기

```html
<div class="box_row row_0">
  <div class="box_block" data-index="00"></div>
  <div class="box_block" data-index="01"></div>
  <div class="box_block" data-index="02"></div>
  <div class="box_block" data-index="03"></div>
  <div class="box_block" data-index="04"></div>
</div>
```

## ✅ 키가 눌렸을 때, 어떤 키가 눌렸는지 알기

### 키를 누르는 event

### 누른 키를 화면에 보이도록 만들기

### 근데 알파벳 외의 키들은 안 돼

### 소문자를 대문자로 바꾸기

## ✅ 박스를 옆으로 한 칸 씩 올겨가기

### 마지막 박스까지 갔으면 함수return

### 5개 글자 다 쓰면 `Enter`키만 눌려야 한다.

## ☑️ if문

마지막 박스까지 갔으면

- `Enter`눌리면, 정답 확인하는 함수 호출하고
- 안 눌리면 함수return하고

알파벳이 눌리면 화면에 표시하세요.

## ✅ 워들 정답과 user의 답을 확인하는 함수

위치, 단어 확인해야 정답인지 아닌지 알 수 있음

### `Enter`을 눌렀을 떄 정답 확인하기

### 한 단어의 n번째 숫자 확인하는 방법

### 글자⭕️ 위치⭕️ 박스 초록색으로

- 맞은 개수 +1

### 글자⭕️ 위치❌ 박스 똥색으로

> 자리는 틀렸지만 단어 내에 글자는 맞았음.
> 이 배열 안에 이 요소가 있나? => includes

### 아예 틀렸으면 박스를 회색으로

### if문 밖에 글자는 흰색, 테두리 없음

## ✅ 다음줄로 넘어가기

- column의 숫자 하나 올려주기
- index 초기화

## ✅ 게임 끝내기

`removeEventListener`

### 5글자 다 맞았으면 게임 끝내기

### 6번 시도했는데 다 클렸으면 게임 끝내기

## ✅ `DELETE` 눌렀을 때 지워지기

## ✅ 게임 타이머
