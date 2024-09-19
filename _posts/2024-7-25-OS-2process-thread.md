---
title: Process, Thread
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ Process

> programs that are dispatched from the ready state and are scheduled in the CPU for execution. <br>
> 메모리 상에서 실행중인 프로그램 <br>

1️⃣ **System call**: to create process <br>

💡 System call <https://soheeparklee.github.io/posts/OS-5systemcall/> <br>

2️⃣ **Process has own address space(code, heap, stack)** <br>

- `Code`: memory(program command)
- `Data`: global variables, static variables, arrays
  - reset data: saved in data
  - not reset data: saved in bss
- `Heap`: dynamic allocation `new()`, `malloc()`
- `Stack`: local variable, parameter, return value (temporary)

<br>

3️⃣ One process has each address space, <br>
and **cannot** access other process's variable or data <br>

<br>

4️⃣ For another process to access other process's resources <br>
need to use **IPC(Inter Process Communication)** to communicate <br>
💡 IPC <https://soheeparklee.github.io/posts/OS-7IPC/> <br>

<br>

5️⃣ One process has minimum one thread <br>

✔️ **Two types of process**

- OS process
- user process

<br>

✔️ **Disadvantages of process**

- 👎🏻 Long time to create
- as process has own resources and space
- 👎🏻 difficult to communicate among process(IPC)
- 👎🏻 process _context switching_ is inefficient, big overhead

## ✅ Thread

> **CPU 사용의 기본 단위** <br>
> segment of a process <br>
> process = consisted of multiple threads <br>
> 프로세스 안에서 실행되는 단위 <br>

✔️ **Thread is consisted of...**

- threadID
- program counter
- register set, stack

<br>

1️⃣ Only gets **individual stack** allocated <br>

- ⭐️ share other areas with other thread(code, data, heap)
- ⭐️ but has own stack
- when one thread changes one resource, other `sibling thread` can also see the change immediately

<br>

2️⃣ when one process is created, minimum one thread is also created <br>

- no thread outside process

<br>

✔️ **Advantages of thread**

- created to complement process
- 👍🏻 creation, termination fast
- 👍🏻 overhead ⬇️
- 👍🏻 communication among thread is easy and fast
  - share process memory, resource
  - threads can communicate without the help of kernel
- 👍🏻 smaller work unit than process
- 👍🏻 fast context switching

<br>

✔️ **Disadvantages of thread**

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

✔️ **private space**

- thread code space
- local variable for thread
- _stack_

✔️ **shared space**

- data
- code
- heap

✔️ **kernel stack**

<img width="326" alt="Screenshot 2024-09-08 at 00 59 04" src="https://github.com/user-attachments/assets/b7e3ab72-917c-421b-b48a-c5d2c20309b2">

<br>

> 💡 **Which space has faster access speed? Stack 🆚 Heap** <br>
>
> > Stack has faster allocation, deallocation speed <br>

- **Stack** uses space that is already allocated
- Allocation in stack means changing pointer in already allocated space

  - 👍🏻 Simple CPU Instrucion, faster
  - 👎🏻 However, stack has very little space
  - 👎🏻 Cannot use stack for all thread

- **Heap** needs space to be allocated
- Allocation in heap means allocating new space caculating
  - required chunk,
  - current memory fragmentation...
  - 👎🏻 require more CPU Instruction

## Kernel level thread 🆚 User level thread

✔️ **Kernel level thread**

> inside kernel

- managed by OS kernel
- OS handles the thread directly
- each kernel level thread has its own context
- 🛠️ Java thread, POSIX thread on Linux

- 👍🏻 true parallelism
- 👍🏻 execution continuity
- 👍🏻 acess to system resources
- 👎🏻 more time to create, manage, context swithcing
- 👎🏻 more overhead on kernel

<img width="169" alt="Screenshot 2024-09-19 at 11 09 31" src="https://github.com/user-attachments/assets/149de8ce-6b6f-4ce3-8b74-b62e965af54c">

✔️ **User level thread**

> outside kernel

- managed by user-level library
  - created, managed by thread library
- no intervention from OS kernel ❌

- 👍🏻 faster than kernel level
- 👍🏻 no overhead of kernel thread
- 👍🏻 highly portable: can be implemented across various OS
- 👎🏻 limited use of multiprocessing
- 👎🏻 no scheduling priority based on overall system(do not know which thread will operate first)
- 🛠️ fine control over threading

<img width="163" alt="Screenshot 2024-09-19 at 11 11 07" src="https://github.com/user-attachments/assets/896e5fe3-1cde-4195-aad2-63f58072dd06">

## Mode switch 🆚 Process switch

✔️ **Mode switch**

> user level mode ➡️ kernel mode

- use system stack

✔️ **Process switch**

> context swithcing

- change currently running process, change to new process

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

## ⭐️ Context Switching

> change process state to another state <br>

- to change to another process
- 1️⃣ save current process context, state so that it can be restored later <br>
  - save current process `PCB(Process Control Block)`
- 2️⃣ then load context or state of another process <br>
- 👎🏻 since each process has memory allocated, if heavy jobs are run, might have overhead problem.

#### ❓ When does context switching occur?

✔️ **Multitasking**

- processes take tuen according to OS scheduler
- each process is allocated CPU

✔️ **Interrupt handling**

- when exception occurs, context switching occurs
- I/O request
- time slice expired: CPU use time expire
- for a child: create child process
- wait for an interrupt

✔️ **User and kernel mode switching**

- change between user and kernel mode

## ✅ Multi Processing

> one program to be consisted of seveal processes <br>
> processes working in parrallel <br>
> increase power of a system <br>

- asymmetric multi processing
- symmetric multi processing

- 👍🏻 secure(solve memory invasion problem at OS level) <br>
- 👍🏻 save cost(if all CPUs share data in one disk)
- 👍🏻 as process has independent resource, does not affect other processes
- 👎🏻 each process has each memory, if lots of context switching ➡️ overhead problem<br>
- 👎🏻 might be slow

> 💡 **When should we use multi processing instead of multi threading?** <br>
>
> > - need distinction betweeen process memory <br>
> > - need process to have independent space address <br>

## ✅ Multi Threading

> normally, one thread in one process <br>
> multiple thread in one process <br>

- 👍🏻 multiple thread is made for increading computing **speed** of the system
- 👍🏻 **shares** address space, resources(unlike process) thus can **save time, resource** <br>
- 👍🏻 communication among thread is efficient, use heap
- 👍🏻 thread context switching is faster than process context switching

- 👎🏻 security <br>
- 👎🏻 if one thread breaks data space, other threads will be affected(since they share memory) <br>
- 👎🏻 need synchronization
- 👎🏻 deadlock
- 👎🏻 testing, debugging more difficult
- 💊 could be prevented by **Critical Section** method <br>

> 💡 **When should we use multi threading instead of multi processing?** <br>
>
> > - to save resource allocation, as threads share resource <br>
> > - communication between thread is cost effective <br>
> > - 👎🏻 however, need to be cautiious about resource sharing! <br>

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
