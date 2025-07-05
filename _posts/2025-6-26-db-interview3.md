---
title: Interview_Index, query execution plan, hint
categories: [Database, DB]
tags: [] # TAG names should always be lowercase
---

## ✅ What is the difference between random I/O and sequential I/O?

- **random I/O**: access data at arbitary locations on storage device
- no order
- 👎🏻 higher seek time
- 👎🏻 read/write head has to move more

- **sequential I/O**: access data in a continuous, ordered way
- 👍🏻 more efficient
- 👍🏻 minimize head movement

## ✅ What is an index in a database?

> data structure to help speed up data retrieval operation

- like a look up table
- like index of dictionary
- store `key value` ➕ `pointer` to corresponding rows

```
if use index
scan entire table ❌
use index to quickly locate data ⭕️
```

## ✅ How does an index work?

- index allow DB to **skip** full table scan

- B-Tree index: maintain balanced tree structure
- DB navigates through the tree to find target `key`, then access the associated `data`

- Hash index: use hash function to map `keys` to specific `buckets`

## ✅ What factors should you consider when creating an index?

- 1️⃣ Query patterns: add index to `WHERE`, `JOIN`, `ORDER BY`, `GROUP BY`
- 2️⃣ Selectivity: high selectivity = many unique values
- 3️⃣ Read vs. Write workload: index speed up reads, slow down writes
- 4️⃣ Table size: index is better for large tables
- 5️⃣ Sort, Group: index help sort, grouping columns
- 6️⃣ uniqueness: use `UNIQUE` index to enforce data integrity

```
When is index most efficient?
- 👍🏻 GROUP BY, ORDER BY
- 👍🏻 lots of unique values
- 👍🏻 read, not write
- 👍🏻 big table
```

## ✅ Is it good to create many indexes on a table?

- 👍🏻 faster read, faster query performance
- 👍🏻 optimized sort, grouping

- index also has trade-offs
- 👎🏻 slower write
- 👎🏻 increased storage usage
- 👎🏻 complexity in index management
- 👎🏻 risk of suboptimal execution plans due to too many choices

## 💡 What is a `covering index`?

> covering index: index that contains all the columns needed to satisfy a query <br>
> DB can answer the query just using index, WO accessing table

- index holds required data
- DB does not need to access actual table rows
- no table lookup
- 👍🏻 reduce I/O
- 👍🏻 faster read
- 👍🏻 efficient for read

```sql
CREATE TABLE users (
  id INT PRIMARY KEY,
  email VARCHAR(255),
  age INT
);

-- create covering index
CREATE INDEX idx_email_age ON users (email, age);

SELECT age FROM users WHERE email = 'john@example.com';
-- WHERE clause knows wmail
-- SELECT needs only age
-- index idx_email_age already has both email and age
```

## 💡 What is a `multi-column index` (or composite index)?

> multi-column index: single index that includes multiple columns from table <br>
> useful when queries filter or sort using more than one column

- when queries involve more than one column
- ⭐️ order of column matters
- index is most effective when query filters based on **leftmost columns first**

```
an index on (first_name, last_name) can efficiently support queries filtering on first_name or both, but not just last_name
```

- example of composite index

```sql
CREATE INDEX idx_email_age ON users (email, age);

-- ⭕️ efficient, use leftmost column
SELECT * FROM users WHERE email = 'john@example.com';

-- ⭕️ efficient, use both index columns
SELECT * FROM users WHERE email = 'john@example.com' AND age = 30;

-- ❌ not efficient, skips first column
SELECT * FROM users WHERE age = 30;
```

## 💡 What are nodes in `B-Tree` and `B+Tree` indexes?

- internal node: node that routes search paths
- leaf node: node that stores actual data(same leaf node, same depth)
- linked leaf nodes: `B+Tree` only, connected from left ➡️ right for range scanning

## 💡 Can you explain the difference between `B-Tree` and `B+Tree` indexes?

- 공통점: balanced tree structures used in indexing
- 차이점: how/where they store data
- InnoDB supports only `B-Tree index`

- **B-Tree**: store **key and actual data** in **both internal and leaf nodes**

- 👍🏻 fast point lookup
- 👎🏻 increase node size and I/O

```
internal node: store key ➕ data
leaf node: store key ➕ data
leaf connection: not linked
point lookup: fast
range query: slow(internal nodes are not linked)
use: old DBs
```

- example

```css
if DB is [5, 10, 15, 20, 25, 30, 35, 40]

           [15] /*internal node*/
          /    \
      [5,10]  [20,25,30] /*leaf nodes*/
                   \
                [35,40]
```

- **B+Tree**: store **only key in internal node**

- actual data resides in leaf nodes
- internal node and leaf nodes are **linked** together
- 👍🏻 fast range query
- 👍🏻 support sequential scans
- used as default in modern databases

