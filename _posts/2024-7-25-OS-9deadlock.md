---
title: Deadlock
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ Deadlock

> when more than two processes/threads cannot be run bc there is no resource
> wait infinite for resource
> occurs when several processes/threads need to work with limited resource

![Screenshot 2024-07-25 at 13 15 42](https://github.com/user-attachments/assets/94f5d409-9415-4636-9f87-6853792aab4a)

situation: process 1 and 2 both need resource 1 and 2
t1: process 1 gets resource 1 and process 2 gets resource 2
t2: process 1 waits for resource 2 and process 2 waits for resource 1

## ✅ Conditions for Deadlock

- mutual exclusion
- hold and wait
- no preemption
- circular wait
