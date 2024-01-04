---
title: SQL datatype, commands
categories: [Data, SQL]
tags: [sql, insert, select, where, order, having, ddl, dml] # TAG names should always be lowercase
---

🆚 SQL은 데이터 지향적 모델링, 행위가 없음 <br>
반면 JAVA는 객체 지향적(또는 행위 지향) 모델링<br>
<br>
✔️ SQL에서는 DB를 schema라고 부른다.<br>
✔️ DB끼리 연결되어 있기 때문이다.<br>
<br>

- column: 열 🟰 필드 🟰 attribute <br>
- row: 행 🟰 레코드 <br>
  row단위로 데이터가 의미를 가진다. <br>
  (고객 아이디, 이름, 성별, 전화번호 등등이 모여서 의미를 가짐.) <br>

## ✅ SQL 데이터 형식

MYSQL 데이터형식이 다르면 그만큼 RAM/DISK 낭비 <br>
효율차이가 심해지므로 데이터 형식을 맞춰주는 것이 중요하다. <br>

⭐️ **가변형 타입:** 좀 넉넉하게 데이터 타입 주었다가 실제로는 더 작은 데이터가 들어오면 알아서 용량을 줄인다. <br>

- Varchar
- Text
- binary

#### ✔️ Char/String

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

#### ✔️ Numeric

자바랑 비슷 int

#### ✔️ Date/Time

- DATE `YYYY-MM-DD` <br>
- TIME `HH-MM-SS` <br>
- DATETIME `YYYY-MM-DD-HH-MM-SS` <br>
  시간대 정보 없음 <br>
  시간 범위 넓은 <br>
- TIMESTAMP `YYYY-MM-DD-HH-MM-SS` <br>
  현재 시간대로 변경되어 저장 <br>
  1970년부터 2038년까지만 가능 <br>

#### ✔️ Blob

사진, 동영상 저장 위함 <br>

#### ✔️ Binary

- binary <br>

## ✅ SQL commands

### ✔️ DDL

Data Definition Language<br>
DB, schema 수준의 작업<br>
데이터베이스에서 뭔가를 하거나<br>
table 생성, 삭제, 컬럼 변경...<br>
컬럼을 수정하거나...<br>

`CREATE`: DB 생성 <br>
`ALTER` <br>
`DROP` <br>
`RENAME` <br>
`TRUNCATE` <br>

### ✔️ DML

Data Manipulation Language <br>
DB데이터(=레코드) 수준의 작업 <br>
데이터를 다루는 명령어 <br>
데이터 조회, 삽입, 업데이트, 삭제 등... <br>

`SELECT` <br>
`INSERT` <br>
`UPDATE` <br>
`DELETE` <br>

## ☑️ SQL commands exmaple

```sql
AUTO_INCREMENT //자동 증강
PRIMARY KEY //기본키
NOT NULL //비울 수 없음
```

```sql
CREATE TABLE member(
	member_id INT AUTO_INCREMENT PRIMARY KEY,
	  mem_name VARCHAR(10) NOT NULL,
    mem_number INT ,
    addr VARCHAR(30),
    phone CHAR(12),
    height TINYINT UNSIGNED,
    enroll_date DATETIME
);

DESC member; -- add comment like this
```

### ☑️ DDL

#### 💡 ALTER

✔️ add column <br>

```sql
ALTER TABLE netflix
ADD COLUMN release_date DATE AFTER movie_title; -- add column
```

✔️ update column <br>

```sql
ALTER TABLE netflix
MODIFY COLUMN movie_director VARCHAR(100) NOT NULL; -- update column
```

✔️ delete column <br>

```sql
ALTER TABLE netflix
DROP COLUMN movie_script; -- delete column
```

#### 💡 DROP, TRUNCATE

DROP: table 자체를 완전 삭제 <br>
TRUNCATE: table의 내용물 삭제 <br>

### ☑️ DML

#### 💡 INSERT

```sql
INSERT INTO member (mem_name, mem_number, addr, phone, height, enroll_date)
VALUES ('Kim', 1, 'Seoul', 010, 160, '2024-01-01 10:00:00'),
		('Park', 3, 'Gimpo', 010, 180, '2024-01-01 11:00:00'),
		('Jang', 7, 'Anyang', 010, 190, '2024-01-01 10:00:00'),
		('Sin', 5, 'Mokdong', 010, 130, '2024-01-01 10:00:00'),
		('Lee', 2, 'Busan', 010, 170, '2024-01-01 13:00:00');
```

#### 💡 UPDATE & WHERE

WHERE 없으면 다 수정됨... <br>

```sql
UPDATE member
SET addr= 'NewYork'
WHERE mem_name= 'Kim';

SET SQL_SAFE_UPDATES = 0;
```

#### 💡 DELETE & WHERE

