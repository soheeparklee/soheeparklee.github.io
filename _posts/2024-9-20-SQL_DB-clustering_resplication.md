---
title: DB Clustering/ Replication/ Mirroring
categories: [Database, DB]
tags: [] # TAG names should always be lowercase
---

- ⭐️ common ground: methods for enhancing DB **availability, reliability**

## ✅ DB Clustering

> distributed database system across parallel nodes <br>
> by **grouping** interconnected servers to **work as a single system** <br>

- if one DB has a problem, another DB can continue the work

- 👍🏻 availability ⬆️
- 👍🏻 load balancing ⬆️
- 👍🏻 allow data duplication, data recovery, fault tolerance
- 👍🏻 scalability
- 👎🏻 synchronization among replicated data
- 👎🏻 communication among node complicated

## ✅ DB Replication

> horizontal model <br>
> copy several database <br>
> multiple copies of data across different devices, systems <br>
> several server can access <br>

- 👍🏻 synchronization among replicated data easy
- 👍🏻 data remains up to date
- 👍🏻 data availability, distribution, disaster recovery
- 👎🏻 need to replicate data, more resource use

- snapshot
- transactional replication
- merge replication

#### ✔️ Master-slave replication

- replicate data to `slave DB` from `master DB`
- `master DB`: read & write
- `slave DB`: read only

## ✅ DB Mirroring

> create exact copy of data from one device to another in real-time <br>

- replicated data 🟰 synchrnoized with origin data

- 👍🏻 redundancy
- 👍🏻 recovery
- 👍🏻 availability ⬆️
