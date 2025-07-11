---
title: Interview_Schema, Instance, 3-level, RDBMS, Key, Integrity
categories: [Database, DB]
tags: [] # TAG names should always be lowercase
---

## ✅ 파일시스템과 데이터베이스의 차이점에 대해서 설명해주세요.

- **파일시스템**: manage data in files
- create, delete, update, search files
- 👎🏻 data redundancy: 같은 데이터가 여러번 중복해서 서로 다른 파일에 저장
- 👎🏻 data consistency
- 👎🏻 data integrity: 데이터가 동일한 조건을 가져야 한다(비밀번호는 5글자 이상)
- 👎🏻 data concurrency
- 👎🏻 data dependency: 데이터 구성 방법, 물리적 저장 방법에 맞게 파일이 작성되어야 한다
- 응용 프로그램이 데이터 접근을 담당

- **데이터베이스**: 데이터를 **통합**하여 저장하는 software
- 파일 시스템의 `data redundancy`, `data dependency` 문제 해결
- 데이터베이스 DBMS가 데이터 접근을 담당함

## ✅ 데이터베이스의 특징에 대해 설명해주세요.

✔️ **Data in database should be...**

- shared data
- integrated data: does not allow data redundancy
- stored data
- operational data

✔️ **Database should be...**

- 1️⃣ real-time accessibility
- 2️⃣ continuous evolution: database should keep changing, updating real life data
- 3️⃣ concurrent sharing: several users should be able to access at the same time
- 4️⃣ contens reference: should be able to search data content with value

## ✅ DBMS는 뭘까요? 특징에 대해 설명해주세요.

> Database Management System

- DBMS가 데이터베이스의 데이터 생성, 접근 및 `삽입, 삭제, 수정, 검색`을 담당
- 사용자는 요청만 하고, **DBMS가 데이터베이스와 관련된 작업 수행** 후 결과만 반환
- 응용 프로그램 ↔ DBMS ↔ 데이터베이스
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

- **data redundancy** problem sovled
- **data independent**: not influenced by data structure
- **data concurrency**: DBMS has tools to control concurrent access
- **security**: 권한 가진 유저만 데이터 접근 가능, 접근 수준 차별화 가능
- **data integrity**: accuracy of data, update/input of data is gone through integrity test in DBMS
- standarize data management
- debug
- no need to develop database application(DBMS manages data)

## ✅ Disadvantages of database

- high cost
- backup, rollback difficult
- central control can lead to huge failure

## ✅ What is a Schema?

- schema: define **stucture** of a database
- `table`, `field`, `relationships`, `constraints`...
- like a **blueprint** for how data is organized
- 데이터베이스에 저장되는 `데이터 구조`와 `제약조건`을 정의한 것
- 일반적으로 `conceptual schema`를 의미

```SQL
CREATE TABLE Student (
  student_id INT PRIMARY KEY,
  name VARCHAR(100),
  major VARCHAR(50)
);
```

- this SQL defines a schema

<img width="569" alt="Image" src="https://github.com/user-attachments/assets/39a76a4d-8084-4344-b39b-a95ad815bffb" />

## ✅ 인스턴스란 뭘까요?

- **actual data** stored in DB at the specific moment time
- actual rows that are inserted

- 정해진 스키마에 의해 데이터베이스에 실제로 저장된 값
- 보통 스키마는 한번 정해지면 잘 변하지 않지만
- 인스턴스는 자주 바뀜

## ✅ Explain the Three-Level Database Architecture.

- 3단계 데이터베이스 구조: 하나의 데이터베이스를 3단계로 나눠서 쉽게 이해하자
- 데이터가 어떻게 저장되고 유지되는지 복잡한 내용 숨기고, 필요한 데이터만 단순화해서 일반 사용자에게 제공
- separate uder view from physical data storage
- 👍🏻 enable **abstraction, independence**

- 외부단계로 갈수록 abstraction level higher ⬆️
- 👍🏻 복잡한 내용 숨기기
- 👍🏻 불필요한 데이터 접근 방지

- ✔️ **external level**: individual user view
- ✔️ **conceptual level**: organizational view/logical view
- ✔️ **internal level**: physical storage view

<img width="712" alt="Image" src="https://github.com/user-attachments/assets/0469df98-98c5-4ed5-bba5-72bf50c431c5" />

#### ☑️ external level

> how **user** sees the DB application <br>
> HR employee sees employee names, department, Finance sees salaries