WHERE 없으면 다 지워짐... <br>
만약 WHERE 안 쓰면 TRUNCATE랑 같음 <br>

```sql
DELETE FROM member WHERE mem_name= 'Lee';
```

🆚 **DELETE TUNCATE DROP** <br>
DELETE: where 써서 조건 만족하는 한 행씩 지우기 <br>
TUNCATE: 표의 열은 남겨두고 내용(행)은 지우기, auto_increment도 초기화 <br>
DROP: 모든 행과 테이블 삭제 <br>

## 💡 SELECT

### ☑️ SELECT 구문 작성 순서

- SELECT
- FROM
- WHERE
- GROUP BY
- HAVING
- ORDER BY

### ☑️ SELECT 내부 실행 순서

- FROM + JOIN
- WHERE
- GROUP BY
- HAVING
- SELECT
- ORDER BY
- LIMIT

#### ✔️ WHERE, BETWEEN, IN, LIKE

- BETWEEN
- IN
- %
  글자수 상관 없음
- LIKE\_\_
  글자수 제한 있음

```sql
SELECT *
FROM group_singer
WHERE height >= 180;

SELECT *
FROM group_singer
WHERE height > 160 AND height < 170;

SELECT *
FROM group_singer
WHERE height BETWEEN 160 AND 170; -- same code as before

SELECT *
FROM group_singer
WHERE addr IN ('경기', '경남');

```

```sql
SELECT *
FROM group_singer
WHERE mem_name LIKE '아'; --아이유, 아일랜드 등등

SELECT *
FROM group_singer
WHERE mem_name LIKE '아__';  -- 아이유(아 뒤에 2글자만 올 수 있음)
```

#### ✔️ ORDER BY, ASC, DESC, LIMIT, DISTINCT

❗️ 적는 순서에 유의하자! <br>

##### ➖ ORDER BY

```sql
SELECT *
FROM group_singer
WHERE mem_number < 6
ORDER BY debut_date DESC;

-- 💥 만약 순서바뀌면 실행 ❌
--SELECT *
--FROM group_singer
--ORDER BY debut_date DESC
--WHERE mem_number < 6;
```

##### ➖ LIMIT

```sql
SELECT mem_name, debut_date
FROM group_singer
ORDER BY debut_date ASC
LIMIT 3;
```

```sql
SELECT mem_name, debut_date
FROM group_singer
WHERE mem_number > 4
ORDER BY debut_date ASC
LIMIT 5,3; --5번쨰부터 3개 가져오기
```

##### ➖ DISTINCT

DISTINCT는 SELECT뒤에서 쓰인다. <br>
몇 개의 선택지가 있는지 확인할 떄 유용하다. <br>

```sql
SELECT DISTINCT  addr
FROM group_singer
ORDER BY addr; --경기, 서울, 경남, 전남, 충북 출력
```

#### ✔️ GROUP BY, SUM, AVERAGE, HAVING, COUNT

##### ➖ GROUP BY

데이터를 모아서 보여준다. <br>
구매이력에서 이 사람이 여러 차례 물건을 샀는데(GROUP BY), 몇 번 샀는지 다 더하기(SUM) <br>

```sql
SELECT mem_id, SUM(amount)
FROM buy_history
GROUP BY mem_id;

SELECT mem_id, SUM(price * amount) -- 얼마짜리를 몇 번 샀는지, 총 비용 구하기
FROM buy_history
GROUP BY mem_id;

SELECT mem_id, SUM(price * amount) AS total_price --출력되는 컬럼명을 바꿀 수 있음
FROM buy_history
GROUP BY mem_id;
```

##### ➖ AVG

```sql
SELECT mem_id, AVG(price * amount) AS average
FROM buy_history
GROUP BY mem_id;
```

##### ➖ COUNT

개수 세어 준다. <br>

```sql
SELECT COUNT(*) -- mem001이 총 몇 개 샀는지 개수 세어 준다.
FROM buy_history
WHERE mem_id = 'mem001';

SELECT mem_id, COUNT(*) --각 아이디별로 총 몇 개 샀는지 개수 구하기
FROM buy_history
GROUP BY mem_id;
```

##### ➖ HAVING

특정 그룹 핑 데이터 특정하기 <br>
**WHERE절이 GROUP BY보다 먼저 실행되기 때문에 생기는 문제 해결** <br>
HAVING문으로 조건식을 특정할 수 있다. <br>

```sql
-- SELECT mem_id, SUM(amount * price) AS total_price
-- FROM buy_history
-- WHERE SUM(amount * price) > 10000; --WHERE이 GROUPBY보다 먼저 실행되서 이 코드는 불가능
-- GROUP BY mem_id;

-- HAVING 으로 해결
SELECT mem_id, SUM(amount * price) AS total_price
FROM buy_history
GROUP BY mem_id
HAVING SUM(amount * price) > 10000;
```
