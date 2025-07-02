---
title: Interview_
categories: [Database, DB]
tags: [] # TAG names should always be lowercase
---

## ✅ What is a DB session?

- ✔️ **DB session**: **logical connection** between user(application) and DB
- DB session starts when user makes the connection
- and ends when user disconnects

- allow DB to track user activity like `queries`

## ✅ What is a connection in the context of databases?

- ✔️ **connection**: acutal network link between user and DB
- enable data exchange

## ✅ What is a transaction in databases?

- ✔️ **Transaction**: group of one or more operations that need to be **executed together** as a **single unit of work**

- all operations must succeed(`commit`) or fail(`rollback`)
- 👍🏻 transactions help keep your data consistent

## ✅ What is a commit in a database?

- ✔️ **Commit**: permanently save changes made in a transaction
- transaction success

## ✅ What is a rollback in a database?

- ✔️ **Rollback**: undo all changes made by current transaction
- restore DB to its previous state
- transaction fail

## ✅ What is Auto Commit in a database?

- ✔️ **Auto Commit**: `Auto Commit` automatically commits each SQL after execution
- in `MySQL`, `Auto Commit` is ON by default
- if you turn it off, you have to save manually yourself

## ✅ Why would you set Auto Commit to false?

- 👍🏻 if you want to group multiple operations into a single transaction
- 👍🏻 reduce unnecessary commits, and improve performance

- instead of saving after each line, save after writing whole paragraph

## ✅ How do developers handle manual commit when Auto Commit is off?

- Manually call `COMMIT` after finishing operation
- use `SpringBoot` annotation such as `@Transactional`

## ✅ What are ACID properties of transactions?

- ✔️ **Atomicity**: transaction should occur in one single work unit, all or nothing
- ✔️ **Consistency**: Even if money moved from A to B, sum should be the same.
- ✔️ **Isolation**: Transaction must not interfere with each other
- ✔️ **Durability**: Once commited, data should remain even if DB fails

## ✅ What is transaction isolation level?

- ✔️ **Transaction Isolation Level**: how transactions interact with each other
- low isolation level: better performance, less safe
- (ex) read uncommited

- high isolation level: more safe, lower performance.
- (ex) serializable

## ✅ What are the problems that can occur due to low isolation levels?

- 💥 **Dirty Read**: read data that has been changed, but not commited
- if data is rolled back, you have read wrong data

- 💥 **Non-repeatable Read**: same query returns different result
- another transaction changes the data

- 💥 **Phantom Read**: new rows appear between reads
- after `INSERT`, `SELECT` would return new results

## ✅ What are the common isolation levels?

- 1️⃣ **READ UNCOMMITED**: read data before commit, if roll-back, you get dirty read

- 2️⃣ **READ COMMITED**: only read commited data

- 3️⃣ **REPEATABLE READ**: same query, same result

- 4️⃣ **SERIALIZABLE**: full isolation, `one-at-a-time`

```
Isolation Strength →
READ UNCOMMITTED < READ COMMITTED < REPEATABLE READ < SERIALIZABLE
          ↑                ↑               ↑                ↑
    High performance   Balanced     Better safety     Best consistency

```

## ✅ What is the default isolation level of major RDBMSs?

- MySQL: REPEATABLE READ
- PostgreSQL: READ COMMITED
- Oracle: READ COMMITED

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅
