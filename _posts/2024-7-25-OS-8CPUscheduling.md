---
title: Scheduling
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ Scheduling

> order plan to allocate CPU to thread <br>
> process on ReadyQueue will be scheduled <br>
> First in queue has CPU first <br>

Overhead ⬇️ / Usage ⬆️/ Stavation ⬇️

- `Batch System`: throughout(처리량) ⬆️
- `Interactive System`: fast reaction time ⬆️ less waiting time ⬇️
- `Real-time System`: deadlines

> Why do we need scheduling? <br>
>
> > to use CPU efficiently <br>
> > decide how to allocate CPU to process <br>

## ✅ Types of Scheduling

**1. Preemptive Scheduling(선점)**

- preemtive: forestall, pre-empt

- OS can forcefully take control of CPU
- 👍🏻 process with priority can be executed
- 👍🏻 fast response time
- 👎🏻 if all processes have priority? overhead
- 👎🏻 difficult to expect runtime

  - Interrupt
  - I/O event completion
  - I/O event wait
  - exit

- Priority Scheduling
- Round Robin
- SRTF
- Multi level Queue
- Multi level Feedback Queue

**2. Non Preemptive Scheduling(비선점)**

- run until process terminates, event such as I/O occurs
- 👍🏻 fair to all processes
- 👍🏻 easier to except runtime
- 👎🏻 process that can end fast has to wait for long process to wait

  - I/O event wait
  - exit

- FCFS(First Come First Served)
- SJF(Shortest Job First)
- HRN(Highest Response-ratio Next): caculate priority

## ✅ Types of Scheduling based on algorithm

### ✔️ First come First Served

- first arrive in queue,
- then gets CPU first

### ✔️ Shortest Job First

- complement `FCFS`
- prioritize job that has shortest time
- If process has long duration time, might never be allocated CPU ➡️ **starvation**

### ✔️ Highest Response-ratio Next

- complement `SJF`(unfair CPU allocation based on time)
- make priority based on waiting time, time needed to perform
- priority = (`waiting time` + `time to process`)/`time to process`

### ✔️ Shortest Remaining Time First

- `burst time`: time that currently processing process needs before terminating
- If process that has shorter `burst time`, forcefully take CPU
- when new process arrives, new shceduling
- **starvation**

### ✔️ Round Robin

- `Time Quantum`: minimum time needed to process
- allocate equal `Time Quantum` to all process ordered by `FCFS`
- modern CPU scheduling method
- when `Time Quantum` ends, process goes to the back of `Ready Queue` to wait again
- 👍🏻 when process time is random
- 👍🏻 can save process context

## ✅ Measure Scheduling

- Response Time
- Turnaround Time
