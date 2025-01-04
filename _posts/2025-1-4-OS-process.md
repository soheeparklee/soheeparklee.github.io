---
title: KOCW_Process / Process Management / VM / Context Switching
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ 컴퓨터 시스템의 작동 개요

- CPU는 매 시점 메모리의 특정 주소에 존재하는 명령을 하나씩 읽어와 수행한다.
- 이 때 CPU가 수행해야 할 **메모리 주소를 담고 있는 레지스터**를 프로그램 카운터 `Program counter, PC`라고 한다.
- 즉, CPU는 매번 프로그램 카운터가 가리키는 메모리 위치의 명령을 처리한다.

## ✅ Multi Programming

- 일반적으로 CPU는 _한 개_
- 따라서 CPU에서 명령이 수행되고 있는 프로그램도 _한 개_
- 그러나 CPU가 짧은 시간 단위로 시간을 나누어 프로그램을 수행하고 ➡️ **time sharing**
- 여러 프로그램이 메모리에 동시 적재되어 있을 수 있으므로
- *"여러 프로그램이 동시에 실행된다"*라고 말할 수 있다.

## ✅ 프로그램의 실행(Memory load)

> 프로그램이 실행되고 있다. <br>
> 1️⃣ 디스크에 존재하던 실행파일이 메모리에 적재된다. <br>
> 2️⃣ 프로그램이 CPU를 할당받고 명령이 수행된다. <br>

- 프로그램은 디스크에 저장
- 실행되면 메모리에 적재
- 운영체제 커널은 메모리에 올라가 있음
- 프로그램이 메모리에 적재되면 ➡️ 프로세스

#### 1️⃣ 디스크에 존재하던 실행파일이 메모리에 적재된다.

- 사실 메모리에 프로그램이 올라가기 전에 한 단계가 더 있음
- 바로 `Virtual Memory`
- 그 프로그램만의 `address space, 독자적인 주소 공간`이 만들어진다.
- 그 `address space`를 바로 `virtual memory`라고 한다.
- 실제로는 존재하지 않음

- 각 프로그램마다 별도의 `주소 공간(코드, 데이터, 스택)`을 가지며
- 프로그램마다 독자적으로 존재하는 주소공간을 `가상 메모리` 또는 `논리적 메모리`라고 부른다.

- 실행 파일이 메모리에 적재될 때, 일부분만 올라가고
- 나머지는 디스크의 특정 영역`swap`에 내려가 있다.
- 이는 메모리 공간을 효율적으로 사용하기 위함이다.
- 그래서 지금 당장 실행되야 할 부분만 메모리에 올라가고
- 아닌 부분들은 `swap`에 올라가 있게 된다.

<img width="498" alt="Screenshot 2025-01-04 at 12 31 14" src="https://github.com/user-attachments/assets/94e87578-3dd9-476f-9167-cbb05bf532d3" />

- `address space`는 각 프로그램마다 `0~n`까지 있고 ➡️ **virtual address**
- `physical memory`는 실제 메모리로, 하나 크게 존재한다. ➡️ **physical address**
- `physical memory`의 가장 낮은 주소에 `운영체제 커널`이 올라가고, 그 위에 현재 실행될 프로그램들이 올라가게 된다.
- 따라서 **virtual address**에서 **physical address**로 **address translation**이 필요하다.

## ✅ Virtual Memory 구성 요소

- 컴퓨터 프로그램 내부는 **함수**들로 구성되어 있다.
- 그래서 하나의 함수가 실행되는 와중에 다른 함수를 호출하고, 호출된 함수의 수행이 끝나면 다시 원래 수행하던 함수로 돌아가 프로그램을 계속 실행한다.
- 한편 프로그램이 실행되기 위해서는 `해당 명령을 담은 프로그램의 주소 영역`이 메모리 위에 올라가 있어야 한다.