- 고객 관리 담당 직원은 고객 데이터에만 관심이 있고
- 상품 담당 직원은 상품 데이터에만 관심이 있다
- *개별 사용자*가 데이터베이스를 어떻게 보는지는 자신의 관심사에 따라 다르다
- `external schema(sub schema)`: `external level`에서 사용자에게 필요한 데이터베이스를 정의한 것
- 사용자마다 생각하는 데이터베이스 구조 `external schema`는 다르다

#### ☑️ conceptual level

> entire database structure <br>
> describe `entity`, `data type`, `relationship`, `constraints`

- 데이터베이스를 사용하는 사용자들의 관점을 통합해
- *조직 전체의 관점*에서 DB표현
- `conceptual schema`: 조직 전체 관점에서 표현한 DB의 논리적 구조
- DBMS 또는 데이터베이스 관리자 관점에서 모든 사용자에게 필요한 데이터를 하나로 합쳐서 표현
- DB당 하나의 `conceptual schema`만 존재
- ➕ 데이터 관계, 제약 조건, 데이터 보안 정책, 접근 권한도 포함

- 각 사용자는 `conceptual schema`의 일부분 사용
- 따라서 `external schema(sub schema)`는 `conceptual schema`를 토대로 사용자의 목적에 맞게 만들어지는 것

#### ☑️ internal level

> how data is physically stored on disk <br> > `file structure`, `index`, `compression`...

- `internal schema`: 저장장치에 실제로 DB가 저장되는 방법을 정의
- DB는 저장장치에 파일형태로 저장
- `internal schema`에는 파일을 구성하는 레코드 구조, 필드 크기, 인덱스 등 정의
- DB당 하나의 `internal schema`만 존재

## ✅ schema mapping이란?

- relationship between schemas
- `external schema` should be mapped to `conceptual schema`, and `conceptual schema` should be mapped to `internal schema`
- 그래야지 사용자가 물리적 저장 장치에 저장된 데이터 접근 가능

```
  +---------------------------+
  |    External Schema(s)     | ← User views (e.g., view for HR)
  +---------------------------+
             ↓ Mapping
  +---------------------------+
  |     Conceptual Schema     | ← Logical data model
  +---------------------------+
             ↓ Mapping
  +---------------------------+
  |      Internal Schema      | ← Physical storage
  +---------------------------+
```

## ✅ 3단계 데이터베이스 구조 & schema mapping의 목적은?

- 👍🏻 data independence: change in DB stucture will not affect users
- 👍🏻 security
- 👍🏻 more simple: HR employee do not have to know about DB physicial details
- 👍🏻 easier to maintain: isolation between levels allow easier updates

## ✅ What is Data Independence?

> capacity to change schema at one level of DB without changing other levles

- 파일 시스템은 파일 구조가 바뀌면 응용 프로그램도 함께 수정해야 함
- DBMS가 데이터베이스에 대해 책임을 지기 때문에
- 데이터의 논리적 구조나 물리적 구조가 변경되더라도 응용 프로그램이 영향을 받지 않는 것
- 즉, **하위 스키마를 변경하더라도 상위 스키마가 영향을 받지 않는 특성**

<img width="620" alt="Image" src="https://github.com/user-attachments/assets/470fdb9b-7d9a-4892-8b4c-fd6e875fd551" />

## ✅ What is Logical Independence?

- `external schema(sub schema)` will not be influenced even when `conceptual schema`is changed
- user does not have to know `database logical structure` has been changed
- **application interface**: relationship betwen `external schema(sub schema)` and `conceptual schema`

```
conceptual schema에서 데이터 이름이 연락처 ➡️ 전화번호로 바뀜
external schema의 mapping만 전화번호로 수정해주면
external schema에서는 데이터 이름 여전히 연락처
external schema를 변결할 필요가 없다
```

## ✅ What is Physical Independence?

- changes to `internal schema` will not affect `logical schema`
- even if developer changes storage from row-based to column-based, `conceptual schema` does not change

## ✅ What is an RDBMS? RDBMS(관계형 데이터베이스 관리시스템)는 뭘까요?

> DB that store data in tables with SQL

- create database into tables
- 👍🏻 easy structure to understand
- example: `oracle`, `MS SQL`, `MySQL`

- table-based
- relational model: use foreign keys
- data integrity: use constraints like foreign keys and primary keys
- transaction support: ACID
- minimize duplication of data: through normalization ❌
- access-control
- SQL query

<img width="711" alt="Image" src="https://github.com/user-attachments/assets/3d3d158c-2d1e-4a79-bacc-f2c86d2e0e1e" />

