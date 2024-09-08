---
title: Deadlock
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ Deadlock

> requirement for system resource order is mixed up <br>

- when more than two processes/threads cannot be run bc there is no resource <br>
- wait infinite for resource <br>
- occurs when several processes/threads need to work with limited resource <br>
- 둘 이상의 프로세스가
- 서로가 점유한 자원을 서로 기다림
- 무한 대기에 빠진다.

![Screenshot 2024-07-25 at 13 15 42](https://github.com/user-attachments/assets/94f5d409-9415-4636-9f87-6853792aab4a)

situation: process 1 and 2 both need resource 1 and 2 <br>
t1: process 1 gets resource 1 and process 2 gets resource 2 <br>
t2: process 1 waits for resource 2 and process 2 waits for resource 1 <br>

## ✅ Conditions for Deadlock

✔️ **mutual exclusion**

- only one process can use resource at a time
- if other process wants to use the resource, has to wait

✔️ **hold and wait**

- there should be a process with minimum one resource,
- waiting for resource to be allocated, that is already posessed by another process

✔️ **no preemption**

- Cannot take resource from another process forcefully

✔️ **circular wait**

- Resource wait in circular way

## ✅ Solution for Deadlock

1. **Prevention** <br>

- prevent `mutual exclusion`
- prevent `hold and wait`
- prevent `no preemption`
- prevent `circular wait`

2. **Avoidance** <br>

- only allow resource with deadlock vulnerability in `safe state`
- do not allow `unsafe allocation`(situation with deadlock possibility)

- `Safe state`: safe sequence(order for allocating resource without deadlock)

  - every process can end

- `Unsafe state`: situation with deadlock possibility

  - 💊 은행원 알고리즘
  - 💊 자원 할당 알고리즘

- In order for avoidance, following conditions should be met
- fixed number of process
- fixed number of type, number of process
- knowledge of process maximum required resource
- process should return resource after use

3. **Detection**, **Recovery** <br>

- detect deadlock
- 👎🏻 need to continuously check, overhead
  <br>

- recovery
- A. 사용자 처리
- user forcefully stops one process
- B. 시스템 처리
- stops process
- stops all process in deadlock
- stops process on by one until deadlock is solved
- take resource from process, and allocate to other processes until deadlock is solved
