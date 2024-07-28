---
title: Transaction
categories: [Database, DB]
tags: [] # TAG names should always be lowercase
---

## ✅ Transaction

> work unit for updating database

- atomacity: 반영되거나, 반영되지 않거나
- consistency
- isolation
- durability: transaction result must be forever applied

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

1. UNDO

- when pages are updated
- output on disk by buffer algorithm
- if transaction is not closed properly,
- all the pages that were updated by this transaction should be undo

2. REDO

- when transaction is complete,
- decide to write on disk the pages that the transaction updated
