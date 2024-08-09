---
title: Interview_Process/Thread/Deadlock/Paging/Semaphone/Mutex/Segmentation/Virtual Memory
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

<img width="1112" alt="Screenshot 2024-08-08 at 13 05 37" src="https://github.com/user-attachments/assets/ed32694f-f9be-436a-86bf-f6373978e11a">

## Process 🆚 Thread

- Process:
  - program running on memory
  - has own address, resource

<br>

- Thread: work unit in process
  - does not have independent address, resource
  - only has independent stack

💡 <https://soheeparklee.github.io/posts/OS-2process-thread/> <br>

## ✅ Why use multi threading instead of multi processing?

> **System call** to create process and allocate resource decrease <br>
> communication between thread is costless than communication between process(IPC) <br>
> However, need to take **synchronization** into account for multitasking <br>

## ✅ Context Switching?

> 하나의 프로세스가 CPU를 사용 중인 상태에서 다른 프로세스가 CPU를 사용하도록 하기 위해, 이전의 프로세스 상태를 보관하고 새로운 프로세스의 상태를 적재하는 작업 <br>
> 한 프로세스의 문맥은 그 프로세스의 PCB에 기록됨 <br>

💡 <https://soheeparklee.github.io/posts/OS-6pcb/> <br>

## Semaphore 🆚 Mutex

- Semaphore:

  - 공유자원에 접근할 수 있는 최대 허용치만큼만 동시에 사용자 접근 가능
  - 스레드들은 리소스 접근 요청
  - 세마포어는 카운트가 하나씩 줄어들게 되며 리소스가 모두 사용중인 경우(카운트=0) 다음 작업은 대기

- Mutex:
  - 제어되는 섹션에 하나의 스레드만 허용
  - 해당 섹션에 접근하려는 다른 스레드들을 강제적으로 막음
  - 첫번재 스레드가 해당 섹션을 빠져나올 때까지 기다려야 함

💡 <https://soheeparklee.github.io/posts/OS-11semapore/> <br>

## ✅ What is deadlock?

> What is deadlock? <br>
>
> > When process cannot get the resource, and cannot work <br>
> > occurs when several threads are trying to gain access to shared resource <br> <br>

> Four conditions of deadlock <br>
>
> > - **Mutual exclusion**: shared resouce requires exclusive control, inshareable <br>
> > - **Resource holding**: thread is waiting for another resource to be released while holding onto an allocated resource <br>
> > - **circular wait**: each process waiting for a resource held by the next process in the chain <br>
> > - **no preemption**: thread cannot get a resource until the resource is finished by another thread <br> <br>

> How to avoid deadlock? <br>
>
> > prevention: eliminate condition <br>
> > (for no-preemtion: let go of the holding resource) <br>
> > avoidance: run algorithm on requests to check for a safe state <br>
> > detection <br>
> > recovery <br>

## ✅ Memory Hierchy

- Register
- Cache
- RAM
- Hard Disk

💡 <https://soheeparklee.github.io/posts/4-WEB_os_architecture/> <br>

## ✅ Memory Allocation Algorithm

- First fit:

  - search memory from start
  - allocate the first space that has enough storage

- Next fit:

  - begin search from the last allocated place

- Best fit:

  - search all the memory to find the best place to allocate

## ✅ Paging, Segmentation

> Paging <br>
>
> > optimize memory usage <br>
> > divide memory into fixed-size pages <br> <br>

> Segmentation <br>
>
> > divide memory into various size, more flexible <br>

💡 <https://soheeparklee.github.io/posts/OS-12paging/> <br>

## ✅ Page Fault, Virtual Memory

> Page Fault <br>
>
> > when a running program accesses a memory page that is mapped into virtual address space <br>
> > but not loaded on physical memory <br>
> > OS has to replace one of the existing page with newly needed page <br>
> > thus, the need for page replacement algorithm <br> <br>

> Virtual Memory <br>
>
> > memory management technique <br>
> > create an illusion of memory using RAM + disk storage <br>
> > 실제 메모리 안에 공간이 부족하면, 현재 사용하고 있지 않은 데이터를 빼내어 가상 메모리에 저장해두고, 실제 메모리에선 처리만 하게 하는 것이 가상 메모리의 역할이다. <br>
> > 즉, 실제 메모리에 놀고 있는 공간이 없게 계속 일을 시키는 것. 이를 도와주는 것이 '가상 메모리' <br> <br>

## ✅ Page Replacement Algoirthm

- FIFO: keep memory in queue, oldest page is in front
- LRU: Least recently used 최근 가장 오랫동안 사용하지 않은 페이지
- LFU: Least frequently used 사용 빈도 적은 페이지
- MRU: Most recently used

💡 <br>
