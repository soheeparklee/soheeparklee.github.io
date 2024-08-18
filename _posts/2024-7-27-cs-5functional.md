---
title: Functional/Sequential/Procedural/Imperative/Declarative Programming
categories: [Computer Science, CS_Basics]
tags: [] # TAG names should always be lowercase
---

<img width="663" alt="Screenshot 2024-08-14 at 00 29 40" src="https://github.com/user-attachments/assets/840abfed-f718-435b-bbbb-c022169a962f">

## ❤️ Imperative 명령형

> 🆚 Declarative <br>
> focus more on **how** <br>

- Procedural Programming
- OOP

## 💙 Declarative 선언형

> 🆚 Imperative <br>
> program by expressing logic of computation withoug talking about control flow <br>
> focus more on **what** needs to be done than how <br>
> declare the result we want <br>

- Logic Programming
- Functional Programming
- Database

## ❤️ Procedural Programming 절차 지향

> **procedures** that perform specific tasks <br>
> sequence, steps, procedure <br>
> focuses on the **order** of procedures <br>

- if order changes, the result will change
- 👍🏻 similar to computer operation, fast in running
- C, Pascal, Fortran

## ❤️ OOP 객체 지향

> object: instance of class <br>
> organize code around object and their interaction <br>

- Encapsulation, Abstaction, Inheritence, Polymorphism
- 👎🏻 slower than procedual programming
- Java, C++, Python, Ruby

💡 <https://soheeparklee.github.io/posts/cs-4OOP/> <br>

## ❤️ Parallel Processing

- program instructions by dividing them among multiple processors

## 💙 Logic Programming

> abstract model of computation <br>
> knowledge and problem to solve <br>

## 💙 Functional Programming

> mathematical functions <br>
> pure functions: don't alter state or rely on external state <br>

- Pure functions
  - more than one pararmeter
  - no variable other than parameter
- Function composition
- Avoid shared state
- Avoid mutating state
- Avoid side effects

- Haskell, Scala, functional features in Python and JS

```javascript
var arr = [1, 2, 3, 4, 5];
var map = arr.map(function (x) {
  return x * 2;
}); // [2, 4, 6, 8, 10]
```

### ✔️ Functional Programming in JAVA

- lamda
- stream api
- functional interface

## ✅ Sequential Programming

> linear execution of instructions <br>
> each statement is executed in **order** <br>

- part of procedural programming

🆚 **Procedural Programming** <br>

- Procedural programming is a broader paradigm that includes sequential execution
- also involves organizing code into procedures
- include loops and conditionals
