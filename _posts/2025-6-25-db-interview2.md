---
title: Interview_SQL
categories: [Database, DB]
tags: [] # TAG names should always be lowercase
---

## ✅ Can you explain what SQL is and how it differs from programming languages like C?

- Structured Query Language: declarative language to interact with RDB
- used to manage RDB
- such as `INSERT`, `DELETE`, `SELECT`, `UPDATE`
- DBMS manages how to run query
- `what to find in DB`

- C: procedural lanaguage for software development
- programmer defines control flow
- `how to do smth`

## ✅ How is an SQL query executed in a DBMS like MySQL?

- **1. SQL Request**: client ➡️ request to MySQL server
- `connection handler` accepts request

- **2. Query Parser**: break down query, construct `parse tree`
- check for syntax error

- **3. Preprocessor**: validate logical structure
- check for referenced table/column, if table/columns really exists
- check for permission

- **4. Optimizer**: generate execution plan, choose the most efficient
- use index
- join algorithm, full table scan

- **5. Query Execution Engine**: execute query by interacting with appropriate `storage engine(InnoDB)`
- execute query that is optimized by `Optimizer`
- return result to client

## ✅ What is DML and what are its key statements?

> Data Manipulation Language <br>

- manage data within existing table
- can be rolled back

- ✔️ **SELECT**: get data

```sql
SELECT name FROM student WHERE age > 20;
```

- ✔️ **INSERT**: add new record

```sql
INSERT INTO student (id, name, age) VALUES (1, 'John', 20);
```

- ✔️ **UPDATE**:

```sql
UPDATE student SET age = 21 WHERE id = 1;
```

- ✔️ **DELETE**:
- ✔️ **WHERE**: filter
- ✔️ **LIMIT**:
- ✔️ **ORDER BY**: sort
- ✔️ **AS**: assign aliases to columns for readability

## ✅ What is DDL and what types of statements does it include?

> Data Definition Language <br>

- define, modify schema(structure) of DB
- cannot be rolled back

- ✔️ **CREATE**:
- ✔️ **ALTER**: modify existing structure

```sql
ALTER TABLE student ADD gender CHAR(1);
```

- ✔️ **DROP**: permanently delete table
- ✔️ **TRUNCATE**: delete all data without logging each row
- faster then DELETE(does not leave log)
- but cannot rollback(does not leave log)
- reset `auto_increment`

## ✅ What is DCL and what are its commands?

> Data Control Language

- manage access permission of DB

- ✔️ **GRANT**: give previleges

```sql
GRANT SELECT ON student TO 'user1'@'localhost';
```

- ✔️ **REVOKE**: remove granted previleges

```sql
REVOKE SELECT ON student FROM 'user1'@'localhost';
```

## ✅ What is TCL and what commands does it include?

> Transaction Control Langauge

- manage transactions
- ensure ACID

- ✔️ **COMMIT**: save all changes in transaction
- after `COMMIT`, cannot rollback

- ✔️ **ROLLBACK**: cancel transaction, revert changes

- ✔️ **SAVEPOINT**: create a checkpoint to rollback partially

```sql
BEGIN;
INSERT INTO student VALUES (1, 'Alice', 22);
SAVEPOINT s1;
UPDATE student SET age = -1 WHERE id = 1;
ROLLBACK TO s1;
COMMIT;
```

## ✅ What is referential integrity?

- 🟰 foreign key constraint
- foreign key always refers to existing primary key in another table
- data consistency

- 👍🏻 prevent orphan records
- 👍🏻 enforce data integrity

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);
```

## ✅ What is a foreign key?

- constraint used to link to tables
- one column of table references primary key of another table

## ✅ Why is foreign key + referential integrity so important?

- 👍🏻 maintain data consistency
- 👍🏻 reduce redundancy
- 👍🏻 support cascading behavior

```
Imagine User, Order table
- if user is deleted but order remains, order will become orphan data
- if there is no referential integrity, have to save phone, address both on User and Order, and have to update both
```

## ✅ What is CASCADE in a foreign key? What are its pros and cons?

- `CASCADE`: changes in `parent table` affects the `child table`
- option to keep **referential integrity**

- `ON DELETE CASCADE`: delete child when parent is deleted
- `ON UPDATE CASCADE`: update child when parent key changes

## 💡 Why is CASCADE risky?

- 👎🏻 can lead to unintended deletions
- 👎🏻 data flow is hard to trace

- should use `CASCADE` only when child data is fully owned by parent
- 💊 handle cascading behavior explicitly in application code with `if`, `persist()`, `remove()`
- make control flow more transparent

## ✅ What is a VIEW in SQL?

- **virtual table** to see table
- does not store data itself, but returns results based on table

```sql
CREATE VIEW active_students AS
SELECT name, age FROM student WHERE status = 'active';
```

- 👍🏻 simple query

## ✅ What’s the difference between a VIEW and a TABLE?

- ✔️ `VIEW`: no physical storage
- always reflect current state
- slower than `TABLE`
- simple
- does not show origial table, more secure

```sql
CREATE VIEW engineering_employees AS
SELECT id, name, salary
FROM employees
WHERE department = 'Engineering';
```

- ✔️ `TABLE`: physically stored on disk
- faster

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    department VARCHAR(50),
    salary INT
);
```

