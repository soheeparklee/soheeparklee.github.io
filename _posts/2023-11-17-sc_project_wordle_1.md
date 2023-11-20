---
title: Wordle Clone Coding
categories: [Project, Wordle Clone Coding]
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

## 1️⃣ 앱이 시작되면 실행되는 제일 중심이 되는 함수

```javascript
const appStart = () => {
  //이 안에 모든 로직들
};
```

## 2️⃣ 글자 입력되는 함수 handleKeyDown

### 키가 눌렸을 때, 어떤 키가 눌렸는지 알기

```javascript
const handleKeyDown = (event) => {
  //event.key는 a
  const key = event.key.toUpperCase();
  //event.keyCde는 65숫자
  const keyCode = event.keycode;
};

window.addEventListener("keydown", handleKeyDown);
```

### 키를 누르는 event

💡 eventListener은 항상 event를 암묵적으로 return한다.

```javascript
window.addEventListener("keydown", handleKeyDown);
```

### 💡 소문자를 대문자로 바꾸기 toUpperCase()

```javascript
const key = event.key.toUpperCase();
```

### 받아온 키를 박스 안에 입력되게 만들기

### 💡 class안에 속성 값 선택해서 뽑는 방법

```javascript
const thisBox = document.querySelector(
  `.box_block[data-index= "${attempts}${index}"]`
);
thisBox.innerHTML = key;
```

### 근데 알파벳 외의 키들은 안 돼

```javascript
if (65<= keyCode && keyCode <= 90){
    thisBox.innerHTML= key;
```

### 박스를 옆으로 한 칸 씩 올겨가기

```javascript
if (65 <= keyCode && keyCode <= 90) {
  thisBox.innerHTML = key;
  index = index + 1;
}
```

### 5개 글자 다 쓰면 입력 멈추고, `Enter`키만 눌려야 한다.

```javascript
  if (event.key === "Enter") {
        handleEnter();
```

### ✅ if문

**IF** 마지막 박스까지 갔니?

- `Enter`눌리면, 정답 확인하는 함수 호출하고
- `Delete`눌리면, 지우는 함수 호출하고
- 안 눌리면 함수return하고(아무일도 일어나지 않음)

**IF** 마지막 박스까지 안 갔니?

- 알파벳만 눌릴 수 있어.
- 알파벳이 눌리면 화면에 표시하세요.
- `Delete`가 눌리면 지우세요.

### ☑️ handleKeyDown CODE

```javascript
function appStart() {
  const handleKeyDown = (event) => {
    const key = event.key.toUpperCase();
    const keyCode = event.keyCode;

    const thisBox = document.querySelector(
      `.box_block[data-index= "${attempts}${index}"]`
    );

    if (index === 5) {
      if (event.key === "Enter") {
        handleEnter();
      } else if (event.key === "Backspace") {
        handleDelete();
      } else return;
    } else if (65 <= keyCode && keyCode <= 90) {
      thisBox.innerHTML = key;
      index = index + 1;
    } else if (event.key === "Backspace") {
      handleDelete();
    }
  };
  window.addEventListener("keydown", handleKeyDown);
}
```

## 3️⃣ Enter: 정답 확인하는 함수

위치, 단어 확인해야 정답인지 아닌지 알 수 있음

### `Enter`을 눌렀을 떄 정답 확인하기

워들의 정답과 client의 정답이 일치하는지 한 글자씩 확인해야 함.

```javascript
const handleEnter = () => {
  //정답을 확인하는 로직
};
```

### 한 단어의 n번째 알파벳 확인

**반복문**을 사용하여 배열의 [n]번쨰 가져와 비교  
`answer[i]`

### client가 어떤 단어를 입력해는지 알아오는 방법

```javascript
  for(let i=0; i<5; i++){
            //워들의 정답과 client의 정답이 일치하는지 한 글자씩 확인해야 함.
            //client가 입력한 답 한 글자씩 가져오는 방법
            const thisBox= document.querySelector(`.box_block[data-index= "${attempts}${i}"]`)
            const clientAnswer= thisBox.innerHTML;
```

### if문으로 정답 확인하면 ~실행

#### ▪️ 글자⭕️ 위치⭕️

##### 정답 = client이 입력한 답 글자⭕️ 위치⭕️ 박스 초록색으로

- 맞은 개수 +1

```javascript
(answer[i] === clientAnswer){
thisBox.style.backgroundcolor= rgb(106,169,100);
```

#### ▪️ 글자⭕️ 위치❌

### 💡 이 배열 안에 이 요소가 있나? => includes

자리는 틀렸지만 단어 내에 글자는 맞았음.

```javascript
answer.includes(clientAnswer);
//return true/false
```

### ☑️ handleEnter CODE

