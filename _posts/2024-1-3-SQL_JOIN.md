---
title: JOIN
categories: [Data, SQL]
tags: [join, inner, outer] # TAG names should always be lowercase
---

table을 JOIN할 때, table끼리는 1:N 관계이다. <br>
FK로 JOIN한다. <br>
ON: join하는 조건인데, FK로 join <br>

## ✅ INNER JOIN

두 table간 **겹치는 부분을 return**하는 JOIN <br>
가장 기본적인 JOIN은 INNER JOIN <br>

```sql
SELECT *
FROM group_singer
INNER JOIN buy_history
ON buy_history.mem_id = group_singer.mem_id;  --mem.id로 연결(FK)
```

### alias 사용(줄임말)

```sql
SELECT G.mem_name, B.prod_name
FROM group_singer G
INNER JOIN buy_history B
ON B.mem_id = G.mem_id;
```

### sub query

서울/경기 출신 그룹 중, 소모한 비용 SUM이 10000이상 되는 그룹이 몇 개인지 반환 <br>

```sql
SELECT COUNT(*)
FROM(
SELECT G.mem_number, G.mem_id, G.addr, SUM(B.price) as total_price
FROM group_singer G
	INNER JOIN buy_history B
	ON G.mem_id = B.mem_id
WHERE G.addr IN('서울', '경기')
GROUP BY G.mem_id  -- FK로 GROUP BY하는 경우 많음
HAVING total_price > 10000
) sub; -- 안에 있는 표 내용을 sub라고 이름짓기
```

## ✅ OUTER JOIN

- LEFT JOIN <br>
  왼쪽 table에 있으면 무조건 넣어라. <br>
  합쳐지는 오른쪽 테이블에 값이 없어도 왼쪽 테이블에 있으면 무조건 <br>
  null 값이라도 넣기 <br>

- RIGHT JOIN <br>
- FULL JOIN <br>

```sql
SELECT {칼럼 목록}
FROM{기준 테이블}
<LEFT | RIGHT | FULL > OUTER JOIN {조인 대상 테이블}
ON {조건, FK}
```

```sql
SELECT *
FROM group_singer G
	LEFT OUTER JOIN buy_history B
	ON G.mem_id = B.mem_id;
```

#### 구매 목록이 없는 그룹 가수 중에서 평균키가 큰 순서대로 3명 반환

```sql
SELECT *
FROM group_singer G
	LEFT OUTER JOIN buy_history B
	ON G.mem_id = B.mem_id
WHERE B.price IS NULL
ORDER BY G.height DESC
LIMIT 3;
```

#### 구매 목록이 없는 가수는 총 몇 그룹인가?

```sql
SELECT COUNT(*)
FROM (
	SELECT G.mem_id
	FROM group_singer G
		LEFT OUTER JOIN buy_history B
		ON G.mem_id = B.mem_id
	WHERE B.price IS NULL
) sub; --Sub Query 이름 붙여주기
```

## ✅ Sub Query

쿼리 안에 또 쿼리 사용하기 <br>
⭐️ 만약 중복되는 column 명이 있다면 그 column을 없애기 위해 이름을 바꾸거나, alias로 바꾼다. <br>
⭐️ 또 Sub Query라고 새로운 이름을 붙여준다. <br>

## ✅ SELF JOIN

자기 자신 테이블을 참조 테이블로 둔다. <br>
무조건 alias를 강제적으로 사용해야 한다. <br>
내가 나를 참조하니까 이름 헷갈리므로 alias 쓰는 것이다. <br>

```sql
SELECT *
FROM employee E1
	JOIN employee E2
    ON E1.manager_id = E2.employee.id;
```

## ✅ CROSS 상호 JOIN

서로를 모두 참조해야 함. <br>
예를 들어 table A에 3개의 행이 있고, table B에 3개의 행이 있으면 3 \* 3= 9개 행 만들어진다. <br>
