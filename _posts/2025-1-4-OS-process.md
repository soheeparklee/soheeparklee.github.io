---
title: KOCW_Process/ VM / Context Switching
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ Program

> 특정 작업을 수행하는 일련의 명령어들의 모음

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

## ✅ Process

> Program in execution <br>
> 운영체제로부터 자원을 할당받는 작업 단위 <br>
> 이 떄 자원: CPU 할당 시간/code, data, stack, heap <br>

- 프로세스는 독립적인 개체
- 하나의 프로그램을 여러번 실행 ➡️ 여러개의 프로세스가 메모리에서 실행

## ✅ Process context

> process가 현재 어떤 상태에 있는가? <br>
> 시간에 따라서 변한다 <br>

- 이 프로세스는 CPU를 얼마나 썼는가?
- 메모리를 얼마나 가지고 있는가?
- 함수 어디를 실행하고 있는가?
- OS는 이 프로세스의 문맥을 아주 중요하게 생각한다.

- ❓ 프로세스 문맥은 어디에 쓰일까?
- time sharing 시스템에서 각 프로세스는 짧은 시간동안 CPU를 사용하고, 다른 프로세스에게 또 CPU를 넘긴다.
- 따라서 CPU를 넘겨받아 이어서 사용하려고 할 때, 이전에 수행했던 작업을 이어서 수행하기 위해 `프로세스 문맥`이 필요하다.
- ➡️ `process context`를 사용헤 `context switching`을 한다.

#### ☑️ process context 종류

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

## ✅ 프로세스 주소 공간

- `해당 명령을 담은 프로그램의 주소 영역/공간`은 `코드 code`, `데이터 data`, `스택stack`으로 구분된다.

- ✔️ `code`: **컴파일 타임에 할당**

  - CPU에서 수행할 기계어
  - CPU는 `code`영역에 위치한 명령어를 하나씩 가져와 처리
  - 우리가 작성한 프로그램 함수들의 코드가 CPU에서 실행될 수 있도록 기계명령어로 변환되어 저장됨
  - 프로스램 소스 코드
  - `hex` 또는 `binary`형태

- ✔️ `data`: **컴파일 타임에 할당**

  - 프로그램이 실행되다가 메모리를 사용하는 데이터
    - 전역 변수 `global variable`등 프로그램이 사용하는 데이터 저장
  - (`global 변수`, `배열`, `static 변수`)
  - 프로그램 시작과 동시에 할당, 프로그램 종료되어야 메모리에서 소멸

  - `data`안에는 `BSS(Block Stated Symbol)`이라는 영역이 존재
  - 초기화되지 않거나/ 초기화를 0으로 하거나/ 초기화를 NULL로 한 전역변수와 정적 변수는 `BSS`에 위치
  - ❓ 목적: 공간을 효율적으로 활용하기 위해
  - 예를 들어 _크기가 큰 배열을 선언만 하고 값은 넣지 않는 경우_, 크기만큼 공간을 할당해주지 않고 `BSS`에 올려 공간 절약

- ✔️ `stack`: **런타임에 할당**

  - `local 변수`, `parameter`위치
  - 어떤 함수를 호출한 후 return할 곳
  - 호출된 함수의 수행을 마치고 복귀할 주소 및 데이터 임시로 저장
  - 함수의 호출과 함께 할당`push`되고, 함수 호출이 완료되면 메모리에서 소멸`pop`
  - 메모리의 _높은_ 주소에서 _낮은_ 주소 방향으로 할당

- ✔️ `heap`: **런타임에 할당**

  - 프로그래머에 의해 메모리 공간이 동적으로 할당되고 해제되는 영역
  - `C`언어의 `malloc()`, `free()`함수
  - 메모리의 _낮은_ 주소에서 _높은_ 주소 방향으로 할당된다.

#### 컴파일 타임 🆚 런타임

- 컴파일 타임: 사람이 작성한 `소스코드`가 **컴파일**이라는 과정을 통해 `기계어 코드`로 변환되는데 걸리는 시간
- 런타임: 컴파일을 마친 기계어가 실행되는 시간, 프로그램이 동작하는 시간

## ✅ 프로세스의 상태

- ✔️ **new**
- 프로세스 생성 후
- 프로세스를 위한 각종 자료 구조는 생성되었지만
- 메모리 획득 승인은 받지 못함
- `admitted` 받아야 `running`으로 갈 수 있음

- ✔️ **terminated**
- 프로세스가 종료되었으나 운영체제가 그 프로세스와 관련된 자료구조를 정리 중

- ✔️ **Running**
- CPU에서 기계어를 *실행*하는 프로세스는 _한 개_
- 현재 CPU를 잡고 instruction을 수행 중

- ✔️ **Ready**
- CPU를 쓰려고 _기다리는_ 프로세스
- 메모리 등 다른 조건은 모두 만족했고, 기다리고 있음
- `ready`상태에 있는 여러개의 프로세스 중 하나가 CPU를 할당받는 과정을 **CPU 디스패치**라고 한다.

- ✔️ **Blocked(wait, sleep)**
- CPU를 줘봐야 소용이 없는 프로세스
- (오래걸리는 I/O작업 하고 있는 프로세스)

- OS는 `data`의 `PCB`를 통해서 각 프로세스의 상태를 관리하고 있다.
- 각 `queue`에 줄을 세워서 관리
- 그리고 CPU는 `CPU queue`다음에 있는 프로세스에게 CPU를 준다.
- 그러다가 I/O가 끝나서 `interrupt`가 들어오면 `interrupt 요청한 프로세스`의 상태를 `ready`로 바꾸고 그 프로세스에게 CPU를 준다.

- ✔️ **Suspended(stopped)**
- 외부적인 이유로 프로세스의 수행이 정지된 상태
- 프로세스는 통째로 disk에 `swap out`된다.

  - 메모리가 꽉 차서 운영체제 `swapper`이 디스크로 쫒아냄
  - 사용자가 프로세스를 일시 정지함

#### Blocked 🆚 Suspended

- 공통점: CPU없음

- Blocked:

  - 자신이 요청한 event가 만족되면 ready
  - 프로세스가 CPU만 빼앗겼을 뿐, I/O장치에서 뭔가 작업을 하고 있음
  - 적극적으로 일을 하고 있기는 함

- Suspended:
  - 메모리에 없는 상태
  - 외부(운영체제 또는 사람)에서 resume해 주어야 active
  - 메모리가 필요한 일을 아예 못함!
  - 하지만 I/O는 할 수 있음

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

4. 사용자가 프로세스를 일시정지시킴(break key)
➡️ suspended

5. 시스켐이 여러 이유로 프로세스를 중단시킴
(메모리에 너무 많은 프로세스가 올라옴)
➡️ suspended

```

- ❓ `프로세스 A`가 `running`하다가 `system call`로 운영체제를 호출하면 `프로세스 A`의 상태는?
- 프로세스 A 입장에서는 계속 `running`이다.
- CPU는 없지만 I/O입력이라든가 계속 일을 하고 있으니까
- 다만 전에는 `user mode`였다면 이제는 `kernel mode, monitor mode`이다.

- ❓ `프로세스 A`가 `running`하다가 `interrupt`가 들어오면 `프로세스 A`의 상태는?
- `프로세스 A`가 CPU를 가지고 있었는데 디스크가 `interrupt`
- CPU는 운영체제에게 넘어간다.
- `프로세스 A`의 상태는 본인과 상관없는 이유로 CPU가 넘어갔지만, `running`이다.
- `interrupt`직전에 돌고 있던 프로세스를 그냥 `running`하고 있다고 간주한다.
- 다만 마찬가지로, 전에는 `user mode`였다면 이제는 `kernel mode, monitor mode`이다.

## ✅ PCB에 어떤 내용이 들어있는가

> PCB: Process Control Block <br>
> in OS kernel `data` <br>
> 운영체제가 각 프로세스를 관리하기 위해 **프로세스당** 유지하는 정보 <br>

#### ☑️ PCB 구성 요소(구조체로 유지)

<img width="690" alt="Screenshot 2025-01-05 at 13 51 32" src="https://github.com/user-attachments/assets/945ab5b8-0f85-456b-be32-3e5d83826e53" />

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

> CPU 제어권을 한 프로세스에서 다른 프로세스로 넘겨주는 과정 <br>
> 반드시 한 프로세스`process A`에서 다른 프로세스`process B`로 넘어가야 함 <br>

#### ☑️ Context Switching 과정

```
- system call, interrupt occurs
- OS saves process context(PC and registers) to process PCB
- change process state to running ➡️ blocked/ready/exit
- put PCB in the appropriate queue(block queue, ready queue)
- select next process to be run
- change process state to running
- bring process context(PC and registers) from process PCB
- CPU runs process
```

#### ☑️ CPU가 다른 프로세스에게 넘어갈 때 OS역할

```
1. CPU를 내어주는 프로세스 상태를 그 프로세스 PCB에 저장
2. CPU를 새롭게 얻는 프로세스 상태를 PCB에서 읽어옴
```

- CPU에서 실행시킬 프로세스를 변경하기 위해
- 원래 실행중이던 프로세스의 `process context`를 자신의 `PCB`에 저장하고
- 새로운 프로세스의 `process context`를 세팅하는 과정

- 👎🏻 `Context Switching`은 context를 `PCB`에 저장하고 또 context를 불러오는 두 가지 과정이 필요하므로
- 모드 변경에 비해 훨씬 큰 overhead

## 🆚 Mode switch

> Mode switch: 프로세스 실행 중 `interrupt/system call`이 발생하여 CPU제어권이 OS로 넘어가 운영체제 커널 코드가 실행되는 것

- CPU제어권이 운영체제로 넘어가기 전 현재 실행중인 프로세스의 `process context`를 `PCB`에 저장하지만,
- 이는 context swtiching은 아니다.
- 왜냐하면 프로세스의 실행 모드만이 유저모드 ➡️ 커널 모드로 바뀌는 것 뿐
- CPU를 점유하는 프로세스가 다른 프로세스로 바뀌지는 않기 때문
- 오버헤드가 적다.

- Context Switch와 Mode switch 공통점:
- 현재 CPU에서 실행중인 프로세스의 `process context`를 `PCB`에 저장한다.

- Context Switch와 Mode switch 차이점:
- Context Switch가 오버헤드가 훨씬 크다

#### context switching ⭕️❌

<img width="546" alt="Screenshot 2025-01-04 at 16 55 53" src="https://github.com/user-attachments/assets/26ff5235-6bfb-441f-b18b-ee81a2b15ef6" />

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

- context switching ❌ mode switching

```
CPU Process A running: 🏴 user mode
🛑 interrupt or system call
ISR or system call function: 🏳️ kernel mode
➡️ back to user mode
CPU Process A running: 🏴 user mode

➡️ This is NOT context switching, this is mode switching
💡 OS does save context to PCB
- user mode에서 kernelmode 로 바뀌는 건 부담이 비교적 크지 않음
- 모든 context를 다 save할 필요는 없으니까
```

- 공통점: OS에서 context를 `PCB`에 저장해야 함
- 🆚 차이점: context switching이 훨씬 부담이 크다, big overhead

## ✅ CPU dispatch

- process in `ready` state gets CPU

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
