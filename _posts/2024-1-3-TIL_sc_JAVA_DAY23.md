---
title: 2024.JAN.03(WED) JAVA DAY 23
categories: [TIL(Today I Learned), SuperCoding_JAVA]
tags: [todayilearned, til, sql, databse]
---

#### ❓ RDB에서 하나의 몽땅 테이블이 아닌 개체를 나타내는 개개의 테이블과 그 관계로 구성하는 대표적인 이유 3가지 설명해주세요.

하나의 테이블로 나타내면 유지 보수가 어렵고 데이터 간 관계를 나타내기 어렵기 때문이다. <br>
개체를 나타내는 개개의 테이블로 만들고 그 테이블 간 관계를 규정하므로써 데이터 간 관계를 효율적으로 나타낼 수 있다. <br>

- 데이터 중복 최소화 <br>
- 데이터 일관성 보장 <br>
- 데이터 효율적 관리 <br>

#### ❓ SQL의 DDL과 DML 에 대해 각각 간단하게 설명하고 각각에 속하는 SQL 명령어들을 나열해주세요.

DDL은 data definition language의 약자로, 테이블 생성, 삭제, 행, 열 생성, 삭제, 수정과 연관이 있다. 명령어로는 CREATE, ALTER, DROP, TRUNCATE 등이 있다. <br>
DML은 data modificcation language의 약자로, 테이블 내 데이터의 입력, 수정, 삭제와 연관이 있다. 명령어로는 SELECT, INSERT, UPDATE, DELETE 등이 있다. <br>

#### ❓ SQL의 데이터 타입에는 가변형이라는 개념이 있습니다. 가변형이 왜 필요한지, CHAR과 VARCHAR의 예시를 비교하여 설명해주세요.

SQL의 데이터 타입에는 VARCHAR, TEXT, BOOLEAN 등의 가변형이 있다. 이는 예상한 값보다 실제 값이 더 작게 들어왔을 때, 데이터타입 형태를 실제 입력된 값에 맞게 줄여 저장공간을 절약하기 위함이다. 그래서 길이가 고정되어 있는 값은 기본형으로, 정해지지 않은 값은 가변형으로 설정하면 좋다. 그러나 기본형에 비해 속도가 느리다는 단점이 있다. <br>

#### ✅ 인사팀에 속한 직원들 중 경력(experience)이 3년 이상인 직원들의 이름(name)과 경력(experience)을 조회하세요. 결과는 경력(experience)이 높은 순서대로 정렬되어야 합니다.

```sql
SELECT name, experience
FROM employees
WHERE department = '인사팀'
GROUP BY name, experience
HAVING experience >=3
ORDER BY experience DESC;
```

#### ✅ 각 부서별로 평균 연봉(salary)과 최고 연봉(salary)을 조회하세요. 결과는 부서 이름을 가나다 순으로 정렬되어야 합니다. ( 단, 평균은 1의 자리 숫자로 반올림 )

```sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department
ORDER BY department ;

SELECT department, MAX(salary)
FROM employees
GROUP BY department
ORDER BY department ;

-- 합치기 가능
SELECT department, ROUND(AVG(salary)), MAX(salary)
FROM employees
GROUP BY department
ORDER BY department ;
```