- `해당 명령을 담은 프로그램의 주소 영역/공간`은 `코드 code`, `데이터 data`, `스택stack`으로 구분된다.
- `code`:
  - CPU에서 수행할 기계어
  - 우리가 작성한 프로그램 함수들의 코드가 CPU에서 실행될 수 있도록 기계명령어로 변환되어 저장됨
- `data`:
  - 프로그램이 실행되다가 메모리를 사용하는 데이터(전역변수, 배열)
  - 전역 변수 `global variable`등 프로그램이 사용하는 데이터 저장
- `stack`:
  - 어떤 함수를 호출한 후 return할 곳
  - 호출된 함수의 수행을 마치고 복귀할 주소 및 데이터 임시로 저장

## ✅ 운영체제 kernel구조

- 운영체제도 하나의 프로그램이므로, 운영체제 커널 역시 `주소 공간(코드, 데이터, 스택)`을 가진다.
- 운영체제의 목적은 `1. 아랫단의 하드웨어 자원 효율적 관리`, `2. 윗단의 응용프로그램 및 사용자에게 편리한 서비스 제공`
- ✔️ kernel `code`:
  - CPU, 메모리 등 자원 관리 부분 ➕ 사용자에게 편한 인터페이스를 제공하기 위한 부분
  - 또 시스템 콜, 인터럽트 처리 코드
  - 자원 관리 CPU scheduling, memory management위한 코드
- ✔️ kernel `data`:
  - 각 프로세스의 상태, CPU 사용 정보, 메모리 사용정보 등을 유지하기 위한 자료구조 `PCB`를 두고 있다.
  - 하드웨어, 소프트웨어를 포함해 시스템 내 모든 자원을 관리하기 위한 자료구조를 가지고 있다.
  - `PCB`: Process Table and Control Block
  - data structure used by OS to store information about specific process
  - each process has its own PCB, includes details for the OS to manage, control process
  - 현재 프로세스가 10개 실행되고 있다 ➡️ `PCB`도 10개
- ✔️ kernel `stack`:
  - 함수 호출 시 복귀주소 저장
  - 현재 실행중인 프로세스마다 **별도의** 스택을 두어 관리한다.
  - 예를 들어 `프로그램 A`가 실행되다가 운영체제를 호출하면 `stack A`에 `프로그램 A`저장해놓는 식이다

<img width="529" alt="Screenshot 2025-01-04 at 13 01 57" src="https://github.com/user-attachments/assets/ef7c83c0-ccca-4c3c-bc90-3f2f5232ee2b" />

## ✅ 사용자 프로그램이 사용하는 함수

> 사용자 정의 함수, 라이브러리 함수, 커널 함수

#### ☑️ **사용자 정의 함수**

> 프로그래머가 직접 작성한 함수

- 자신의 프로그램에서 정의한 함수

#### ☑️ **라이브러리 함수**

> 프로그래머가 직접 작성하지는 않았지만, 누군가 작성해 놓은 함수를 호출만 해서 사용하는 것

- 자신의 프로그램에서 정의하지는 않았지만, 내 프로그램에 정의된 함수
- `사용자 정의 함수`와 `라이브러리 함수`는 모두 프로그램의 코드 영역에 기계어 명령 형태로 존재한다.
- 프로그램이 실행될 때마다 `프로세스의 주소 공간`에 포함됨
- 함수 호출 시에도 자신의 `주소 공간`에 있는 `스택` 사용

#### ☑️ **커널 함수**

> 운영체제의 커널 코드에 정의된 함수 <br>
> 커널 함수를 호출하는 것이 바로 `system call`

- CPU제어권을 운영체제에게 넘겨야 한다.
- 커널함수는 `운영체제 커널의 주소 공간`에 `코드` 정의

- ✔️ 커널함수의 두 종류

  - 시스템 콜 함수
  - 인터럽트 처리 함수

- 예를 들어, `삼각 함수 sin()`은 라이브러리 함수
- `printf()` 그 자체로는 라이브러리 함수지만, 궁극적으로 특권 명령인 입출력을 수반하므로 `printf()` 내에서 커널 함수를 호출하는 시스템 콜을 동반한다.
- 일반적인 함수 호출 🆚 시스템 콜
  - 일반적인 함수 호출: 사용자 프로그램 내에 존재하는 코드 실행
  - **시스템 콜**: 운영체제라는 별개의 프로그램에 CPU를 넘겨서 실행
    - CPU를 운영체제에게 넘기기 위해서 인터럽트와 통일한 메커니즘, 즉 CPU의 인터럽트 라인을 세팅하는 방법을 사용한다.

## ✅ 프로세스의 두 가지 실행 상태

- 프로세스 A가 CPU에서 실행되고 있음
- 1️⃣ 일반적인 함수 호출(자신의 주소 공간에 정의된 코드 실행) ➡️ **사용자 모드**
  - 사용자 정의함수, 라이브러리 함수 호출
  - 모드의 변경 없이 `사용자 모드`에서 실행 지속, `modebit 1`
- 2️⃣ 커널의 시스템 콜 함수 실행 ➡️ **커널 모드**
  - `커널모드`로 진입해 커널의 주소 공간에 정의된 함수 실행 `modebit 0`
- 따라서 프로세스 실행은 `사용자 모드`와 `커널모드`를 왔다갔다 하면서 실행

## ✅ Process

> Program in execution

#### ☑️ Process context

> process가 현재 어떤 상태에 있는가? <br>
> 시간에 따라서 변한다

- 이 프로세스는 CPU를 얼마나 썼는가?
- 메모리를 얼마나 가지고 있는가?
- 함수 어디를 실행하고 있는가?
- OS는 이 프로세스의 문맥을 아주 중요하게 생각한다.

- ✔️ **CPU수행 상태**를 나타내는 **하드웨어** 문맥
- `PC program counter`를 살펴보기
- 각종 register에 어떤 값을 넣고 있는가

- ✔️ **프로세스 주소 공간**
- 자신의 메모리 공간 `data`에 무엇을 가지고 있는가?
- `stack`에 몇 개의 함수가 있는가?

- ✔️ **프로세스 관련 커널 자료 구조**
- `PCB`
- `kernel stack`
- OS의 `PCB`, `stack`에 프로세스 문맥에 대한 정보도 저장되어 있을 것임.

## ✅ 프로세스의 상태

- ✔️ **Running**
- CPU에서 기계어를 *실행*하는 프로세스는 _한 개_
- 현재 CPU를 잡고 instruction을 수행 중

- ✔️ **Ready**
- CPU를 쓰려고 _기다리는_ 프로세스
- 메모리 등 다른 조건은 모두 만족했음

- ✔️ **Blocked(wait, sleep)**
- CPU를 줘봐야 소용이 없는 프로세스
- (오래걸리는 I/O작업 하고 있는 프로세스)

- OS는 `data`의 `PCB`를 통해서 각 프로세스의 상태를 관리하고 있다.
- 각 `queue`에 줄을 세워서 관리
- 그리고 CPU는 `CPU queue`다음에 있는 프로세스에게 CPU를 준다.
- 그러다가 I/O가 끝나서 `interrupt`가 들어오면 `interrupt 요청한 프로세스`의 상태를 `ready`로 바꾸고 그 프로세스에게 CPU를 준다.

```
- new: 프로세스 생성 중
- ready: 메모리에 올라옴
- running: 기다리다가 CPU 할달 받음

1. 오래걸리는 작업이 필요함(수행하다가 I/O가 필요함)
➡️ waiting = blocked
- 오래걸리는 작업이 끝나면
➡️ ready

2. timer가 작동함
➡️ ready

3. 작업이 끝남, 종료
➡️ terminate
```

## ✅ PCB에 어떤 내용이 들어있는가

> PCB: Process Control Block <br>
> in OS kernel data <br>
> 운영체제가 각 프로세스를 관리하기 위해 프로세스당 유지하는 정보 <br>

#### ☑️ PCB 구성 요소(구조체로 유지)

<img width="198" alt="Screenshot 2025-01-04 at 17 00 20" src="https://github.com/user-attachments/assets/355bc98f-dd4c-443e-bcfe-6d729e10efeb" />

- ✔️ **OS가 관리상 사용하는 정보**
- process state, Process Id
- scheduling information, priority
- process with highest priority will get the CPU in the next turn

- ✔️ **CPU수행 관련 하드웨어 값**
- 프로세스 문맥 context
- `PC program counter`: CPU빼앗기기 전 어디까지 실행했었는지, 이어서 실행하기 위해
- (그래서 `프로세스 A`한테서 CPU 빼앗기 전에 `프로세스 A PCB`안에 저장을 해둔다. )
- registers

- CPU의 `PC, register` 🆚 OS kernel `data PCB`의 `PC, register`
- CPU의 `PC, register`: CPU가 어디까지 실행했는지, CPU연산 값 `register`에 저장
- OS kernel `data PCB`의 `PC, register`: CPU를 빼앗기 전 해당 프로세스를 어디까지 실행했는지 저장
- 각 프로세스마다 각각의 `data PCB`, 각 `PC, register`가 있다

- ✔️ **메모리 관련**
- code, date, stack위치 저장

- ✔️ **파일 관련**

## ✅ Context Switching 문맥 교환

> CPU를 한 프로세스에서 다른 프로세스로 넘겨주는 과정 <br>
> 반드시 한 프로세스`process A`에서 다른 프로세스`process B`로 넘어가야 함 <br>

#### ☑️ CPU가 다른 프로세스에게 넘어갈 때 OS역할

```
1. CPU를 내어주는 프로세스 상태를 그 프로세스 PCB에 저장
2. CPU를 새롭게 얻는 프로세스 상태를 PCB에서 읽어옴
```

#### context switching ⭕️❌

<img width="546" alt="Screenshot 2025-01-04 at 16 55 53" src="https://github.com/user-attachments/assets/26ff5235-6bfb-441f-b18b-ee81a2b15ef6" />

- context switching ❌

```
CPU Process A running: 🏴 user mode
🛑 interrupt or system call
ISR or system call function: 🏳️ kernel mode
➡️ back to user mode
CPU Process A running: 🏴 user mode

➡️ This is NOT context switching
💡 OS does save context to PCB
- user mode에서 kernelmode 로 바뀌는 건 부담이 비교적 크지 않음
- 모든 context를 다 save할 필요는 없으니까
```

- context switching ⭕️

```
CPU Process A running: 🏴 user mode
🛑 interrupt or system call or timer
ISR or system call function: 🏳️ kernel mode
➡️ Context switching
CPU Process B running: 🏴 user mode

💡 OS has to save context to PCB
- Much more burden for OS
- big overhead
(cache memory flush)
```

- 공통점: OS에서 context를 `PCB`에 저장해야 함
- 🆚 차이점: context switching이 훨씬 부담이 크다, big overhead

## ✅ 프로세스를 scheduling하기 위한 queue

> OS는 프로세스를 모두 `queue`에 넣고 관리한다.

- ✔️ **Job Queue**
- 현재 시스템 내에 있는 모든 프로세스

- ✔️ **Ready Queue**
- 현재 메모리 내에 있고
- CPU를 당장 얻어도 되는, 기다리고 있는 프로세스

- ✔️ **Device Queues**
- I/O디바이스에서 기다리고 있는 프로세스

<img width="680" alt="Screenshot 2025-01-04 at 17 02 14" src="https://github.com/user-attachments/assets/79a5d32a-8d8e-4f24-b272-8b109e302fb0" />