```
internal node: only keys
leaf node: store key ➕ data
leaf connection: linked
point lookup: fast
range query:fast(leaces are linked)
use: modern RDBMS
```

- example

```css
if DB is [5, 10, 15, 20, 25, 30, 35, 40]

           [15] /*internal node: store only keys*/
          /    \
        [5,10]  [20,25]  /*leaf node: store key and data*/
                   \
                  [30,35]
                     \
                    [40]

Leaf node chain: [5,10] → [20,25] → [30,35] → [40] /*linked*/
```

- example of real-world query

```sql
CREATE INDEX idx_age ON users (age);

SELECT id, email
FROM users
WHERE age BETWEEN 20 AND 30
ORDER BY id;
```

## 💡 What is a `Hash index`, and when would you use it?

> use **hash function** to map `search keys` into `fixed-sized bucket number`

- hash function maps the `key` to `bucket number`
- `id = 15` ➡️ hash function ➡️ `Hash table bucket number 3`

- 👍🏻 equality search `WHERE id = 13`
- retrieve search data in constant time
- 👎🏻 not suitable for range query `ORDER BY`
- Why? hash function destroy natural ordering of data
- 👎🏻 not suitable for prefix match `LIKE 'abc%'`

- used in Memory tables or special DB
- `Hash index` is NOT used in InnoDB(MySQL)

## 💡 What is a `clustering index`?

> determine physical order of data in the table

- rows are stored on disk **in the same order** as index
- only ONE clustering index per table is possible
- Why? only one row can be `clustering index`
- (id순으로 정렬해둘지, 나이순으로 정렬해둘지, 날짜 순으로 정렬해 둘지 하나만 고를 수 있으니까)
- in InnoDB, `primary key` is `clustering index` by default

```
clustering index: created_at

+-----------------------------+
| posts Table (Physical Rows)|
+-----------------------------+
| id=9  | created_at=2023-01-01 |
| id=4  | created_at=2023-01-02 |
| id=12 | created_at=2023-01-03 |
| id=5  | created_at=2023-01-04 |
| id=7  | created_at=2023-01-05 |
+-----------------------------+
        ↑
   (physically sorted)
```

- 👍🏻 `RANGE queries` like `ORDER BY`
- 👍🏻 ordered scans are fast

```sql
SELECT * FROM posts
WHERE created_at BETWEEN '2023-01-02' AND '2023-01-04';
```

- leaf node of the clustering index store the **actual data rows** and **pointers**

## ✅ What is a non-clustering index?

- index that DOES NOT affect the physical order of data in the table
- instead, use `index columns`
- and `pointer`: point to where to find data in actual table row
- thus, only store `index` and `pointer`

```sql
email               → row location
------------------------------
alice@example.com   → row ID 1
bob@example.com     → row ID 2
carol@example.com   → row ID 3
```

- so when I query

```sql
SELECT * FROM users WHERE email = 'bob@example.com';

-- find email
-- then go to row ID 2 with pointer
-- then get user data
```

## ✅ What is a full-text index?

- specialized index used for searching large text data
- such as paragraph, documents
- support advanced text search
- search `words inside text`

```sql
SELECT * FROM posts
WHERE MATCH(content) AGAINST('database indexing');
```

- this query will return posts that mention `database` or `indexing`
- then, sort by relevance

