---
title: Scheduling
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ Scheduling

Overhead ⬇️ / Usage ⬆️/ Stavation ⬇️

- `Batch System`: throughout(처리량) ⬆️
- `Interactive System`: fast reaction time ⬆️ less waiting time ⬇️
- `Real-time System`: deadlines

## ✅ Types of Scheduling

1. Preemptive Scheduling

   - when OS takes control of CPU
   - difficult to expect runtime

     - Interrupt
     - I/O event completion
     - I/O event wait
     - exit

   - Priority Scheduling
   - Round Robin
   - Multi level Queue
   - Multi level Feedback Queue

2. Non Preemptive Scheduling

   - run until process terminates, event such as I/O occurs
   - easier to except runtime

     - I/O event wait
     - exit

   - FCFS(First Come First Served)
   - SJF(Shortest Job First)
   - HRN(Highest Response-ratio Next): caculate priority

## ✅ Measure Scheduling

- Response Time
- Turnaround Time
