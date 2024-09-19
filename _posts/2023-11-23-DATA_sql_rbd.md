---
title: DBMS/ SQL(RDB)/ NoSQL
categories: [Database, DB]
tags: [sql, rdb]
---

## ✅ DBMS

> data base management sysmtem

- 다수가 동시에 DB에 접근가능하기 위해
- 에러 발생 시, DB복구 기능
- 빠른 DB검색 가능

✔️ **DDL** <br>

> data definition language <br>
> what purpose the database has <br>
> how it will be used <br>

- CREATE
- ALTER
- DROP
- RENAME

✔️ **DML** <br>

> data manipulation language <br>
> add, update, delete, search a database <br>

- SELECT
- INSERT
- UPDATE
- DELETE

✔️ **DCL** <br>

> data control language <br>

- GRANT
- REVOKE

## ✅ SQL

> Structured Query Language  <br>
> RDB <br>

## ✅ **RDB 관계형 데이터베이스**

자료가 행과 열로 테이블로 저장 <br>
이러한 테이블 간 관계를 가질 수 있어 <br>
테이블 끼리 연결과 참조가 가능하다 <br>

#### ☑️ 장점:

**1.구조화된 데이터:** <br>

- **정해진 데이터 스키마**에 따라 테이블에 저장
- 데이터는 **관계**를 통해 테이블에 분산 (중복을 피하기 위해)
- RDB는 테이블 구조를 가지고 있어 데이터를 구조화하고 정규화할 수 있습니다.
- 이로 인해 데이터의 일관성과 무결성이 유지됩니다. <br>

**2. 표준화된 질의 언어(SQL):** <br>

- SQL을 통해 데이터를 쉽게 조회, 추가, 수정, 삭제할 수 있습니다.
- 또한 다양한 DBMS에서도 호환성이 좋습니다. <br>

**3. 트랜잭션 지원:** <br>

- RDB는 ACID(원자성, 일관성, 고립성, 지속성) 원칙을 지원하여 안정적인 트랜잭션 처리가 가능합니다. <br>

#### ☑️ 단점:

**1. 확장성:** <br>

- 수직 확장(Scale-up)을 주로 지원
- 수평 확장(Scale-out)에 대한 지원이 제한적
- 이로 인해 대용량 데이터 처리나 분산 환경에서의 성능 저하가 발생할 수 있습니다. <br>

**2. 유연성 부족:** <br>

- 고정된 스키마로 인해 데이터 구조의 변경이 어렵습니다.
- 새로운 데이터 타입이나 구조 변경이 필요할 경우, 추가 작업이 필요합니다. <br>

## ✅ **NoSQL 비관계형 데이터베이스**

> 레코드: 문서 document
> 다른 구조의 데이터를 같은 컬렉션에 추가 가능하다.

#### ☑️ 장점:

**1. 확장성:** <br>

- NoSQL은 수평 확장(Scale-out)을 지원
  - 수직적 확장: 데이터베이스 서버의 성능 향상(CPU 업글레이드)
  - 수평적 확장: 더 많은 서버 추가, 데이터베이스 분산(하나의 데이터베이스 , 여러 호스트)
  - 수평적 확장은 NoSQL만 가능(SQL도 수직적 확장은 지원)

**2. 유연성:** <br>

- 고정된 스키마가 없어 데이터 구조의 변경이 용이합니다.
- 다양한 데이터 타입과 구조를 저장할 수 있어 개발 시간을 단축할 수 있습니다. <br>

**3. 다양한 데이터 모델:** <br>

- Key-Value, Document, Column-Family, Graph 등 다양한 데이터 모델을 지원
- 여러 상황에 적합한 솔루션을 선택할 수 있습니다. <br>

#### ☑️ 단점:

**1. 일관성:** <br>

- 대부분의 NoSQL 데이터베이스는 확장성을 위해 일관성을 희생하는 경향이 있습니다.
- CAP 이론에 따라 일부 데이터베이스는 데이터의 일관성을 보장하지 않을 수 있습니다. <br>

**2. 표준화된 질의 언어 부재:** <br>

- NoSQL에는 표준화된 질의 언어가 없어
- 각 데이터베이스마다 사용하는 질의 언어가 다릅니다.

- 이로 인해 새로운 데이터베이스를 사용할 때마다 새로운 질의 언어를 학습해야 할 수 있습니다. <br>

**3. 트랜잭션 지원 부족:** <br>

- NoSQL 데이터베이스 중 일부는 트랜잭션 처리를 지원하지 않거나 제한적으로 지원합니다.
- 따라서 복잡한 트랜잭션 처리가 필요한 경우 RDB보다 불리할 수 있습니다. <br>

## 🆚 RDB VS NoSQL

RDB는 표 형태, id를 찾거나 삭제 등 가장 많이 쓰이는 데이터베이스 <br>
Oracle, SQLite, Derby 등 <br>
<br>

NoSQL은 관계형 데이터베이스와 달리 안에도 종류 다양 <br>
NoSQL이란 표준화된 구조적 질의 언어가 없는 데이터베이스 또는 관계를 갖지 않는 데이터베이스 <br>
(Nonrelational Operational Database SQL) <br>

> When to use RDB?
>
> > when connected data is frequently altered
> > in NoSQL, has to change several collections with connected data

> When to use NoSQL?
>
> > when developer does not know exact data architecture
> > read frequently from database, but not frequent alternation of database
> > need to scale-out database

## 🆚 SQLite VS MongoDB

### SQLite

**장점** <br>
사용하는 메모리 공간이 적다. <br>  
이식성이 뛰어나 전송이 쉽다. <br>
임베디드 어플리케이션에 적합합니다. 이식성 ⬆️ 이후 확장할 필요 없음 <br>
애플리케이션이 파일을 디스크에 직접 읽고 쓰는 경우 <br>
테스트환경 <br>
<br>

**단점**
동시성 제한(하나의 프로세스만이 데이터베이스 변경 가능) <br>
따라서 높은 볼륨 쓰기가 요구되는 경우 부적합합니다. <br>
사용자 관리가 없어 특별한 액세스 권한 줄 수 없음 <br>
따라서 보안에 취액 <br>
많은 데이터가 요구되는 경우 부적합 <br>
네트워크 액세스가 요구되는 경우 부적합 <br>
<br>

### MongoDB(NoSQL)

**장점** <br>
NoSQL의 장점 Schema-less 그대로(유연성, 확장성, 고성능, 가용성) <br>
비 트랜잭션(commit, rollback없고 모두 autocommit) <br>
데이터 입출력시 JSON(JavaScript Object Notation)형태, 데이터 저장시 BSON(JSON데이터를 이진 형식으로 인코딩한 포멧)형식 <br>
<br>

**단점** <br>
데이터 업데이트 중 장애가 발생하면!!! 데이터 손실 가능 <br>
많은 메모리 데이터 필요 <br>
트랜잭션이 필요한 애플리케이션의 경우 부적합 <br>
<br>
