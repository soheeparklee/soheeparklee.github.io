---
title: Interview_Anomaly, Functional Dependency, Normalization
categories: [Database, DB]
tags: [] # TAG names should always be lowercase
---

## ✅ What is an Anomaly in a database?

- ✔️ **Anomaly**: unexpected problems that happen when `inserting`, `updating`, `deleting` data in DB

- ❓ **When does it happen?**
- when table is not properly structured
- contains redundant, repetitive data

## ✅ What are the types of anomalies?

- Insertion Anomaly
- Update Anomaly
- Deletion Anomaly

## ✅ What is an insertion anomaly? Can you explain each with an example?

- ✔️ **Insertion Anomaly**: when we cannot add data to a table without adding **unrelated, empty data**

```
There is a student table with student score. If a student did not take any exams yet, how do we store data? This is insertion anomaly.

|  StudentID | StudentName | TestScore |
|------------|-------------|-----------|
|   1001     |     Alice   |    NULL   |

```

- we are forced to enter `NULL` into `TestScore`

## ✅ What is an update anomaly? Can you explain each with an example?

- ✔️ **Update Anomaly**: when duplicate data is stored in **multiple rows**, and **only some** get updated
- result in inconsistend information

```
If one teacher teaches more than one subject

| Course | Instructor | Phone       |
|--------|------------|-------------|
| Math   | John Smith | 123-4567    |
| Physics| John Smith | 987-6543 ❌ |
```

## ✅ What is a deletion anomaly? Can you explain each with an example?

- ✔️ **Deletion Anomaly**: deleting a piece of data also **deletes important information** unintentionally

```
If a student drops out of a course and we delete that row
and end up losing all student info

| StudentID | StudentName | Course  |
|-----------|-------------|---------|
| 1001      |    Alice    |  Math   | ← Deleting this removes student 1001 entirely
```

## ✅ To eliminate anomalies, how far should normalization go?

- normalization should be performed up to the **3rd Normal Form**

- ✔️ **1NF:** remove repeating groups
- ✔️ **2NF:** remove partial dependencies
- ✔️ **3NF:** remove transitive dependencies

## ✅ What is Functional Dependency?

> If we know X, then we know Y

- if you know one piece of data, you know another piece

```
| StudentID | StudentName | Course  |
|-----------|-------------|---------|
| 1001      |    Alice    |  Math   |
```

- `studentID` and `studentName` has functional dependency

## ✅ What is a Full (Complete) Functional Dependency?

> attribute depends on the entire primary key <br>
> happens when primary key is made up of **two or more columns** <br>

```
| StudentID |  courseID   | Grade   |
|-----------|-------------|---------|
| 1001      |    ab123    |  A+     |
| 1001      |    cd345    |  B-     |
```

- `grade` depends on both `studentID` and `courseID`

## ✅ What is a Partial Functional Dependency?

> attirbute depends on only part of a composite key <br>
> 🔴 problem, creates repetition and data redundancy

```
| StudentID |  courseID   | StudentName   | courseName  |
|-----------|-------------|---------------|-------------|
| 1001      |    ab123    |     Alice     |    math     |
| 1001      |    cd345    |     Alice     |   science   |
```

- primary key: `StudentID`, `courseID`
- `studentName` depends only on `StudentID`

- 💊 decompose into two tables
- exmaple of `Second Normal Form(2NF)`(remove partial dependency)

```
✔️ student table
| StudentID | StudentName |
|-----------|-------------|
| 1001      |    Alice    |

✔️  course table
| courseID  |  courseName |
|-----------|-------------|
| ab123     |    math     |
| cd345     |    science  |

✔️  enrollment table
| StudentID |  courseID   |
|-----------|-------------|
| 1001      |    ab123    |
| 1001      |    cd345    |
```

## ✅ What is a Transitive Dependency?

> A determine B, B determine C <br>
> thus, A also determines C **indirectly** <br>

- 🔴 problem, update anoamilies
- data inconsistency problem
- redundancy

```
| StudentID | AdvisorID | AdvisorName |
| --------- | --------- | ----------- |
| 1001      | A1        | Prof. Kim   |
| 1002      | A2        | Prof. Lee   |
| 1003      | A1        | Prof. Kim   |

```

- `StudentID` ➡️ `AdvisorID`
- `AdvisorID` ➡️ `AdvisorName`
- thus, `StudentID` ➡️ `AdvisorName`

- 💊 decompose into two tables
- exmaple of `Third Normal Form(3NF)`(remove transitive dependency)

```
- student table
| StudentID | AdvisorID |
| --------- | --------- |
| 1001      | A1        |
| 1002      | A2        |
| 1003      | A1        |


- advisor table
| AdvisorID | AdvisorName |
| --------- | ----------- |
| A1        | Prof. Kim   |
| A2        | Prof. Lee   |
```

## ✅ What is normalization in databases?

- **normalization**: organizing DB
- reduce duplication
- remove anomalies
- ensure data integrity

- break down large table ➡️ smaller, connected tables

- 👎🏻 one big table of users, ordres, products
- 💊 normalization: split into three small tables
  - user table, order table, product table
  - linked with `keys`(`OrderID`, `UserId`, `ProductId`)

## ✅ What is the First Normal Form (1NF)?

