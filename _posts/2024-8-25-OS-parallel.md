---
title: Multi Processing/ Multi Programming/ Multi Tasking/ Multi Threading
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ Multi Processing

> several CPUs <br>

- each CPU can execute different task
- parallel processing

- in process, work in parallel
- operate multiple jobs at the same time
- 👍🏻 reduce time

- 🛠️ used in cloud
- 🛠️ multi-core

## ✅ Multi Programming

> multiple programs are loadad into memory <br>
> CPU switches between them <br>

- ⭐️ several program in memory
- OS schedule which program to be run
- **CPU switching**
- 👍🏻 Optimize CPU usage

- 🛠️ run text editor and compiler simultaneously

💡 Paging <https://soheeparklee.github.io/posts/OS-12paging/>

## ✅ Multi Tasking

<img width="430" alt="Screenshot 2024-09-10 at 16 26 51" src="https://github.com/user-attachments/assets/f33f41f5-f219-4345-8302-160d6f566090">

> OS execute multiple tasks simultaneously <br>
> extension of multiprogramming, but more general sense <br>

- **Task**: unit of work in OS/ command for work <br>
- process보다 확장된 개념 <br>
- **CPU switching**
- appears that CPU is executing two tasks at the same time

- OS handles multi tasking
- tasks have independent memory, do not share resources
- need IPC for communication between tasks
- 👍🏻 has independent memory, can be executed memory

- cooperative multitasking
- preemptive multitasking: force CPU switch

- 🛠️ modern OS, run web browser, text editor, music player
- general purpose OS
- run multiple Apps

## ✅ Multi Threading

> multiple thread in one process

- threads share resource like memory, but execute independently

- 👍🏻 data sharing among thread
- 👍🏻 efficient communication

- 🛠️ multiple client requests
