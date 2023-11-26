---
title: 2023.SEPT.24(FRI) 슈퍼코딩 부트캠프 신입연수원 Day 10
categories: [TIL(Today I Learned), SuperCoding_신입연수원(주특기 선택 이전)]
tags: [todayilearned, til]
---

## ✅ Daily Report

### 📌 **TO-DO LIST**

- [x] submit github blog post
- [x] 54
- [x] 55
- [x] 56
- [x] 57
- [x] assigment: SQL while VS having
- [x] assigment: practice SQL1
- [x] assigment: practice SQL 2
- [x] assigment: SQL JOIN

## ✅ Today I Learned

### SQL WHERE VS HAVING

#### WHERE

그룹 전체에 조건 적용  
exclude individual rows from groups  
apply a condition to individual rows  
Only the rows that meet the conditions in the `WHERE` clause are grouped.  
일반적으로 테이블의 열(컬럼)과 관련된 조건을 기반으로 데이터를 선택하거나 제외  
SELECT, UPDATE, DELETE 문에서 사용

```sql
-- 나이가 30세 이상인 직원 데이터만을 조회
SELECT * FROM employees WHERE age > 30;
```

#### HAVING

```sql
-- 부서별 직원 수가 10명 이상인 부서만을 조회
SELECT department, COUNT(*) as employee_count
FROM employees
GROUP BY department
HAVING employee_count > 10;
```

#### WHERE, HAVING common features

apply condition

```sql
SELECT titles.pub_id, AVG(titles.price)
FROM titles INNER JOIN publishers
   ON titles.pub_id = publishers.pub_id
WHERE publishers.state = 'CA'
GROUP BY titles.pub_id
HAVING AVG(price) > 10;
```

### SQL practice 1

```sql
SELECT OrderDetails.ProductID, Orders.OrderDate, OrderDetails.Quantity FROM OrderDetails
INNER JOIN Orders ON OrderDetails.OrderID = Orders.OrderID;
```

```sql
-- 같은 아이디를 가지는 product끼리 모은 후
-- product의 개수 총 몇 개인지 합쳐서 세기
-- 그리고 product개수 많은 순서대로 정렬하기

SELECT product_id, sale_amount FROM sales
GROUP BY product_id
ORDER BY SUM(sale_amount) DESC;
```

### SQL practice 2

```sql
-- 고객의 나이를 알기 위해 (올해 년도 - 태어난 연도)
-- 이 값을 FLOOR으로 감싸 1/2/3...등으로 구별
-- 그런 값을 age로 저장
-- 연령대별 고객 수를 알기 위해 COUNT함수
-- age로 GROUP BY하고
-- age순서대로 나열
SELECT FLOOR((birth_year-2023)/10) as age, COUNT(*) as customer_count FROM customers
GROUP BY age
ORDER BY age ASC;
```

### SQL JOIN

#### (INNER) JOIN

Returns records that have matching values in both tables  
두 테이블에 모두 있는 값

#### LEFT (OUTER) JOIN

Returns all records from the left table, and the matched records from theright table  
왼쪽 테이블에 있는 값, 그리고 오른쪽 테이블에서 일치하는 값  
만약 오른쪽 테이블에 일치하는 값이 없다면 오른쪽 테이블에서는 0개 불러올 것임.  
만약 오른쪽 테이블에 일치하는 값이 없어도 왼쪽 테이블에 있는 값들은 모두 return

```sql
SELECT column_name(s) FROM 왼쪽 테이블
LEFT JOIN 오른쪽 테이블 ON 왼쪽 테이블.column_name = 오른쪽 테이블.column_name;
```

#### RIGHT (OUTER) JOIN

Returns all records from the right table, and the matched records from the left table  
오른쪽 테이블에 있는 값 그리고 왼쪽 테이블에서 일치하는 값

#### FULL (OUTER) JOIN

Returns all records when there is a match in either left or right table  
오른쪽이나 왼쪽에서 하나라도 조건 만족하면 가져오기  
그러다보니 오른쪽에는 있는데 왼쪽에는 없는 값들도 가져오다 보니 셀 값이 NULL일 때도 많다.

💟 참조
<https://www.w3schools.com/sql/sql_join.asp>
