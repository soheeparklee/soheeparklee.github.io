---
title: Partitioning, Sharding
categories: [Database, DB]
tags: [] # TAG names should always be lowercase
---

## ✅ Partitioning

> divide big table into small several tables <br>

- 👍🏻 improve query performace
- data is physically divided into seperate tables
- but user can access the data as if it is on the same table

- 🆚 save all data on one computer

## ✅ Sharding

> save divided data in small unit <br>
> on several DB server with same schema <br>

- **shard**: small unit to divide data into
- one of parallel partitioning

- 👍🏻 query performace
- 👍🏻 balance overhead
- 👍🏻 parallel scale-out of DB

- 🆚 save data on several computers
