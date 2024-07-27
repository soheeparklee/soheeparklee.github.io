---
title: SQL contraints
categories: [Datanase, SQL]
tags: [unique, primary, check, default] # TAG names should always be lowercase
---

## ⭐️ Contraint

**데이터 무결성**을 지키기 위해 제약조건이 필요하다. <br>
입력되는 데이터 값을 제한한다. <br>
<br>
사람의 키는 음수가 될 수 없음.<br>
아이디는 null이 될 수 없음. ➡️ NOT NULL<br>
각각의 데이터는 중복되면 안 되는 경우도 있음. (아이디 같은 경우) ➡️ UNIQUE <br>

### 📣 선언 방식

제약에 따라 다르게 선언해야 하므로 선언 방식을 알아두어야 한다.<br>
<br>
1️⃣ CREATE할 때 inline 선언<br>
2️⃣ CREATE할 때 외부 제약 조건 선언<br>
3️⃣ ALTER문 사용할 떄 제약 조건 선언<br>

## ✅ NOT NULL contraint

해당 필드는 null이 될 수 없다.<br>

**📣 선언 방식:** 1️⃣ CREATE할 때 inline 선언<br>

```sql
CREATE table book_room_1
(
	id INT NOT NULL,
    name VARCHAR(30),
    reserve_date DATE,
    room_num INT
);

-- 방법 2: 외부 CONSTRAINT ❌
CREATE table book_room_2
(
	id INT NOT NULL,
    name VARCHAR(30),
    reserve_date DATE,
    room_num INT
	-- CONSTRAINTS id_not_null NOT NULL(id)
);

-- 방법 3: ALTER 방식 ❌
CREATE table book_room_3
(
	id INT,
    name VARCHAR(30),
    reserve_date DATE,
    room_num INT
);
-- ALTER TABLE book_room_4 ADD CONSTRAINT id_not_null NOT NULL(id);

DESC book_room_1;

INSERT INTO book_room_1 (id, name, reserve_date, room_num)
values (null, 'room1', '2022-01-11', 5);
-- 💥 null을 넣어서 동작 ❌
```

## ✅ UNIQUE contraint

두 필드가 같은 값을 가질 수 없음.<br>
해당 필드는 고유의 값을 가져야 한다.<br>
근데 null은 여러개 있어도 괜찮음.<br>

**📣 선언 방식:** 1️⃣ 2️⃣ 3️⃣ 방식 모두 가능하나, inline 선언이 제일 보편적<br>

```sql
-- 방법 1. 인라인 방식 ⭕️
CREATE TABLE book_room_4
(
	id INT UNIQUE,
    name VARCHAR(30),
    reserve_date DATE,
    room_num INT
);
-- 방법 2: 외부 제약 선언 ⭕️
CREATE TABLE book_room_5
(
	id INT,
    name VARCHAR(30),
    reserve_date DATE,
    room_num INT,
    CONSTRAINT id_unique UNIQUE(id),
    UNIQUE (name)
);


-- 방법 3: ALTER 사용 ⭕️
CREATE TABLE book_room_6
(
	id INT,
    name VARCHAR(30),
    reserve_date DATE,
    room_num INT
);
ALTER TABLE book_room_5
ADD CONSTRAINT id_unique UNIQUE(id);

DESC book_room_6;

INSERT INTO book_room_6 (id, name, reserve_date, room_num)
values (1, 'room1', '2022-01-11', 5);

-- 💥 불가능 , 위 코드에서 id=1 이미 있으니까
-- INSERT INTO book_room_4 (id, name, reserve_date, room_num)
-- values (1, 'room2', '2022-01-12', 6);

-- UNIQUE일 때 null은 가능 ⭕️
INSERT INTO book_room_4 (id, name, reserve_date, room_num)
values (null, 'room2', '2022-01-12', 6);

INSERT INTO book_room_4 (id, name, reserve_date, room_num)
values (null, 'room2', '2022-01-12', 6);


```

## ✅ PRIMARY KEY contraint

해당 필드는 NOT NULL 이고 UNIQUE <br>

### 🆚 NOT NULL, UNIQUE, PRIMARY KEY

