---
title: SQL 문법
categories: [Database, SQL]
tags: [sql]
---

## **SQL**

**SQL Structured Query Language**
관계형 데이터베이스 관리  
시스템에서 데이터를 관리하기 위해 사용되는 표준 프로그래밍 언어

### ✅ SQL Query Execution Order

![image](https://github.com/soheeparklee/sc_project_memo_improved/assets/97790983/bc4a178c-8e59-4679-bfc3-bd538509fc0f)

### ✅ SQL 문법

#### ✓ SELECT

The SELECT clause is executed to derive all desired columns and expressions.

```sql
SELECT * FROM (table);

SELECT Address FROM Customers;
```

#### ✓ FROM/JOIN

The FROM and/or JOIN clauses are executed first to determine the data of interest.  
두 테이블이 동일한 id를 공유하고 있어야 가능하다.

```sql
SELECT * FROM Orders JOIN Customers On Orders.CustomerId= Customers.CustomerId;

-- Orders테이블의 Orders.CustomerId와 Customers테이블의 Customers.CustomerId가 같은 애들을 합쳐 달라.
```

#### WHERE

조건문처럼 조건을 적용해 filtering  
The WHERE clause is executed to filter out records that do not meet the constraints.

```sql
SELECT ProductName, OrderDate, Quantity, Price FROM Orders;
WHERE Quantity > 10 and Price < 20;

-- 양이 10개 이상이고 가격은 20보다 작은  물건만 뽑기
```

#### GROUP BY

특정 컬럼(열)을 기준으로 그룹화
HAVING, COUNT와 자주 같이 사용
The GROUP BY clause is executed to group the data based on the values in one or more columns.

```sql
SELECT * FROM Customers GROUP BY Country;
-- customers를 country 별로 묶어서 보이도록

SELECT Country, COUNT(CustomerID) FROM Customers GROUP BY Country;
-- customers를 country 별로 묶은 다음, 몇 명인지? 세어보기
-- 그러면 한국 n명 이런 식으로 정리 가능
```

#### HAVING

특정 조건을 적용해 filtering
The HAVING clause is executed to remove the created grouped records that don’t meet the constraints.

```sql
SELECT Country, COUNT(CustomerID) FROM Customers
GROUP BY Country HAVING COUNT(CustomerID)>10;

-- 각 국가별 고객 수가 10명 이상인 곳
```

#### ORDER BY

특정 컬컴을 기준으로 정렬(많은 순서대로/적은 순서대로)  
ASC: 오름차순  
DESC: 내림차순  
The ORDER BY clause is executed to sort the derived values in ascending or descending order.

```sql
SELECT Country, COUNT(CustomerID) FROM Customers
GROUP BY Country ORDER BY COUNT(CustomerID) DESC;

-- 가장 많이 고객이 많은 나라부터 적은 나라까지 정렬
-- 데이터를 뽑아온 후 필요한 순서대로 정렬
```

#### LIMIT/OFFSET

LIMIT and/or OFFSET clauses are executed to keep or skip a specified number of rows.

```sql
SELECT Country, COUNT(CustomerID) FROM Customers
GROUP BY Country ORDER BY COUNT(CustomerID) DESC
LIMIT 10;

-- 제일 많은 고객이 있는 나라 top10개만 보여줘
```
