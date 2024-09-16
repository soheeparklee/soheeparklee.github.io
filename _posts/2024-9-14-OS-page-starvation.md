---
title: Starvation/ Aging
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ Starvation

> resource management problem <br>

- process priority is low
- process is never allocated resource

- priority is low: came late, takes long time...
  💡 How to prioritize process <https://soheeparklee.github.io/posts/OS-8CPUscheduling/>

- 프로세스가 원하는 자원을 계속 할당받지 못하는 상태
- several process compete for one resource, never gets it
- always lose in competition

## 🆚 Deadlock

> process cannot get next resource, wait

- 프로세스가 자원을 얻지 못해 다음 처리를 못하는
- several process want one resource
- cannot go onto next step, locked

## 💊 Aging

> to prevent starvation

- If certain process waits for a long time bc has low priority
- let it go first
- or take waiting time into account, make priority level higher
- allow process to be allocated resource

- SJF(Shortest Job First), process with longer time can never get resource
- HRN(Highest Response-ratio Next) take waiting time into account

- MLQ(MultiLevelQueue)
- MLFQ: take aging into account
