---
title: Transaction Isolation Level
categories: [Database, Database]
tags: [] # TAG names should always be lowercase
---

## ✅ Transaction Isolation Level

> define the degree to which a transaction must be isolated from the data modifications made by any other transaction in the database system

### ✔️ Read Uncomitted

- lowest isolation level
- another transaction may read uncommited changes made by other transactions
- transactions are not isolated

### ✔️ Read Committed

- can data that can be read is committed data

### ✔️ Repeatable Read

- most restrictive
- read lock on all rows it references and writes locks on referenced rows for update and delete

### ✔️ Serializable

- highest isolation level
- operations will be done in a serial execution

## ☑️ What happens without isolation

### ✔️ Dirty Read

- transaction reads data that has not yet been committed

### ✔️ Non-repeatable Read

- transaction reads the same row twice and gets a different value each time
- read before transaction, and read after the data is updated
- the retrieval will be different

### ✔️ Phantom Read

- two same queries retirve different rows

## 💡 Reference

<https://www.geeksforgeeks.org/transaction-isolation-levels-dbms/>