```javascript
const handleEnter = () => {
  let rightAnswer = 0;
  for (let i = 0; i < 5; i++) {
    //워들의 정답과 client의 정답이 일치하는지 한 글자씩 확인해야 함.
    //client가 입력한 답 한 글자씩 가져오는 방법
    const thisBox = document.querySelector(
      `.box_block[data-index= "${attempts}${i}"]`
    );
    const clientAnswer = thisBox.innerText;

    if (answer[i] === clientAnswer) {
      thisBox.style.background = "rgb(106,169,100)";
      rightAnswer = +1;
    } else if (answer.includes(clientAnswer)) {
      thisBox.style.background = "rgb(201,180,88)";
    } else {
      thisBox.style.background = "rgb(120,124,126)";
    }

    thisBox.style.color = "white";
  }
};
```

## 4️⃣ 다음줄로 넘어가는 함수

- enter눌렀을 때 다음줄로 넘어가도록
- handleEnter함수 맨 밑에다가 다음줄로 넘어가는 함수 추가
  - column의 숫자 하나 올려주기
  - index 초기화

### ☑️ nextLine CODE

```javascript
const nextLine = () => {
  attempts += 1;
  index = 0;
};
```

## 5️⃣ 게임 끝내기 함수

### 💡 removeEventListener

이벤트를 지워버리는 코드 `removeEventListener`

### ☑️ gameOver CODE

```javascript
const gameOver = () => {
  window.removeEventListener("keydown", handleKeyDown);
  return;
};
```

**언제 게임이 끝나야 하는가?**
두 가지 경우가 있을 것이다.

1.  답을 맞춘 경우
2.  답을 맞추지 못했지만 횟수를 다 쓴 경우

### 1. 5글자 다 맞았으면 게임 끝내기(win)

- handleEnter함수에다가 맞은 정답 개수 variable 추가
- 맞은 정답 개수 variable = 5

handleEnter함수에서 답이 맞으면 gameOver호출, 아니면 다음 줄로 넘어가기 if문

```javascript
if (rightAnswer === 5) {
  gameOver() gameWin();
} else nextLine();
```

### ☑️ gameWin CODE

```javascript
const gameWin = () => {
  const winDiv = document.createElement("div");
  document.body.appendChild(winDiv);
  winDiv.innerText = "You Won";
  winDiv.style =
    "display:flex; justify-content:center; align-items:center; position:absolute; top: 50vh; left: 50vw;";
};
```

### 2. 6번 시도했는데 다 틀렸으면 게임 끝내기(lost)

- nextLine 함수에서 attempts = 6이면 게임 끝, 졌음

```javascript
const nextLine = () => {
  attempts += 1;
  index = 0;
  if (attempts === 6) {
    gameLost();
    gameOver();
  }
};
```

### ☑️ gameLOST CODE

```javascript
const gameLost = () => {
  const failDiv = document.createElement("div");
  document.body.appendChild(failDiv);
  failDiv.innerText = "You Lost";
  failDiv.style =
    "display:flex; justify-content:center; align-items:center; position:absolute; top:50vh; width:50vw;";
};
```

## 6️⃣ `DELETE` 눌렀을 때 지워지기

지금 index에서 두 번 `DELETE`를 눌러야 지워져서,  
미리 index를 하나 줄여서 preBox에 넣었다.  
그리고 index가 마이너스가 되면 안되니까! (그런건 존재하지 않음)  
index >0 이라는 조건을 달아줌.

### ☑️ deleteCODE

```javascript
let interval;

const handleDelete = () => {
  if (index > 0) {
    const preBox = document.querySelector(
      `.box_block[data-index= "${attempts}${index - 1}"]`
    );
    preBox.innerHTML = "";
    index -= 1;
  } else return;
};
```

## 7️⃣ 게임 타이머

### 타이머를 멈추는 방법

`setInterval`은 `ID`를 return하는 함수임.
interval이라는 변수에 `setInterval`을 저장하면 interval이 몇 번째 돌고 있는지 그 id를 return함.
gameOver 함수에 interval을 parameter로 전달

### ☑️ timer CODE

````javascript
function appStart(){
    const startTime= new Date();
    const timer= () =>{
        const timer= document.querySelector(".time");
        const currentTime= new Date();
        const passedTime= new Date(currentTime -startTime);
        const minutes= passedTime.getMinutes().toString().padStart(2, "0");
        const seconds= passedTime.getSeconds().toString().padStart(2, "0");
        timer.innerHTML= `${minutes}:${seconds}`
    }
    interval = setInterval(timer, 1000);
    ```

### ☑️ gameOver CODE
```javascript
const gameOver= () =>{
        window.removeEventListener("keydown", handleKeyDown);
        clearInterval(interval);
        return;
    }
````

## 💟 GITHUB

> version1

<https://github.com/soheeparklee/sc_project_wordle.git>

> version2

<https://github.com/soheeparklee/sc_project_wordle_improved.git>