## ✅ What is the execution order of a SELECT statement?

- `FROM`: from what table?, `JOIN` is also processed here
- ⭐️ `WHERE`
- ⭐️ `GROUP BY`
- ⭐️ `HAVING`
- ⭐️ `SELECT`
- `DISTINCT`
- `ORDER BY`
- `LIMIT`

## ✅ What does `SELECT ... FOR UPDATE` do? ❌

- used in transaction
- to **lock selected rows for update**
- no other transactions cannot modify them until the current transaction ends
- prevent other transactions from modifying them
- 👍🏻 ensure data consisitency
- 👍🏻 prevent race conditions
- 👍🏻 prevent deadlock

```sql
BEGIN;

SELECT * FROM coupons
WHERE id = 101 AND claimed = FALSE
FOR UPDATE; -- lock!

-- Check if the coupon is available
-- If so, mark it as claimed
UPDATE coupons
SET claimed = TRUE, claimed_by = 'user123'
WHERE id = 101;

COMMIT;
```

## ✅ What does the GROUP BY clause do? ❌

- group rows that have same values in specified columns
- normally, followed by `SUM`, `AVG`, `COUNT` and get result

```sql
SELECT product, SUM(amount) AS total_sales
FROM sales
GROUP BY product;
```

- get `SUM` of all grouped `product`
- if table was `banana = 10`, `apple = 5`, `banana = 20`
- get `banana = 30`, `apple = 5`
- grouped by products, get SUM of sales

## ✅ What does the ORDER BY clause do?

- sort by `ASC` or `DESC`

## ✅ What is the difference between INNER JOIN and OUTER JOIN?

- both `JOINs` use `ON` to join the tables

- ✔️ **INNER JOIN**: return only rows that **both** tables have

- ✔️ **OUTER JOIN**: return all rows from one table, plus matching rows from the other
- if there is no match, return `null`
  - ✔️ **LEFT JOIN**: all rows from left table ➕ matched rows from right table
  - ✔️ **RIGHT JOIN**: all rows from right table ➕ matched rows from left table
  - ✔️ **FULL OUTER JOIN**: all rows from both tables

## ✅ What is the difference between LEFT OUTER JOIN and RIGHT OUTER JOIN?

- ✔️ **LEFT OUTER JOIN**: all rows from left table ➕ matched rows from right table
- if no match, `null`

- ✔️ **RIGHT OUTER JOIN**:all rows from right table ➕ matched rows from left table
- if no match, `null`

## ✅ What is a CROSS JOIN?

- ✔️ **CROSS JOIN**: every row from first table will be combined with every row from the second table
- 모든 경우의 수를 반환
- if table A has 3 rows, table B has 2 rows ➡️ result = `3 * 2 = 6`
- 👍🏻 useful for generating combinations, but result size might be very big

## ✅ What is a subquery?

- query within another query
- used in `SELECT`, `WHERE`, `FROM`
- `JOINs` are often preferred over subqueries

```sql
SELECT name FROM users
WHERE id IN (SELECT user_id FROM orders WHERE amount > 100);

```

## ✅ What are the differences between DROP, TRUNCATE, and DELETE?

- 🔥 **DROP**: complete remove table ➕ data, cannot rollback
- ‼️ **TRUNCATE**: remove all rows, but keep structure, faster than delete, cannot rollback
- ⚠️ **DELETE**: delete rows based on condition, can rollback

## ✅ What is DISTINCT? Have you used it?

- remove duplicate rows
- return only unique combinations
- example: generate unique lists, like a dropdown of categories without repetition

```java
SELECT DISTINCT country FROM users;
```

## ✅ What is an SQL Injection and how do you prevent it?

- **SQL Injection**: attackers inject malicious SQL through input fields
- get unauthorized access, manipulate data

- 💊 use prepared statement
- 💊 use parameterized queries
- 💊 validate, sanitize user input
- 💊 apply least privilege

## ✅ Do you know any SQL anti-patterns?

- 👎🏻 `SELECT*`: bring unnecessary data
- 👎🏻 ignoring data types: for example, comparing `String` to `number`, causing implicit casting, breaking indexing
- 👎🏻 use wildcard `LIKE %value%`: prevent index use, result in full table scan
- 👎🏻 overuse, misuse index
- 👎🏻 relying on subqueries instead of `JOIN`

## ✅ How would you write a pagination query in SQL?

- use `LIMIT` and `OFFSET`
- `OFFSET`: where data starts
- `LIMIT`: how many rows
- if `LIMIT = 5, OFFSET = 10`: column 11~15

- 👎🏻 `OFFSET` must scan and skip all previous rows before reaching target
- not good for large datasets

## ✅ How do you implement pagination without using OFFSET?

- 💊 use cursor
- `last_seen_id` is cursor to get to the next page
- ensure we only fetch new rows after the cursor
- can use when data is `sorted`

```sql
SELECT * FROM posts WHERE id < last_seen_id ORDER BY id DESC LIMIT 10;
```

## ✅

## ✅