## ✅ What is Relation, Relation Schema and Relation Instance?

- ✔️ `Relation`: table of rows and columns
- data is saved in `relation`

- ✔️ `Relation Schema`: structure of the table
- `attribute(column)`, `domain(data types)`, `constraints`

```SQL
Student(student_id: INT, name: VARCHAR, major: VARCHAR)
```

- ✔️ `Relation Instance`: actual rows of data in table
- tuple
- cardinality

```SQL
+------------+----------+--------+
| student_id | name     | major  |
+------------+----------+--------+
| 1001       | Alice    | CS     |
| 1002       | Bob      | Math   |
+------------+----------+--------+
```

## ✅ What are Relation Degree and Cardinality?

- ✔️ **Relation Degree**: number of columns in a relation
- ✔️ **Cardinality**: number of rows

```SQL
Student(student_id, name, major) → Degree = 3
Rows in table = 1000 students → Cardinality = 1000
```

## ✅ What is a Key in RDBMS? (슈퍼키, 후보키, 기본키, 대리키, 외래키)

- 💡 **key**: constraint that ensures **uniqueness**
- help _identify_ rows(tuples)
- create _relations_

- ✔️ **Super key**: set of attribute that uniquely identifies tuples(rows)
- ✔️ **Candidate key**: minimal super key(no attribute can be removed)
- ✔️ **Primary key**: chosen candidate key used as main identifier, must be `unique` and `not null`
- ✔️ **Alternate key**: candidate key that is not selected as primary
- ✔️ **Surrogate key**: artificial key used when no natural key exists(auto-increment ID)
- ✔️ **Foreign key**: primary key in another table, enforcing reference integrity

## ✅ What are Integrity Constraints? 무결성 제약조건에 대해서 설명해주세요. (도메인 무결성, 개체 무결성, 참조 무결성)

- ✔️ **Domain Integrity**: column values are within valid domain
- `CHECK`, `NOT NULL`, `DEFAULT`

```sql
age INT CHECK(age >= 0)

-- age can only be INT, cannot be String
-- age can only be >=0
```

- ✔️ **Entity Integrity**: primary key is `not null`, `unique`
- 🟰 primary key constraint
- each row must be identifiable

- ✔️ **Referential Integrity**: foreign key references valid primary key
- 🟰 foreign key constraint

```sql
FOREIGN KEY (customer_id) REFERENCES Customer(customer_id)
```

## ✅ Database charecteristics

- ✔️ **MySQL**: structured, relational data
- user info, shoppingMall project
- support transactions, index, join
- `InnoDB`(ACID compliant)

- ✔️ **MongoDB**: semi-structured, large volume
- NoSQL, document based(JSON-like documents)
- good for parallel scalability
- `key-value` storage

- ✔️ **MariaDB**: RDBMS, open source MySQL
- after MySQL was aquired by Oracle, original developers created MariaDB to ensure free access
- sometimes faster than MySQL

## ✅ How does MySQL engine work?

- `MySQL server` 🟰 `MySQL engine` ➕ `storage engine`
- `MySQL server` is thread based, consisted of `foreground thread` and `background thread`

- `MySQL engine` refers to `storage engine` for MySQL
- manage save, search, update, delete data
- consisted of `connection handler`, `SQL parser`, `optimizer`, `Preprocessor`, `Query Execution Engine`

## ☑️ How does `API handler` work?

- interface to send query request to `storage engine`
- when query is run in `MySQL engine` , `API handler` sends the query to `storage engine`

## ☑️ What is `SQL query parser`?

- break query into token
- token: minimum unit that MySQL can understnad)
- make into tree
- find syntax error

## ☑️ What is `Preprocessor`?

- check structure errors based on `query parser`
- check if data exists
- check permissions

## ☑️ What is `Optimizer`?

- optimize how to run query
- use index here
- decide how to `join`, `full table scan`

## ☑️ What is `Query Execution Engine`?

- engine to run the SQL that is optimized by `Optimizer`
- call `storage engine` like `InnoDB`
- return result to client

## ✅ How does InnoDB work?

- `InnoDB` is the default `exect engine` for MySQL
- `InnoDB storage engine` manage **read, write** of disk

```sql
CREATE TABLE test_table (fd1 INT, fd2 INT) ENGINE=INNODB;
```

- has own buffer pool, cache system 👍🏻 fast read
- support record level lock 👍🏻 synchronizatoin
- support transaction
- support ACID
- ensure data integrity
