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

<img width="499" alt="Image" src="https://private-user-images.githubusercontent.com/97790983/437763825-80189631-0bb2-4fd6-bec0-e749a7dbf6c6.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDc4NjEyMjksIm5iZiI6MTc0Nzg2MDkyOSwicGF0aCI6Ii85Nzc5MDk4My80Mzc3NjM4MjUtODAxODk2MzEtMGJiMi00ZmQ2LWJlYzAtZTc0OWE3ZGJmNmM2LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA1MjElMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwNTIxVDIwNTUyOVomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTZjNGVlZmFlNWNlZWI4YmM1M2Y4ZWZhYmIyZTI3ZGFiN2E2ZGUwZmIxNzg3NmE4MzUwZTNhMTYyNWE2ZjQ2NWEmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.CUtIfNG1WfTmtXNAy1QLoBgiewGp825473lp8CoM5DA" />

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
