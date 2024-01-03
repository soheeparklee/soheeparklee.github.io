---
title: 2024.JAN.2(TUE) JAVA DAY 22
categories: [TIL(Today I Learned), SuperCoding_JAVA]
tags: [todayilearned, til, sql, databse]
---

## ✅ CREATE, INSERT INTO, UPDATE

```SQL
CREATE TABLE product(
	product_name CHAR(4),
    price INT,
    make_date DATE,
    company CHAR(5),
    amount INT
    );

DESC product;

INSERT INTO product
VALUES
('ap', 2000, '2023-02-05', 'comp2', 30),
('pot', 1000, '2023-01-01', 'comp1', 50);

SET SQL_SAFE_UPDATES=0;

SELECT * FROM super_codingDB.product;
UPDATE product
SET price = 6000, amount= 10
WHERE product_name= 'pot';
```
