---
title: Cache Memory, Web Caache
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ Cache Memory

> memory to decrease loading time <br>
> serve as a buffer between the main memory (RAM) and the central processing unit (CPU) <br> <br>

- when CPU reads from RAM, saves frequently used data on cache memory
- next time, bring the data from cache ➡️ save time

### ✔️ Different levels of cache

- L1: CPU will start looking for data in L1 <br>
- L2: if not in L1, look for data in L2 <br>
- L3 <br>

## ☑️ Operation of cache

1. when CPU needs to read or write a location in the main memory, check cache
2. find the memory location in cache: **cache hit**
3. does not find: **cache miss**
   - cold miss: location was called for the first time
   - conflict miss: when trying to save multiple lines in the same cache, might have to evict some of them to make room for new data
   - capacity miss: cache is too small to save data
4. performance of cache memory is measured in **hit ratio**

## ☑️ Cache mapping

1️⃣ **Direct Mapping**

> map each memory block to one possible cache line <br>
> if new block is needed, the old block is trashed <br>

- address space = index field ➕ tag field(cache)
- DRAM의 여러 주소가 캐시 메모리의 한 주소에 대응되는 다대일 방식

2️⃣ **Associative Mapping**

> any block can go into any line of cache <br>

- flexible, fastest
- 비어있는 캐시 메모리 아무대나 저장
- 저장은 간단하지만 찾는게 문제

3️⃣ **Set-Associative Mapping**

> enhanced form of direct mapping ➕ Associative Mapping <br>
> group a few lines together to create set<br>
> block in memory can map to any line of a specific set<br>

- 특정 행을 지정하고 그 행 안의 비어있는 열에 저장

## cache 🆚 cookie

- cache: decrease loading time <br>
- cookie: trace user preferences<br>
  <https://www.geeksforgeeks.org/difference-between-cache-and-cookies/?ref=header_search>

## ✅ Web Cache

> save copy of frequently used resource

- if a request requires resource in cache,
- the resource will not be provided by original server ❌ but by cache ⭕️

### 👍🏻 Benefits of cache

- reduce unnecessary data transmission
- burden of original server ⬇️
- network bottleneck ⬇️
- bandwidth ⬆️
- can react to sudden high traffic
- reduce latency due to distance ⬇️ (get resource from close cache server)

## ☑️ Cache hit, cache miss, revalidation

<img width="327" alt="Screenshot 2024-08-27 at 08 57 48" src="https://github.com/user-attachments/assets/7ad7701f-40b2-4f20-b2b5-b924b273613b">

✔️ **cache hit**

- requested data **is found** in the cache
- fast data retrieval

✔️ **cache miss**

- data **not** in cache at time of request
- slower retrival from meain memory, origin server

## ☑️ cache revalidation

- data in origin server can change
- so cache has to **check** if the data copy it has is valid(if the copy is same w origin server)

- add to HTTP GET request `If-Modified-Since` header
- means _get me copy **only if** the origin data was altered_
  - if origin data not changed:
  - HTTP response `HTTP 304 Not Modified`
  - if origin data is different from copy that cache has:
  - HTTP response `HTTP 200 OK`

> **When to check cache validation?**
>
> > - HTTP lets origin server to add **expirary limit** to resources
> > - use header such as `cache-control`, `expires`
> > - after this expirary limit, cache has to validate itself
> > - and if not valid, get the new altered resource with new expirary limit

- `cache-control`: max age

  - max age a resource can have
  - recorded in `seconds`
  - example: `cache-control`: max-age: 484200

- `expires`: data
  -expirary date
  - `expires`: Fri, 05 Jul 2025, 05:00:00 GMT

## ☑️ Types of Web Cache

✔️ **Private cache**

- 개인 전용 캐시
- cache allocated to private user
- most web browsers have `Private cache`
- save frequently used resources in cache in computer disk, memory

✔️ **Public proxy cache**

- 공용 프락시 캐시
- proxy cache provide resources in local cache
- can access server as user
- **several users** can access public cache, reducing unnecessary traffic ⬇️

## ✅ Spring cache

<https://soheeparklee.github.io/posts/Spring_cache/>
