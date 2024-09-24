---
title: Table Full Scan/ Index Range Scan/ Index Full Scan
categories: [Database, DB]
tags: [] # TAG names should always be lowercase
---

## ✅ Table Full Scan

- read all blocks in table to find data
- used for database optimization, optimizing query
- 👎🏻 can affect database performance if the table is big, query is complex

## ✅ Index Range Scan

- use index to read certain data
- use ROWID to find table record
- **ROWID**: point to where table record is saved on disk

## ✅ Index Full Scan

- not read all table, but read all index
- index is much smaller than table