NOT NULL, UNIQUE는 한 테이블에 여러개 가능하지만, PRIMARY KEY은 테이블 당 한 개만 존재할 수 있다.<br>

**📣 선언 방식:** 1️⃣ 2️⃣ 3️⃣ 방식 모두 가능하나, inline 선언이 제일 보편적<br>

```sql
-- 방법 1: 인라인 방식 ⭕️
CREATE TABLE book_room_7
(
	id INT PRIMARY KEY,
    name VARCHAR(30),
    reserve_date DATE,
    room_num INT
);

-- 방법 2: 외부 제약선언 ⭕️
CREATE TABLE book_room_8
(
	id INT,
    name VARCHAR(30),
    reserve_date DATE,
    room_num INT,
    CONSTRAINT id_pk PRIMARY KEY(id)
    -- PRIMARY KEY(id)
);

-- 방법 3: ALTER 사용 ⭕️
CREATE TABLE book_room_9
(
	id INT,
    name VARCHAR(30),
    reserve_date DATE,
    room_num INT
);
ALTER TABLE book_room_9
ADD CONSTRAINT id_pk PRIMARY KEY(id);

DESC book_room_9;

-- 값 넣기
INSERT INTO book_room_3 (id, name, reserve_date, room_num)
values (1, 'room1', '2022-01-11', 5);

-- 💥 불가능
INSERT INTO book_room_3 (id, name, reserve_date, room_num)
values (1, 'room2', '2022-01-12', 6);

-- 💥 불가능
INSERT INTO book_room_3 (id, name, reserve_date, room_num)
values (null, 'room2', '2022-01-12', 6);
```

## ☑️ CHECK contraint

해당 필드는 CHECK 안에 있는 조건문을 통과해야지만 테이블에 INSERT 가능<br>

**📣 선언 방식:** 1️⃣ 2️⃣ 3️⃣ 방식 모두 가능함<br>

```sql
-- 방식 1. 인라인 생성 ⭕️
CREATE TABLE member_1(
	mem_id INT AUTO_INCREMENT PRIMARY KEY,
    mem_name VARCHAR(10) NOT NULL,
    height TINYINT UNSIGNED CHECK( height >= 100 ),
    distict_phone CHAR(3) CHECK( distict_phone IN ( '02', '031', '032') )
);

INSERT INTO member_1 (mem_name, height)
VALUES ('이순신', 180);
-- 💥 동작 안함. 키 100 안 넘어서
INSERT INTO member_1 (mem_name, height)
VALUES ('이순신2', 90);

-- 방식 2. 외부 제약 조건 생성 ⭕️
CREATE TABLE member_2(
	mem_id INT AUTO_INCREMENT PRIMARY KEY,
    mem_name VARCHAR(10) NOT NULL,
    height TINYINT UNSIGNED,
    distict_phone CHAR(3) CHECK( distict_phone IN ( '02', '031', '032') ),

	CHECK ( height >= 100 )
);

-- 방식 3. ALTER ⭕️
CREATE TABLE member_3(
	mem_id INT AUTO_INCREMENT PRIMARY KEY,
    mem_name VARCHAR(10) NOT NULL,
    height TINYINT UNSIGNED,
    distict_phone CHAR(3) CHECK( distict_phone IN ( '02', '031', '032') )
);
ALTER TABLE member_1
ADD CONSTRAINT check_height CHECK( height >= 100 );

DESC member_1;
```

## ☑️ DEFAULT contraint

해당 필드가 null이면 DEFAULT값을 자동으로 넣어준다.<br>

**📣 선언 방식:** 1️⃣ CREATE할 때 inline 선언<br>

