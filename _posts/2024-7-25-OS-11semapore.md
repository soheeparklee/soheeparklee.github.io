---
title: Semaphore, Mutex
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

> kernel resources that provide synchronization services <br>

## ✅ Semaphore

> limit access to shared resource in multi programming <br>
> singnaling mechanism: thread can be signaled by another thread <br>
> Wait(P), Signal(V) <br>
> machine independent <br>

### ⭐️ Critical Section

> program code to access shared data <br>

- if one process is running in `Critical Section`, other processes cannot access
- However, multiple threads can access the `Critical Section` at the same time

## ✅ Mutex

> Mutual Exclusion <br>
> thread execution time to be independent <br> > **lock, unlock** <br>

- kind of binary semaphore

### ⭐️ Lock, unlock

lock: authorized to go into Critical Section <br>
unlock: annouce this process is done with Critical Section <br>

### Mutex Algorithm

- Dekker algorithm
- Peterson algorithm
- Backery algorithm

💡 <https://www.geeksforgeeks.org/mutex-vs-semaphore/> <br>
