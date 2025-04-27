---
title: Open Closed Principle
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ OCP

- **Open** for extension: new code should be able to be extended
  - 확장에는 열려있고
- **Closed** for modification: old code must not be modified
  - 변경에는 닫혀있어야 한다

## ✅ How to implement OCP

- implement interface
- implement extends, abstract class

- even if a new car is added, `open new class`,
- driver class is not altered `closed for modification`

<img width="499" alt="Image" src="https://github.com/user-attachments/assets/80189631-0bb2-4fd6-bec0-e749a7dbf6c6" />

- distinguish `code to be added` and `code not to be modified`
- `open` : NewCar class 추가
- `closed`: Driver class, Car interface는 변하지 않음

## ✅ Strategy pattern

- have an interface
- and several classes that implement interface
- even if a new class is added, do not need to modify existing old classes
- easy to add a new class instance

## ✅

## ✅

## ✅

## ✅

## ✅
