---
title: 2023.SEPT.24(FRI) 슈퍼코딩 부트캠프 신입연수원 Day 10
categories: [TIL(Today I Learned), SuperCoding_신입연수원(주특기 선택 이전)]
tags: [todayilearned, til]
---

## ✅ Daily Report

### 📌 **TO-DO LIST**

- [x] submit github blog post
- [ ] 54
- [ ] 55
- [ ] 56
- [ ] 57
- [ ] assigment: SQL while VS having
- [ ] assigment: practice SQL1
- [ ] assigment: practice SQL 2
- [ ] assigment: left INNER JOIN

      <br>
      <br>

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

```javascript
SELECT OrderDetails.ProductID, Orders.OrderDate, OrderDetails.Quantity FROM OrderDetails
INNER JOIN Orders ON OrderDetails.OrderID = Orders.OrderID;
```

### SQL practice 2

### SQL JOIN