- ✔️ **First Normal Form**: get rid of duplicates
- each column has **atomic(indivisible, 나눌 수 없는)** values

- 👎🏻 before, bad DB

```
| StudentID | StudentName |        Hobbies    |
|-----------|-------------|-------------------|
| 1001      |    Alice    | reading, swimming |
```

- 💊 after 1NF
- each hobby is stored in separate row or separate table

```
| StudentID | StudentName |  Hobby   |
|-----------|-------------|----------|
| 1001      |    Alice    | reading  |
| 1001      |    Alice    | swimming |
```

- 👎🏻 however, partial dependency issue persists
- if we consider `StudentID` and `Hobby` to be primary keys,
- column `Name` depends only on `StudentID`, not on `Hobby`

- 💊 after 2NF
- solved partial dependency issue

```
- student table
| StudentID | Name |
| --------- | ---- |
| 1         | John |

- hobby table
| StudentID | Hobby    |
| --------- | -------- |
| 1         | Reading  |
| 1         | Swimming |


```

## ✅ What is the Second Normal Form (2NF)?

- ✔️ **Second Normal Form**: get rid of partial dependency
- table is in 1NF
- and **all non-key columns** **fully depend on entire primary key**, not partially

- 👎🏻 before, bad DB
- `studentName` only depends on `StudentID`

```
| StudentID |  courseID   | StudentName   | courseName  |
|-----------|-------------|---------------|-------------|
| 1001      |    ab123    |     Alice     |    math     |
| 1001      |    cd345    |     Alice     |   science   |
```

- 👍🏻 after 2NF

```
✔️ student table
| StudentID | StudentName |
|-----------|-------------|
| 1001      |    Alice    |

✔️  course table
| courseID  |  courseName |
|-----------|-------------|
| ab123     |    math     |
| cd345     |    science  |

✔️  enrollment table
| StudentID |  courseID   |
|-----------|-------------|
| 1001      |    ab123    |
| 1001      |    cd345    |
```

## ✅ What is the Third Normal Form (3NF)?

- ✔️ **Third Normal Form**: get rid of transitive dependency
- table is in 2NF
- non-key columns **should not** depend on other non-key columns

- 👎🏻 before, bad DB

```
| StudentID |  courseID   |  courseName  |
|-----------|-------------|--------------|
| 1001      |    ab123    |     math     |
| 1001      |    cd345    |    science   |
```

- 👍🏻 after 3NF

```
- enrollment table
| StudentID | CourseID |
| --------- | -------- |
| 1001      | ab123    |
| 1001      | cd345    |


- course table
| CourseID | CourseName |
| -------- | ---------- |
| ab123    | math       |
| cd345    | science    |

```

## ✅ What is Boyce-Codd Normal Form (BCNF)?

- ✔️ **Boyce-Codd Normal Form**: every determinant(a column that determines another) must be a candidate key
- every functional dependency, `X ➡️ Y`, `X` **must be** a candiate key
- violated when a non-candidate key determines another column

- 👍🏻 example of abiding BCNF

```
| StudentID | StudentName | RoomNumber |
|-----------|-------------|------------|
| 1001      |    Alice    |    101     |
| 1002      |    Danny    |    102     |
| 1003      |    Smith    |    203     |
| 1004      |    Lilly    |    203     |
```

- 👎🏻 example of violating BCNF
- also violates 2NF

```
| StudentID | Course | Instructor |
| --------- | ------ | ---------- |
| 1001      | Math   | Prof. Kim  |
| 1002      | Math   | Prof. Kim  |
| 1003      | CS     | Prof. Lee  |
```

- primary key: `StudentID`, `Course`
- however, `Instructor` relys only on `Course` ➡️ 💥 violate 2NF
- `Course ➡️ Instructor`, however `Course` is not a candidate key ➡️ 💥 violate BCNF

## ✅ 4th Normal Form (4NF)

- ✔️ **4th Normal Form**: has no multivalued dependencies
- no attribute determines multiple independent values

- multivalued dependency: when one column determines multiple values
- but those columns do not depend on each other
- `Language` and `Hobby` do not depend on each other

```
| Student | Language | Hobby  |
| ------- | -------- | ------ |
| John    | English  | Guitar |
| John    | English  | Soccer |
| John    | Spanish  | Guitar |
| John    | Spanish  | Soccer |


- fix after 4NF
- Language table
| Student | Language |
| ------- | -------- |
| John    | English  |
| John    | Spanish  |


- Hobby table
| Student | Hobby  |
| ------- | ------ |
| John    | Guitar |
| John    | Soccer |

```

## ✅ 5th Normal Form (5NF)

- ✔️ **5th Normal Form**: has no join dependency
- table can be split into smaller tables and re-joined without having redundancy problems

```
| Employee | Skill  | Trainer |
| -------- | ------ | ------- |
| Alice    | Java   | Bob     |
| Alice    | Python | Bob     |
| Alice    | Java   | Carol   |
| Alice    | Python | Carol   |

- can be split into
- Employee-Skill
- Skill-Trainer
- Employee-Trainer
```

## ✅ What is denormalization?

- ✔️ **denormalization**: intentionally add redundancy by combining tables
- 👍🏻 to improve read performace
- 👎🏻 increase storage
- 👎🏻 increase update anomality

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅
