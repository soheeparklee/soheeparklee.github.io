---
title: Interview_Process/ Thread
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

### ✅ 프로그램에 대해 설명해주세요.

- 특정 작업을 수행하는 명령어
- 디스크에 저장되어 있다가 실행되면 메모리에 실행파일이 적재

### ✅ 프로세스에 대해 설명해주세요.

- 디스크에 있던 프로그램이 메모리에 적재되어 CPU를 사용하려고 하는 상태
- OS로부터 자원을 할당받는 작원 단위
- 독립적인 개체

### ✅ What is CPU dispatch?

- `ready`상태에 있던 프로세스가 CPU를 얻는 것
- `CPU scheduler`이 다음번에 실행될 프로세스를 결정하면 `CPU dispatcher`이 프로세스에게 CPU 제어권을 준다.

### ✅ 프로그램이 실행되면 그 일련의 과정을 설명해주세요

- 디스크에 저장되어 있던 프로그램 실행
- 메모리에 실행 파일 적재
- 그 프로그램 만의 `address space`가 만들어진다.
- 프로그램이 프로세스가 되고
- CPU를 기다리는 `ready queue`에서 기다리기

### ✅ 프로세스 문맥`context`에 대해 설명해주세요.

- all the information OS needs to manage, execute process
- 프로세스가 현재 어떤 상태에 있는지
  <br>

- ❓ `context`이 필요한 이유
- `time sharing`을 기반으로 하는 시스템에서 `Context Switching`이 이루어져야 하는데
- 이 때 `context`에다가 프로세스의 상태를 저장, 나중에 또 이어서 실행
  <br>

- ✔️ CPU수행 상태 `PC program counter`, `registers`
- ✔️ `kernel` context
- ✔️ `PCB`

### ✅ 프로세스의 메모리 공간에 대해 설명해주세요.

- 프로세스 `address space`
- **memory** that is allocated process by OS
- ✔️ `code`: CPU 기계어 ➡️ compile time
- ✔️ `data`: global변수, static변수 저장 ➡️ compile time
- ✔️ `stack`: local변수, parameter ➡️ runtime

### ✅ 프로세스 `context` 🆚 프로세스 `address space`

- 프로세스 `context`: process state, info of process that OS needs to manage process
- 프로세스 `address space`: memory allocated to process

### ✅ 프로세스 제어블록(PCB)에 대해 설명해주세요.

> process control block

- OS가 관리상 사용하는 정보: `PID`, scheduling information, priority
- `PC`, `registers` 같은 `context`
- OS kernel의 `data PCB`, `PC, register`: CPU를 빼앗기 전 어디까지 실행했는지 저장
- 메모리 관련
- 파일 관련

### ✅ 문맥교환(context switch)에 대해 설명해주세요.

- `context switch`: 한 프로세스에서 다른 프로세스로 CPU제어권 넘겨주기
  <br>

- 1. 프로세스A 실행 중
- 2. 프로세스A가 I/O가 필요하여 `system call` 또는 인터럽트
- 3. 프로세스A의 `context`를 `PCB`에 저장
- 4. 프로세스A의 상태를 `ready`, `blocked`
- 5. `CPU scheduling`을 통해 다음 프로세스 선정
- 6. 다음 프로세스인 프로세스B의 `context`를 `PCB`에서 꺼내옴
- 7. 프로세스B에게 CPU제어권 넘겨주기

### ✅ 문맥교환(context switch)이 일어났을 때 운영체제의 역할

1. 현재 실행중인 프로세스 `context`를 `PCB`에 저장 <br>
2. 다음 실행할 프로세스의 `context`를 `PCB`에서 꺼내옴 <br>

### ✅ `Context Switching`의 단점

- 오버헤드가 커진다.
- `Context Switching`를 위해서는 `OS kernel data`부분의 `PCB`에 프로세스의 `context`를 저장하고
- 새로운 프로세스의 `context`를 `PCB`로부터 불러와야 한다.
- 이 과정이 너무 많이 반복되어도 비효율적

### ✅ Compare Context switching and Mode switch

공통점: 모두 `context`를 `PCB`에 저장한다.
<br>

차이점:

- `Context switching`: CPU에서 실행되는 프로세스가 다른 프로세스로 바뀌는 것
- `Mode switch`: `user mode`에서 `kernel mode`로 또는 그 반대로 바뀌는 것.
- 프로세스에서 `system call`을 통해 또는 `interrupt`를 통해 이루어지게 된다.
- 반드시 CPU에서 실행되는 프로세스가 다른 프로세스로 바뀌는 것은 아니다.
- `Mode switch`는 `Context switching`에 비해 오버헤드가 적다

### ✅ 프로세스 수행 상태 변화 과정에 대해 설명해주세요.

- 프로세스 생성: **new**
- 메모리 할당받고 `admitted`, CPU를 기다리면: **ready**
- CPU할당: **running**
- I/O작업같이 CPU있어도 소용 없는 상태: **blocked/wait/sleep**
- 다시 CPU를 기다리면: **ready**
- 메모리가 다 차서 `SWAP`영역으로 쫒겨나면: **suspended**
- 사용자가 프로세스를 일시정지함: **suspended**
- 프로세스 종료: **terminated**

### 프로세스 상태 blocked 🆚 suspended

- 공통점: CPU 없음
- blocked: 자신이 요청한 작업이 완료되면 `ready`로 변함, CPU는 없지만, I/O같은 작업을 하고 있음
- suspended: 메모리에서 프로세스가 쫒겨남, 외부에서 다시 `resume`해줘야 `active`

### ✅ 프로그램A가 `running`하다가 `system call`로 운영체제를 호출하면?

- 프로그램A 상태는 `running` 또는 `wait/blocked`로 볼 수 있음
- 프로그램A는 I/O작업을 하고 있으므로 `running`이지만,
- CPU는 없기 때문에 `wait/blocked`
- I/O작업이 끝나면 다시 `ready`가 될 것이다.

### ✅ 프로그램A가 `running`하다가 인터럽트가 들어오면?

- 프로그램A 상태는 `ready`
- 예를 들어 `timer`인터럽트가 들어오면, CPU를 빼앗기고 다시 `ready`

### ✅ What is degree of Multiprogramming?

- 메모리는 한정되어 있으므로 일정한 양의 프로그램만 올라갈 수 있다는 것.
- `장기 스케쥴러`, `단기 스케쥴러`에서 구현,
- 너무 많은 양의 프로그램이 올라가게 되면 `단기 스케쥴러`는 `SWAP`영역으로 프로세스를 메모리에서 쫒아내버리고
- `장기 스케쥴러`는 바로 프로세스를 메모리에 올리지 않고, 어떤 것을 `ready queue`로 보낼지 결정

### ✅ 멀티 프로세스에 대해서 설명해주세요.

- 하나의 프로그램 안에서 여러개의 프로세스를 실행하는 기술
- 하나의 `부모 프로세스`가 `자식 프로세스` 생성
- 프로세스 끼리는 서로 독립적인 메모리를 가진다.
- 예를 들어 `프로그램: 크롬`을 실행하고 `프로세스: 여러개의 크롬 창`을 띄운다.

### ✅ fork() 명령어에 대해 설명해주세요.

- `부모 프로세스`가 `자식 프로세스`를 **복제해서**생성
- OS에게 `fork system call`

<br>

- 트리 계층 구조
- 각 프로세스는 서로 다른 메모리를 가지고 있고
- `자식 프로세스`는 `부모 프로세스`를 복제했기 때문에 `fork`한 시점부터 이어서 실행

### ✅ 왜 프로세스를 복제해서 생성할까?

- 매번 생성하면 그 프로세스의 자원을 다 생성해줘야 하는데
- 복제해서 사용하면 부모의 `address space`를 복사해서 물려받으므로 간단
- 그래서 부모랑 `code`, `data`, `stack` 다 똑같음

### ✅ 부모 프로세스와 자식 프로세스를 어떻게 구별하나?

- `fork`후 return값이 다르다.
- 부모: 자식의 PID, 양수
- 자식: 0

### ✅ exec() 명령어에 대해 설명해주세요.

- 부모와 다른 프로그램을 돌리고 싶으면 자식에게 `exec system call`
- `address space`에 새로운 `address space` 덮어 씌우기

### ✅ wait() 명령어에 대해 설명해주세요.

- 부모 프로세스가 자식 프로세스 수행을 기다린다.
- 부모 프로세스 `block`
- 원래 프로세스끼리는 경쟁사이지만, 부모 자식 사이에는 기다리기 가능

### ✅ exit() 명령어에 대해 설명해주세요.

- 프로세스가 수행을 마치고 자발적으로 terminate
- 자식부터 종료되어야 한다.
- 각종 자원 OS에게 반납

### ✅ abort() 명령어에 대해 설명해주세요.

- 부모가 자식을 강제종료
- 언제?
  - 자식이 할당 자원 한계치를 넘어서거나
  - 자식이 더 이상 필요없거나
  - 부모가 `exit()`하는 경우: 자동으로 자식도 다 종료, 트리 계층 구조

### ✅ 프로세스끼리 협력하는 방법에 대해서 설명해주세요.

- IPC: Inter Process Communication

- message passing
  - direct communication
  - indirect communication
- shared memory

### ✅ 공유 메모리 방식의 장점, 단점?

- 👍🏻 프로세스 협력을 통해 처리 속도 향상, 정보 공유 가능
- 👎🏻 동기화 문제, 일관성 문제

## 📌 Thread

### ✅ 쓰레드에 대해 설명해주세요.

- CPU의 최소 실행 단위로,
- 하나의 프로세스 안에서 CPU 실행 단위
- 프로세스의 `code`, `data`, `heap`은 공유하고 `stack`은 각자 가진다는 특징

- 👍🏻 빠른 통신, 빠른 쓰레드 간 `context switching`, 빠른 생성
- 👍🏻 프로세스의 `context switching`을 줄여 `overhead`감소

### ✅ 쓰레드의 메모리 공간에 대해 설명해주세요.

- 프로세스의 `heap`, `data`, `code`를 공유
- 👍🏻 빠른 쓰레드 간 `context switching`, `overhead`적음

### ✅ 쓰레드 제어블록(TCB)에 대해 설명해주세요.

- 각 쓰레드마다 OS가 `context`정보를 담고 있는 자료 구조
- 프로세스가 공유하지 않고 각자 가지는 `stack`부분
- `PC`, `registers`, `priority`, `thread ID`, `scheduling info`

### ✅ 사용자 수준 쓰레드와 커널 수준 쓰레드의 차이를 설명해 보세요.

- `kernel-level thread` 🆚 `user-level thread`
- `kernel-level thread`: 커널이 쓰레드의 존재를 알고 커널이 쓰레드 관리
  - sheduling 단위: 쓰레드
- `user-level thread`: 커널은 쓰레드의 존재를 모름, 사용자가 `thread libary`사용해서 멀티쓰레딩 프로그램 작성
  - sheduling 단위: 프로세스

### ✅ kernel-level thread 장점, 단점?

- 장점: 쓰레드 단위로 scheduling가능, 여러 쓰레드를 동시에 처리 가능
- 단점: 쓰레드 간 `context switching`

### ✅ user-level thread 장점, 단점?

- 장점: 커널의 개입이 필요 없음
- 단점: 하나의 쓰레드가 `block`되면 전체 프로세스가 `block`

### ✅ 멀티 쓰레딩 프로그래밍 대해서 설명해주세요.

- 한 개의 프로세스 작업을 여러 개의 쓰레드가 프로세스의 자원을 공유하며 작동

### ✅ 멀티 쓰레드 프로그래밍의 장단점을 설명해 주세요.

- 👍🏻 여러개의 쓰레드가 하나의 프로세스 작업 가능
- 👍🏻 `kernel-level thread`라면 하나의 thread가 `block`되어도 다른 thread가 다른 작업 가능
- 👍🏻 자원 공유 가능

- 👎🏻 공유 자원에 대한 동기화
- 👎🏻 thread간 `race condition`
- 👎🏻 하나의 thread에 문제가 생기면 전체 thread에 문제

### ✅ 멀티 프로세스대신 멀티 쓰레드를 사용하는 이유가 뭔가요?

- 👍🏻 자원 공유, 중복 자원 낭비 방지

- 👍🏻 커널의 개입 없이 쓰레드 간 통신 가능

- 👍🏻 `context switching` overhead가 작다
- `멀티 프로세스`는 `context switching`의 overhead가 크다.
- 프로세스 `context`를 `PCB`에 저장해야 되기 때문

- 👍🏻 `cache` 사용 가능
- `멀티 프로세스`는 `context switching`되면 이전 프로세스의 `cache`는 의미가 없어짐
- 하지만 `멀티 쓰레드`는 자원을 공유하기 때문에 `cache`도 사용 가능

- 👍🏻 속도가 빠르다
- 자원을 공유하므로 쓰레드 `fork`생성도 빠르다
- `멀티 쓰레드`는 공유하지 않는 부분만 교환하면 되므로 `멀티 쓰레드 context switching`이 더 빠르다

### ✅ 멀티 쓰레드 프로그래밍에서 주의할 점이 있을까요?

- 공유 자원에 대한 동기화
- 쓰레드 간 `race condition`
- `deadlock`: 공유 자원이 release될 때까지 무한정 기다림
  - `mutual exclusion`, `hold and wait`, `circular wait`, `no preemption`
- 하나의 쓰레드에 문제가 생기면 다른 쓰레드도 다 문제 발생

- 따라서 자원을 공유하기 때문에 `thread safe`하게 작성하여, `동시성 이슈`가 발생하지 않도록 한다.

### ✅ Thread-Safe하다는 의미와 그렇게 설계하는 방법을 설명해 주세요.

- `thread safe`: 여러 쓰레드가 동일 자원에 접근하더라도 `동시성 이슈`가 발생하지 않는다.
- 기본적으로 불변 객체`immutable` 활용
- `lock`을 통해 공유 자원에 접근할 수 있는 쓰레드 제한
- `mutex`: only one thread can access critical section at a time
- `semaphore`: limited number of thread can access

### ✅

### ✅

### ✅

### ✅

### ✅

### ✅

### ✅

### ✅

### ✅
