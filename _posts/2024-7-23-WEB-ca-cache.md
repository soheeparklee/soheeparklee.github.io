---
title: Cache Memory
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ Cache

> memory to decrease loading time <br>
> serve as a buffer between the main memory (RAM) and the central processing unit (CPU) <br> <br>

- when CPU reads from RAM, saves frequently used data on cache memory
- next time, bring the data from cache ➡️ save time

### ✔️ Different levels of cache

L1: CPU will start looking for data in L1 <br>
L2: if not in L1, look for data in L2 <br>
L3 <br>

### ✔️ Operation of cache

1. when CPU needs to read or write a location in the main memory, check cache
2. find the memory location in cache: **cache hit**
3. does not find: **cache miss**
   - cold miss: location was called for the first time
   - conflict miss: when trying to save multiple lines in the same cache, might have to evict some of them to make room for new data
   - capacity miss: cache is too small to save data
4. performance of cache memory is measured in **hit ratio**

### ✔️ Cache mapping

1️⃣ Direct Mapping

> map each memory block to one possible cache line <br>
> if new block is needed, the old block is trashed <br>

- address space = index field ➕ tag field(cache)
- DRAM의 여러 주소가 캐시 메모리의 한 주소에 대응되는 다대일 방식

2️⃣ Associative Mapping

> any block can go into any line of cache <br>

- flexible, fastest
- 비어있는 캐시 메모리 아무대나 저장
- 저장은 간단하지만 찾는게 문제

3️⃣ Set-Associative Mapping

> enhanced form of direct mapping ➕ Associative Mapping <br>
> group a few lines together to create set<br>
> block in memory can map to any line of a specific set<br>

- 특정 행을 지정하고 그 행 안의 비어있는 열에 저장

## cache 🆚 cookie

cache: decrease loading time <br>
cookie: trace user preferences<br>
<https://www.geeksforgeeks.org/difference-between-cache-and-cookies/?ref=header_search>
