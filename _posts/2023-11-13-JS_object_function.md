---
title: Object, Boolean, Function
categories: [Javascript, JS_Basics]
tags: [object, boolean, function] # TAG names should always be lowercase
---

## Object

```javascript
const Sohee= {
    name: sohee,
    gender: female,
    age: 123,
    job: programmer,
    adress:
}

```

```javascript
console.log(Sohee.job);
```

programmer

```javascript
Sohee.hobby = swimming;
console.log(Sohee.hobby);
```

swimming

## Boolean

- true
- false
- undefined: 존재하지 않는다
- null: 존재는 하나 값이 없다

```javascript
console.log(Sohee.name === sohee);
```

true

```javascript
console.log(Sohee.adress);
```

null

```javascript
console.log(Sohee.nationality);
```

undefined

## Function

### How to define a Function

Arrow function

```javascript
const add = (a, b) => a + b;
```

Function expression

```javascript
const add = function (a, b) {
  return a + b;
};
```

### Function & Object

> console.log으로 보여주는 함수 만들기

```javascript
    const caculator= {
        add: function (a, b) {
            console.log("a+b" = a+b);
        },
        //화살표 함수
        minus: (a, b) => {
            console.log("a-b" = a-b);
        }
    }

caculator.add(10+20)

```

30

> return 은 값을 반환\
> 그래서 그 값을 변수에 저장하였음

```javascript
const caculator = {
  add: function (a, b) {
    return a + b;
  },
  //화살표 함수
  minus: (a, b) => {
    return a - b;
  }
};

const result = caculator.add(10 + 20);
console.log(result);
```
