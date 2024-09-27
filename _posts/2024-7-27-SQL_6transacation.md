---
title: Transaction/ Transaction Isolation Level
categories: [Database, DB]
tags: [] # TAG names should always be lowercase
---

## ✅ Transaction

> work **unit** for updating database

- **atomacity**: 반영되거나, 반영되지 않거나
- **consistency**
- **isolation**: when one transaction is working, another transaction cannot interfere
- **durability**: transaction result must be forever applied

- commit: when one transaction is completed successfully and DB is consistent
- rollback: if atomacity of transaction breaks, go back to state before

## ✅ DBMS strategy for Transaction

➕ DBMS structure

- Query Porcessor
- Storage System
- input unit: fixed size page, write or read on disk
- memory: involatile disk, partly saved on main memory

➕ Page Buffer Manager or Buffer Manager

- module in `Storage System`
- manage page in main memory

**1. UNDO**

- when pages are updated
- output on disk by buffer algorithm
- if transaction is not closed properly,
- all the pages that were updated by this transaction should be undo

**2. REDO**

- when transaction is complete,
- decide to write on disk the pages that the transaction updated

## ✅ Transaction Isolation Level

> define the degree <br>
> to which a transaction must be **isolated** from the data modifications <br>
> made by any other transaction in the database system <br>

#### ✔️ Read Uncomitted

- lowest isolation level
- another transaction may read uncommited changes made by other transactions
- transactions are not isolated

- 😬 dirty read
- 😬 non-repeatable read
- 😬 phantom read

#### ✔️ Read Committed

- data that can be read is committed data

- 😬 non-repeatable read
- 😬 phantom read

#### ✔️ Repeatable Read

- read lock on all rows it references
- and writes locks on referenced rows for update and delete

- 😬 phantom read

#### ✔️ Serializable

- highest isolation level
- operations will be done in a serial execution

## ☑️ What happens without isolation

#### ✔️ Dirty Read

- transaction reads data that has been changed, but not yet been committed
- transaction can read value that has been rolled back ➡️ read unvalid data

#### ✔️ Non-repeatable Read

- transaction reads the same row twice and gets a different value each time
- read before transaction, and read after the data is updated
- the retrieval will be different

#### ✔️ Phantom Read

- type of non-repeatable read
- two same queries retirve different rows
- row that has been newly created, or has been deleted