[![Screenshot-2025-06-30-at-01-22-20.png](https://i.postimg.cc/CxGpVDBF/Screenshot-2025-06-30-at-01-22-20.png)](https://postimg.cc/183jG8rT)

## ✅ Can you explain different types of index scans in a database?

- Index scan: retrieving data using index, instead of scanning the entire table

- ✔️ **Index Full Scan**: scan all entries in index
- query access all rows in index
- can be faster than `table full scan` if index has fewer columns

```sql
SELECT name FROM users;
```

- ✔️ **Index Range Scan**: scan specific range based on conditions
- `BETWEEN`, `<`, `>`, `LIKE 'A%`

```sql
SELECT * FROM employees WHERE age BETWEEN 30 AND 40;
```

- ✔️ **Index Unique Scan**: retrieve single row with unique index

```sql
SELECT * FROM users WHERE id = 123;
```

- ✔️ **Index Skip Scan**: when you are using composite index(multi-column index) but your query skips the first column

```sql
-- have composite index on department, job_title
CREATE INDEX idx_dept_job ON employees(department, job_title);

-- however, run query on job_title
-- the query DOES NOT filter the first column
SELECT * FROM employees WHERE job_title = 'Manager';

-- in composite index, need to use first or both index in query
-- thus, normally, index will not be used
-- 🟢 with index skip scan, DB will use index smartly
```

- DB will check `department` per `job_title`
- smth like `Teacher + Manager`, `Developer + Manager`...
- DB will do a **subtree scan** within the index

- better query
- use both index columns, no skipping is needed

```sql
SELECT * FROM employees
WHERE department = 'Sales' AND job_title = 'Manager';
```

## ✅ Have you ever checked a query execution plan? Can you explain what it is and how you analyze it?

- checked a query execution plan using `EXPLAIN` in MySQL
- query execution plan: strategy chosen by DB optimizer to execute SQL query

- no index
  [![Screenshot-2025-06-30-at-00-46-36.png](https://i.postimg.cc/9QnFryXy/Screenshot-2025-06-30-at-00-46-36.png)](https://postimg.cc/fVYhPt9b)

- use index
  [![Screenshot-2025-06-30-at-00-52-17.png](https://i.postimg.cc/zvcPnDy2/Screenshot-2025-06-30-at-00-52-17.png)](https://postimg.cc/Mf1DwSb1)

- `type`: join type or scan method, important for performance
  - `ALL`: full table scan
  - `index`: full index scan
  - `range`, `ref`, `eq-ref`: efficient indexed access
- `key`: which index is used
- `rows`: number of rows DB expects to scan
- `filtered`: percentage of rows expected to pass the filtering condition

- also used `show profile CPU` to check CPU usage

[![Screenshot-2025-06-30-at-00-47-01.png](https://i.postimg.cc/9M3mBV7M/Screenshot-2025-06-30-at-00-47-01.png)](https://postimg.cc/qtLHkPQV)

## ✅ What is a hint in SQL, and when would you use it?

- hint: directive you include in SQL query to influence the behavior of the query optimizer
- override default optimization, enforce your strategy

- tell optimizer to use `idx_department` index explicitly

```sql
SELECT /*+ INDEX(employees idx_department) */ *
FROM employees
WHERE department = 'Engineering';
```

- ⚠️ overusing hints can reduce maintainability

## ✅ How do you check if an index is being used by a query?

- check by examining `query execution plan`
- use `EXPLAIN` in MySQL

- look for `key` column in the `EXPLAIN` output
- if `key` shows index, that index is being used
- if `key` is null, query is not using index

- can also run `SHOW INDEX;`

```sql
SHOW INDEX FROM user;
```

[![Screenshot-2025-06-30-at-00-58-37.png](https://i.postimg.cc/RZz2GFP2/Screenshot-2025-06-30-at-00-58-37.png)](https://postimg.cc/ppq0L2MB)

## ✅ What should you be careful about when using indexes?

- ⚠️ overuse of index slow down write operations
- ⚠️ index maintenance overhead: changing indexed columns often lead to constant re-balancing of index structure
- ⚠️ using index in low cardinality columns: if use index in `gender` column with only a few distinct values, index will not be effective!
- ⚠️ correct order in `composite(multi-level) index`: `composite index` query should start with first column. Put high-cardinality columns first

## ✅ How does GROUP BY affect index usage in queries?

- index can be used in `GROUP BY` queries **only when the grouping column match the index structure**

- 1. **leading column** of index must appear in `GROUP BY`
- 2. column order in `GROUP BY` must match **index order**
- 3. extra columns in `GROUP BY` that are **NOT** part of index can prevent index use

```sql
-- Index: (country, gender, name)

-- ⭕️ index is used
SELECT country, COUNT(*)
FROM users
GROUP BY country;

SELECT country, gender, COUNT(*)
FROM users
GROUP BY country, gender;

-- ❌ index is NOT used
-- order is wrong
SELECT gender, country
FROM users
GROUP BY gender, country;
```

## ✅ How would you create an index on a table with name, country, and gender?

- 1. Analyze cardinality: how unique is this column?
- `name` would have higher `cardinality`
- `country` or `gender` has low cardinality

- 2. Create composite(multi-column) index

```sql
CREATE INDEX idx_name_country_gender ON users(name, country, gender);
```

- 3. ⚠️ Be careful, in `composite index` including leading column is important!
- always include leading column

```sql
-- ⭕️ use index
SELECT * FROM users WHERE name = 'John';
SELECT * FROM users WHERE name = 'John' AND country = 'Korea';

-- ❌ index will not be used
-- unless Index Skip Scan is enabled
SELECT * FROM users WHERE country = 'Korea';

```

- 4.  ⚠️ In `GROUP-BY`, leading column and order is very important

```sql
-- ⭕️ use index
SELECT name, COUNT(*) FROM users
GROUP BY name;

SELECT name, country, COUNT(*) FROM users
GROUP BY name, country;

SELECT name, country, gender, COUNT(*) FROM users
GROUP BY name, country, gender;

-- ❌ index will not be used
-- leading column is not included
SELECT country, COUNT(*) FROM users
GROUP BY country;

-- ❌ index will not be used
-- order is wrong
SELECT country, name FROM users
GROUP BY country, name;
```
