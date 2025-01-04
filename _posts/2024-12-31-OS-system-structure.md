---
title: KOCW_Process & Thread
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

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

- ✔️ 프로세스 주소 공간
- 자신의 메모리 공간 `data`에 무엇을 가지고 있는가?
- `stack`에 몇 개의 함수가 있는가?

- ✔️ 프로세스 관련 커널 자료 구조
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

> CPU를 한 프로세스에서 다른 프로세스로 넘겨주는 과정

#### ☑️ CPU가 다른 프로세스에게 넘어갈 때 OS역할

```
1. CPU를 내어주는 프로세스 상태를 그 프로세스 PCB에 저장
2. CPU를 새롭게 얻는 프로세스 상태를 PCB에서 읽어옴
```

#### context switching

- context switching ❌

```

```

- context switching ⭕️

```

```

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

CPU
