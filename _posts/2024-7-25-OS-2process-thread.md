---
title: Process, Thread
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ Process

> programs that are dispatched from the ready state and are scheduled in the CPU for execution. <br>
> 메모리 상에서 실행중인 프로그램 <br>

- **system call**: to create process

💡 System call <https://soheeparklee.github.io/posts/OS-5systemcall/> <br>

- ⭐️ has own address space(code, heap, stack)

- **Code**: memory(program command)
- **Data**: global variables, static variables, arrays
  - reset data: saved in data
  - not reset data: saved in bss
- **Heap**: dynamic allocation `new()`, `malloc()`
- **Stack**: local variable, parameter, return value (temporary)

- 👎🏻 Long time to create
- as process has own resources and space
- 👎🏻 difficult to communicate among process
- 👎🏻 process context switching is inefficient, big overhead

## ✅ Thread

> segment of a process <br>
> process = consisted of multiple threads <br>
> 프로세스 안에서 실행되는 단위 <br>

- gets stack allocated
- ⭐️ share other areas with process
- ⭐️ but has own stack
- when one process is created, minimum one thread is also created

- 👍🏻 created to complement process
- 👍🏻 creation, erasure fast
- 👍🏻 overhead ⬇️
- 👍🏻 communication among thread is easy and fast
- 👍🏻 smaller work unit than process

<br>

- 👎🏻 when thread is created, use memory, CPU
- 👎🏻 if there is too much thread, `synchronization`, `resource sharing` problem might happen

![Screenshot 2024-07-25 at 11 30 17](https://github.com/user-attachments/assets/d8edfbe9-69a3-4be7-adc3-8452410f2561)

## ☑️ Thread address space

- In multithreading, all thread in same process share
  - code
  - data
  - heap area
- Stack area is not shared
- Bc of resource sharing, problems such as synchronization can occur

- private space
- shared space
- kernel stack

✔️ **private space**

- thread code space
- local variable for thread
- _stack_

✔️ **shared space**

- data
- _heap_

✔️ **kernel stack**

<img width="326" alt="Screenshot 2024-09-08 at 00 59 04" src="https://github.com/user-attachments/assets/b7e3ab72-917c-421b-b48a-c5d2c20309b2">

> **Which space has faster access speed? Stack 🆚 Heap** <br>
>
> > Stack has faster allocation, deallocation speed <br>

- Stack uses space that is already allocated
- Allocation in stack means changing pointer in already allocated space
  - 👍🏻 Simple CPU Instrucion, faster
  - 👎🏻 However, stack has very little space
  - 👎🏻 Cannot use stack for all thread

<br>

- Heap needs space to be allocated
- Allocation in heap means allocating new space caculating
  - required chunk,
  - current memory fragmentation...
  - 👎🏻 require more CPU Instruction

## Process 🆚 Thread

- both are `units of work` on a computer
- process: has own address space, resources, independent
- thread: shares address space, resources with other threads
  - only has stack
  - operates within process

## ☑️ Processing

- when lots of memory, resources are needed
- able the use to memory space and resource to be seperated

## ☑️ Threading

- when there is a lot of work
- parallel threading
- able work to be done in order

## ☑️ Thrashing

- when there is less SWAP space
- occurs when there is frequent page pansion
- CPU usage ⬆️

## ✅ Multi Process

> one program to be consisted of seveal processes <br>
> processes working in parrallel <br>
> increase power of a system <br>

- asymmetric multi processing
- symmetric multi processing

👍🏻 secure(solve memory invasion problem at OS level) <br>
👎🏻 each process has each memory, overhead problem ➡️ context switching <br>

## ⭐️ Context Switching

- save process context, state so that it can be restored later <br>
- then load context or state of another process <br>
  👍🏻 since each process has memory allocated, if heavy jobs are run, might have overhead problem. <br>

## ✅ Multi Thread

> multiple thread is made for increading computing speed of the system

- 👍🏻 shares address space, resources(unlike process) thus can save time, resource <br>
- 👎🏻 security <br>
- if one thread breaks data space, other threads will be affected(since they share memory) <br>
  ➡️ could be prevented by **Critical Section** method <br>

## ⭐️ Critical section

> when one thread is chaning the value of shared data, <br>
> prevents from other thread accessing the data <br>
> only one thread at a time <br>

## ⚠️ Synchronization

Synchronization <https://soheeparklee.github.io/posts/JAVA_multiThread/#-server-multithread> <br>

## 📌 Semaphore, Mutex, Spinlock

Semaphore, Mutex, Spinlock <https://soheeparklee.github.io/posts/OS-11semapore/> <br>

## 📌 Deadlock

Deadlock <https://soheeparklee.github.io/posts/OS-9deadlock/> <br>

## ⭐️ Can the area created by a thread be accessed by other threads?

- YES
- need synchronization
- or shared vaiable among thread

## 💡 Reference

Process/Thread <br>
<https://www.geeksforgeeks.org/difference-between-process-and-thread/> <br>

Multi Processing/Multi Thread <br>
<https://www.geeksforgeeks.org/difference-between-multiprocessing-and-multithreading/> <br>

Context Switching <br>
<https://www.geeksforgeeks.org/context-switch-in-operating-system/> <br>
