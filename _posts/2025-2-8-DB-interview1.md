---
title: 데이터베이스 개론_Database/ schema/ RDBMS/ Key
categories: [Database, DB]
tags: [] # TAG names should always be lowercase
---

## ✅ 파일시스템과 데이터베이스의 차이점에 대해서 설명해주세요.

- 파일시스템: manage data in files
- create, delete, update, search files
- 👎🏻 data redundancy: 같은 데이터가 여러번 중복해서 서로 다른 파일에 저장
  - 👎🏻 data consistency
  - 👎🏻 data integrity: 데이터가 동일한 조건을 가져야 한다(비밀번호는 5글자 이상)
  - 👎🏻 data concurrency
- 👎🏻 data dependency: 데이터 구성 방법, 물리적 저장 방법에 맞게 파일이 작성되어야 한다
- 응용 프로그램이 데이터 접근

- 데이터베이스: 데이터를 **통합**하여 저장하는 software
- 파일 시스템의 `data redundancy`, `data dependency` 문제 해결
- 데이터베이스 DBMS가 데이터 접근을 담당함

## ✅ 데이터베이스의 특징에 대해 설명해주세요.

✔️ **Data in database should be...**

- shared data
- integrated data: does not allow data redundancy
- stored data
- operational data

✔️ **Database should be...**

- real-time accessibility
- continuous evolution: database should keep changing, updating real life data
- concurrent sharing: several users should be able to access at the same time
- contens reference: should be able to search data content with value

## ✅ DBMS는 뭘까요? 특징에 대해 설명해주세요.

> Database Management System

- DBMS가 데이터베이스의 데이터 생성, 접근 및 `삽입, 삭제, 수정, 검색`을 담당
- 사용자는 요청만 하고, DBMS가 데이터베이스와 관련된 작업 수행 후 결과만 반환
- 모든 응용 프로그램이 데이터베이스 공유할 수 있게 함

- 👍🏻 data redundency problem solved
- 👍🏻 data concurrency problem solved
- 👍🏻 user does not need to care about database physical problems, how to alter data
- 👍🏻 data independency

## ✅ DBMS의 기능

- ✔️ 정의 기능: DBMS는 데이터베이스 구조 정의
- ✔️ 조작 기능: DBMS는 데이터 `삽입, 삭제, 수정, 검색`
- ✔️ 제어 기능: 데이터 공유 문제 해결, 권한 있는 사용자만 접근 가능하도록 보안 유지, data integrity

## ✅ Advantages of database

- data redundancy problem sovled
- data independency: not influenced by data structure
- data concurrency: DBMS has tools to control concurrent access
- security: 권한 가진 유저만 데이터 접근 가능, 접근 수준 차별화 가능
- data integrity: accuracy of data, update/input of data is gone through integrity test in DBMS
- standarize data management
- debug
- no need to develop database application(DBMS manages data)

## ✅ Disadvantages of database

- high cost
- backup, rollback difficult
- central control can lead to huge failure

## ✅ 스키마가 뭘까요?

- 데이터베이스에 저장되는 `데이터 구조`와 `제약조건`을 정의한 것

```
user_id: INT
name: CHAR(10)
age: INT
address: CHAR(20)
```

<img width="569" alt="Image" src="https://github.com/user-attachments/assets/39a76a4d-8084-4344-b39b-a95ad815bffb" />

## ✅ 인스턴스란 뭘까요?

- 정해진 스키마에 의해 데이터베이스에 실제로 저장된 값
- 보통 스키마는 한번 정해지면 잘 변하지 않지만
- 인스턴스는 자주 바뀜

## ✅ 3단계 데이터베이스 구조에 대해 설명해주세요.

## ✅ 데이터 독립성에 대해서 설명해주세요.

- 파일 시스템은 파일 구조가 바뀌면 응용 프로그램도 함께 수정해야 함
- DBMS가 데이터베이스에 대해 책임을 지기 때문에 구조가 변경되어도 응용 프로그램이 영향을 받지 않는다

## ✅ RDBMS(관계형 데이터베이스 관리시스템)는 뭘까요?

- create database into tables
- 👍🏻 easy structure to understand
- oracle, MS SQL, MySQL

<img width="711" alt="Image" src="https://github.com/user-attachments/assets/3d3d158c-2d1e-4a79-bacc-f2c86d2e0e1e" />

## ✅ 릴레이션 스키마와 릴레이션 인스턴스에 대해서 설명해주세요.

## ✅ 릴레이션의 차수와 카니덜리티에 대해 설명해주세요.

## ✅ 키(Key)에 대해서 설명해주세요. (슈퍼키, 후보키, 기본키, 대리키, 외래키)

## ✅ 무결성 제약조건에 대해서 설명해주세요. (도메인 무결성, 개체 무결성, 참조 무결성)

## ✅ 사용했던 데이터베이스에 대해서 설명해주세요. (오라클DB, MySQL, MariaDB, MongoDB 등)

## ✅

## ✅

## ✅

## ✅

## ✅
