---
title: Semaphore, Mutex
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ Semaphore

> limit access to shared resource in multi programming

### ⭐️ Critical Section

> program code to access shared data

- if one process is running in `Critical Section`, other processes cannot access

## ✅ Mutex

> Mutual Exclusion
> thread execution time to be independent
> lock, unlock

### ⭐️ Lock, unlock

lock: authorized to go into Critical Section
unlock: annouce this process is done with Critical Section

### Mutex Algorithm

- Dekker algorithm
- Peterson algorithm
- Backery algorithm
