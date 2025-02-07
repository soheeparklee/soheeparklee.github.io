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
- 일반적으로 `conceptual schema`를 의미

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

- 3단계 데이터베이스 구조: 하나의 데이터베이스를 3단계로 나눠서 쉽게 이해하자
- 데이터가 어떻게 저장되고 유지되는지 복잡한 내용 숨기고, 필요한 데이터만 단순화해서 일반 사용자에게 제공
- 각 단계별로 abstraction
- 외부단계로 갈수록 abstraction level higher ⬆️
- 👍🏻 복잡한 내용 숨기기
- 👍🏻 불필요한 데이터 접근 방지

- ✔️ **external level**: individual user view
- ✔️ **conceptual level**: organizational view
- ✔️ **internal level**: physical storage view

<img width="712" alt="Image" src="https://github.com/user-attachments/assets/0469df98-98c5-4ed5-bba5-72bf50c431c5" />

#### ☑️ external level

- 고객 관리 담당 직원은 고객 데이터에만 관심이 있고
- 상품 담당 직원은 상품 데이터에만 관심이 있다
- *개별 사용자*가 데이터베이스를 어떻게 보는지는 자신의 관심사에 따라 다르다
- `external schema(sub schema)`: `external level`에서 사용자에게 필요한 데이터베이스를 정의한 것
- 사용자마다 생각하는 데이터베이스 구조 `external schema`는 다르다

#### ☑️ conceptual level

- 데이터베이스를 사용하는 사용자들의 관점을 통합해
- *조직 전체의 관점*에서 DB표현
- `conceptual schema`: 조직 전체 관점에서 표현한 DB의 논리적 구조
- DBMS 또는 데이터베이스 관리자 관점에서 모든 사용자에게 필요한 데이터를 하나로 합쳐서 표현
- DB당 하나의 `conceptual schema`만 존재
- ➕ 데이터 관계, 제약 조건, 데이터 보안 정책, 접근 권한도 포함

- 각 사용자는 `conceptual schema`의 일부분 사용
- 따라서 `external schema(sub schema)`는 `conceptual schema`를 토대로 사용자의 목적에 맞게 만들어지는 것

#### ☑️ internal level

- `internal schema`: 저장장치에 실제로 DB가 저장되는 방법을 정의
- DB는 저장장치에 파일형태로 저장
- `internal schema`에는 파일을 구성하는 레코드 구조, 필드 크기, 인덱스 등 정의
- DB당 하나의 `internal schema`만 존재

## ✅ schema mapping이란?

- relationship between schemas
- `external schema` should be mapped to `conceptual schema`, and `conceptual schema` should be mapped to `internal schema`
- 그래야지 사용자가 물리적 저장 장치에 저장된 데이터 접근 가능

## ✅ 3단계 데이터베이스 구조 & schema mapping의 목적은?

- 데이터 독립성

## ✅ 데이터 독립성에 대해서 설명해주세요.

- 파일 시스템은 파일 구조가 바뀌면 응용 프로그램도 함께 수정해야 함
- DBMS가 데이터베이스에 대해 책임을 지기 때문에
- 데이터의 논리적 구조나 물리적 구조가 변경되더라도 응용 프로그램이 영향을 받지 않는 것
- 즉, **하위 스키마를 변경하더라도 상위 스키마가 영향을 받지 않는 특성**

<img width="620" alt="Image" src="https://github.com/user-attachments/assets/470fdb9b-7d9a-4892-8b4c-fd6e875fd551" />

## ✅ 논리적 데이터 독립성이란?

- `external schema(sub schema)` will not be influenced even when `conceptual schema`is changed
- user does not have to know `database logical structure` has been changed
- **application interface**: relationship betwen `external schema(sub schema)` and `conceptual schema`

```
conceptual schema에서 데이터 이름이 연락처 ➡️ 전화번호로 바뀜
external schema의 mapping만 전화번호로 수정해주면
external schema에서는 데이터 이름 여전히 연락처
external schema를 변결할 필요가 없다
```

## ✅ 물리적 데이터 독립성이란?

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
