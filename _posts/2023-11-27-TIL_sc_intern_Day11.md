---
title: 2023.SEPT.27(MON) 슈퍼코딩 부트캠프 신입연수원 Day 11
categories: [TIL(Today I Learned), SuperCoding_신입연수원(주특기 선택 이전)]
tags: [todayilearned, til]
---

## ✅ Daily Report

### 📌 **TO-DO LIST**

- [x] submit github blog post
- [x] 58
- [x] 59
- [x] 60
- [x] 61
- [x] 62
- [x] 62
- [x] assigment: ERD 구현
- [x] assigment: mongoBD
- [x] assigment: chatApp 구현

## ✅ Today I Learned

### 유저 인증 Authentication

#### Session

- session: 유저의 정보를 DB에 저장해두었다가 그떄그떄 가져와 쓰는 방식

#### JSON Web Token

- JWT: 토큰에 base 64로 인코딩해 두었다가 사용
  토큰을 조회하면 사용자의 정보를 모두 알 수 있음
  확장성이 좋다.
  보안성은 refresh token으로 높일 수 있다. (일정 시간 지나면 refresh token 전송)

### RDB VS NoSQL

RDB는 표 형태, id를 찾거나 삭제 등 가장 많이 쓰이는 데이터베이스  
Oracle, SQLite, Derby 등  
NoSQL은 관계형 데이터베이스와 달리 안에도 종류 다양  
NoSQL이란 표준화된 구조적 질의 언어가 없는 데이터베이스 또는 관계를 갖지 않는 데이터베이스  
(Nonrelational Operational Database SQL)

### SQLite VS MongoDB

#### SQLite

**장점**  
사용하는 메모리 공간이 적다.  
사용자 친화적 RDBMS  
이식성이 뛰어나 전송이 쉽다.
임베디드 어플리케이션에 적합합니다. 이식성 ⬆️ 이후 확장할 필요 없음  
애플리케이션이 파일을 디스크에 직접 읽고 쓰는 경우  
테스트환경  
**단점**
동시성 제한(하나의 프로세스만이 데이터베이스 변경 가능)  
따라서 높은 볼륨 쓰기가 요구되는 경우 부적합합니다.  
사용자 관리가 없어 특별한 액세스 권한 줄 수 없음  
따라서 보안에 취액  
많은 데이터가 요구되는 경우 부적합  
네트워크 액세스가 요구되는 경우 부적합

#### MongoDB(NoSQL)

**장점**  
NoSQL의 장점 Schema-less 그대로(유연성, 확장성, 고성능, 가용성)  
비 트랜잭션(commit, rollback없고 모두 autocommit)  
데이터 입출력시 JSON(JavaScript Object Notation)형태, 데이터 저장시 BSON(JSON데이터를 이진 형식으로 인코딩한 포멧)형식
**단점**
데이터 업데이트 중 장애가 발생하면!!! 데이터 손실 가능  
많은 메모리 데이터 필요  
트랜잭션이 필요한 애플리케이션의 경우 부적합

## ☑️ Summary of the Day <br>

어제 미리미리 공부를 해 두었더니 오늘 조금 수월하다. 내일도 미리미리!! 파이팅!
