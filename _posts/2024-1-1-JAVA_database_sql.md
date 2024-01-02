---
title: SQL commands
categories: [Data, SQL]
tags: [sql] # TAG names should always be lowercase
---

SQL은 데이터 지향적 모델링, 행위가 없음 <br>
반면 JAVA는 객체 지향적(또는 행위 지향) 모델링<br>
<br>
✔️ SQL에서는 DB를 schema라고 부른다.<br>
✔️ DB끼리 연결되어 있기 때문이다.<br>
<br>

- column: 열 🟰 필드 🟰 attribute <br>
- row: 행 🟰 레코드 <br>
  row단위로 데이터가 의미를 가진다. <br>
  (고객 아이디, 이름, 성별, 전화번호 등등이 모여서 의미를 가짐.) <br>

### ✅ SQL commands

#### ✔️ DDL

Data Definition Language<br>
DB, schema 수준의 작업<br>
데이터베이스에서 뭔가를 하거나<br>
table 생성, 삭제, 컬럼 변경...<br>
컬럼을 수정하거나...<br>

- CREATE: DB 생성
- ALTER
- DROP
- RENAME
- TRUNCATE

#### ✔️ DML

Data Manipulation Language <br>
DB데이터(=레코드) 수준의 작업 <br>
데이터를 다루는 명령어 <br>
데이터 조회, 삽입, 업데이트, 삭제 등... <br>

- SELECT
- INSERT
- UPDATE
- DELETE

### ✅ SQL 데이터 형식

MYSQL 데이터형식이 다르면 그만큼 RAM/DISK 낭비 <br>
효율차이가 심해지므로 데이터 형식을 맞춰주는 것이 중요하다. <br>

가변형 타입: 좀 넉넉하게 데이터 타입 주었다가 실제로는 더 작은 데이터가 들어오면 알아서 용량을 줄인다. <br>

- Varchar
- Text
- binary

#### Char/String

- Varchar <br>
  길이가 고정되지 않은 데이터 <br>
  VARCHAR(6) 해도 3개의 데이터 들어오면 3칸만 차지 <br>
  이메일 주소, 집 주소 <br>

- Char <br>
  길이가 고정된 데이터 <br>
  CHAR(6) 해도 3개의 데이터만 들어와도 6칸 다 차지 <br>
  주민등록번호, 우편번호 <br>

- Text <br>
  Varchar, Char로 커버할 수 없는 글자 수 <br>
  영화 리뷰, 자기소개서 등 <br>

#### Numeric

자바랑 비슷 int

#### Date/Time

- DATE `YYYY-MM-DD` <br>
- TIME `HH-MM-SS` <br>
- DATETIME `YYYY-MM-DD-HH-MM-SS` <br>
  시간대 정보 없음 <br>
  시간 범위 넓은 <br>
- TIMESTAMP `YYYY-MM-DD-HH-MM-SS` <br>
  현재 시간대로 변경되어 저장 <br>
  1970년부터 2038년까지만 가능 <br>

#### Blob

사진, 동영상 저장 위함 <br>

#### Binary

- binary <br>
