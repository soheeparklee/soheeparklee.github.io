---
title: 2024.JAN.04(THU) JAVA DAY 24
categories: [TIL(Today I Learned), SuperCoding_JAVA]
tags: [todayilearned, til, sql, databse, coalesce]
---

#### 경기 출신 그룹 중, 가장 많은 수량을 구매한 상품의 상품 이름과 그 수량을 조회하는 SQL 쿼리를 작성하세요.

```sql
SELECT G.mem_name, B.prod_name, G.addr, SUM(B.amount)
FROM buy_history B
JOIN group_singer G
ON B.mem_id= G.mem_id
WHERE G.addr = '경기'
GROUP BY G.mem_name, B.prod_name
ORDER BY SUM(B.amount) DESC
LIMIT 1;
```

#### 가수 그룹별로 구매한 상품들과 그들의 수량을 모두 조회하는 SQL 쿼리를 작성하세요.

만약 가수 그룹에 해당하는 구매 이력이 없는 경우에 결과에 0이 표시되어야 합니다. <br>
( 참고: **COALESCE:** 인자를 중 NULL이 아닌 첫 번째 인자를 반환하는 함수입니다. ) <br>

```sql
SELECT B.prod_name, G.mem_name, SUM(B.amount)
FROM group_singer G
LEFT OUTER JOIN buy_history B
ON B.mem_id = G.mem_id
GROUP BY G.mem_name,B.prod_name;
```

⭐️ 만약 amount에는 0이 뜨도록 하고 싶다면 **COALESCE** <br>

```sql
SELECT B.prod_name, G.mem_name, COALESCE(B.amount, 0)
FROM group_singer G
LEFT OUTER JOIN buy_history B
ON B.mem_id = G.mem_id
ORDER BY G.mem_name,B.prod_name;
```
