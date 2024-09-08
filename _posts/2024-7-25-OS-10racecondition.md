---
title: Race Condition
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ Race Condition

> when several processes need shared resource at the same time, can affect the result value <br>
> when accessed at **concurrent** time, **data integrity** ⬇️ <br>

- several process attempt shared resource
- timing, order can affect result

## ✅ When Race Condition occurs

**1. Interrupt while kernel** <br>

- using data in kernel mode
- interrupt
- alter data
- global variable in kernel is shared resource
- prone to race condition
  <br>

- 💊 while working in kernel mode, **disable interrupt**
- interrupt cannot take CPU control

**2. System call** <br>

- process makes system call
- enter kernel mode
- context switching occurs
  <br>

- Process 1 in kernel mode, modifying data
- CPU timeout
- CPU control goes over to Process 2
  <br>

- 💊 If process is working in kernel mode, even if timeout, CPU control should not go over to next process

**3. Multi Process environment, while accessing shared memory kernel data** <br>

- In multi processing environment
- two CPUs enter kernel for shared data, alter data
  <br>

- 💊 lock data when shared data is accessed
