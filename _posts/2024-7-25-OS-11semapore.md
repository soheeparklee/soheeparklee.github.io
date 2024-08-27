---
title: Semaphore/ Mutex/ Spinlock
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

> kernel resources that provide **synchronization** services <br>
> synchronization services to prevent multi threads to access shared resrouce at the same time <br>
> limit access to shared resource in multi programming <br>

## ⭐️ Critical Section

> program code to access shared data <br>

- if one process is running in `Critical Section`, other processes cannot access
- However, multiple threads can access the `Critical Section` at the same time
- thus, need technique such as semaphore, mutex, spinlock

## ✅ Semaphore

> singnaling mechanism: thread can be **signaled** by another thread <br>

- **signaling mechanism**
- Wait(P), Signal(V) <br>
- machine independent <br>
- `해도 돼`, `기다려!` 시그널을 준다.
- 👍🏻 can be used for mutual exclusion, or counting semaphore
- 👎🏻 resource might be blocked for a long time

- **Binary semaphore**: 0, 1
  - like mutex
- **Counting semaphore**: count number of available resource

## ✅ Mutex

> Mutual Exclusion <br>
> thread execution time to be independent <br>
> use **lock**

- **lock, unlock** <br>
- kind of _binary semaphore_
- shared resource 잠궈버리기, 뮤텍스 잠겨 있으면 현재 스레드는 다른 작업 하다가 뮤텍스 해제되면 접근 가능
- only mutual exclusion possible

### ⭐️ Lock, unlock

lock: authorized to go into Critical Section <br>
unlock: annouce this process is done with Critical Section <br>

### Mutex Algorithm

- Dekker algorithm
- Peterson algorithm
- Backery algorithm

## ✅ Spinlock

- locking system mechanism
- simply wait in loop until the lock is available
- thread waits in a loop or spin until the lock is available
- 👍🏻 only mutual exclusion possible
- 👍🏻 blocked only for a short period of time

💡 <https://www.geeksforgeeks.org/mutex-vs-semaphore/> <br>