```sql
-- 방식 1. 인라인 생성
CREATE TABLE member_2(
	mem_id INT AUTO_INCREMENT PRIMARY KEY,
    mem_name VARCHAR(10) NOT NULL,
    height TINYINT UNSIGNED DEFAULT 160, -- NOT NULL 넣어도 DEFAULT로 동작함.
    distict_phone CHAR(3) DEFAULT '02'
);

-- 방식 2. 외부 제약 조건 생성 ❌
CREATE TABLE member_2(
	mem_id INT AUTO_INCREMENT PRIMARY KEY,
    mem_name VARCHAR(10) NOT NULL,
    height TINYINT UNSIGNED,
    distict_phone CHAR(3)
    -- CONSTRAINT default_height DEFAULT 160
);

-- 방식 3. ALTER 방식 ❌
CREATE TABLE member_2(
	mem_id INT AUTO_INCREMENT PRIMARY KEY,
    mem_name VARCHAR(10) NOT NULL,
    height TINYINT UNSIGNED,
    distict_phone CHAR(3) CHECK( distict_phone IN ( '02', '031', '032') )
);
-- ALTER TABLE member_2 ADD CONSTRAINT height DEFAULT 160;

INSERT INTO member_2 (mem_name) VALUES ('이순신');
INSERT INTO member_2 (mem_name) VALUES ('이순신2');
```

## ✅ FOREIGN KEY contraint

참조하는 테이블과 테이블의 필드가 필수적으로 존재하고 있어야 함.<br>
참조하는 필드는 **UNIQUE, PK** 필수<br>
<br>
**📣 선언 방식:**<br>
2️⃣ CREATE할 때 외부 제약 조건 선언<br>
3️⃣ ALTER문 사용할 떄 제약 조건 선언<br>

```sql
-- 방법 1: 인라인 생성 ❌
CREATE TABLE buy_history_1 (
	buy_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, -- 순번(PK)
	mem_id CHAR(8) NOT NULL ,
    -- FOREIGN KEY REFERENCES group_singer(mem_id), -- 아이디(FK)
    prod_name CHAR(6) NOT NULL, -- 제품 이름
    group_name CHAR(4), -- 분류
    price INT NOT NULL, -- 단가
    amount SMALLINT NOT NULL -- 수량
);

INSERT INTO buy_history_1 (mem_id, prod_name, group_name, price, amount)
VALUES ('mem001', '아메리카노', '음료', 2500, 2);

-- 방법2: 외부 제약 선언 ⭕️
CREATE TABLE buy_history_1 (
	buy_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, -- 순번(PK)
	mem_id CHAR(8) NOT NULL, -- 아이디(FK)
    prod_name CHAR(6) NOT NULL, -- 제품 이름
    group_name CHAR(4), -- 분류
    price INT NOT NULL, -- 단가
    amount SMALLINT NOT NULL, -- 수량

	CONSTRAINT mem_id_fk FOREIGN KEY(mem_id) REFERENCES group_singer(mem_id)
    -- ⭐️ 같은 의미, constraint 생략해도 잘 동작함
    -- FOREIGN KEY (mem_id) REFERENCES group_singer(mem_id)
);

-- 방법3: Alter 사용 ⭕️
CREATE TABLE buy_history_1 (
	buy_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, -- 순번(PK)
	mem_id CHAR(8) NOT NULL, -- 아이디(FK)
    prod_name CHAR(6) NOT NULL, -- 제품 이름
    group_name CHAR(4), -- 분류
    price INT NOT NULL, -- 단가
    amount SMALLINT NOT NULL -- 수량
);
ALTER TABLE buy_history_1
ADD CONSTRAINT mem_id_fk FOREIGN KEY(mem_id) REFERENCES group_singer(mem_id);
```

## ⭐️ CASCADE

FK가 참조하는 필드는 삭제, 수정할 때 주의해야 한다.<br>
따라서 FK가 있으면 **참조되는 테이블**에서도 제약이 걸림.<br>
이 제약을 풀기 위해서는 CASCADE<br>

**CASCADE:** 기존 테이블을 바꾸면 모두 연동된다.<br>

```sql
CREATE TABLE buy_history_1 (
	buy_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, -- 순번(PK)
	mem_id CHAR(8) NOT NULL, -- 아이디(FK)
    prod_name CHAR(6) NOT NULL, -- 제품 이름
    group_name CHAR(4), -- 분류
    price INT NOT NULL, -- 단가
    amount SMALLINT NOT NULL -- 수량
);

ALTER TABLE buy_history_1
ADD CONSTRAINT mem_id_fk2
FOREIGN KEY(mem_id) REFERENCES group_singer(mem_id)

-- ⭐️ CASCADE
ON UPDATE CASCADE
ON DELETE CASCADE;

ALTER TABLE buy_history_1
DROP CONSTRAINT mem_id_fk2;
```
