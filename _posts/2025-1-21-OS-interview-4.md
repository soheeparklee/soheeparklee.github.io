---
title: Interview_Synchronization/ Semaphore/ Deadlock
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ 병행성(동시성)에대해 설명해주세요

- concurrency
- CPU는 한번에 한 개의 작업만 처리 가능
- 빠른 속도로 여러 작업을 번갈아 처리하여 사용자 입장에서는 동시에 여러 작업이 처리되는 것처럼 느껴짐
- ⚠️ 공유 자원에 대해 문제가 생길 수 있어 `synchronization`필요

## ✅ 병렬성에 대해 설명해주세요.

- parralelism
- 실제로 동시에 여러 작업 처리
- multi processor
- CPU multi-thread

## Concurrency problem 🆚 Race condition

- Concurrency problem: 동시에 여러 작업이 번갈아 처리되다보니 공유 자원이 의도치않게 변경
- Race condition: 프로세스가 자원을 동시에 처리하려고 경쟁하다보니 자원이 의도치않게 변경

## ✅ 프로세스 동기화에 대해 설명해 주세요.

- 여러 프로세스가 같은 자원에 동시에 접근하더라도 결과가 일정하도록 보장
- `consistent` 하도록
- `race condition`방지
- 프로세스가 순서 지켜서 작업하도록
- 예를 들어 `lock`을 걸기(`mutex`, `semaphore`)

## ✅ Critical Section에 대해 설명해주세요.

- 공유 자원에 접근하는 코드
- 공유 자원에 접근한다 🟰 `Critical Section`에 진입한다
- 이 코드에 진입하기 전`lock`을 걸고, 나오면서 `unlock`하는 방식으로 동기화 가능

## ✅ Race Condition이 무엇인가요?

- 여러 프로세스가 동시에 공유 자원에 접근하는 상태
- 동시에 자원을 쓰려고 하다 보니 공유 데이터가 예상치 못하게 처리되는 문제가 있음
- 만약 공유 자원에 동시에 접근한다면 프로세스 수행 순서에 따라 결과가 달라질 수 있다.
- `synchronization`필요

## ✅ Race condition이 발생하는 이유

- 자원에 대한 `read`, `write`, `save` 과정이 `atomic`하게 실행되지 않아서

## ✅ Race condition은 언제 발생하나요?

- `kernel mode`에서 수행 중에 `interrupt` ➡️ `ISR`
- `kernel mode`에서 수행 중에 `system call`, 그래서 `context switching`발생
- multi processor 환경

## ✅ Race Condition을 어떻게 해결할 수 있나요?

- mutual exclusion
- `lock`을 걸기
- 프로세스 간 작업 순서를 정하기

## ✅ Mutual Exclusion에 대해 설명해주세요.

- 단 하나의 프로세스만 `CS`, 즉 `공유자원`에 접근할 수 있다.
- 어떤 프로세스가 자원에 접근하고 있으면 다른 프로세스들은 기다려야 한다.

## ✅ Process Synchronization 문제를 풀기 위한 조건 3가지는?

- mutual exclusion
- progress: `CS`가 비어있고 `CS`에 들어가고자 하는 프로세스가 있으면 들어가게 해 줘야 한다.
- bounded waiting: 프로세스가 `CS`에 들어가기 위해 기다리는 횟수가 제한되어야 한다.
- 동일 속도 가정

## ✅ Mutual Exclusion을 할 수 있는 방법은?

- SW: `Peterson's Algorithm`
- HW: `TAS`
- OS: `semaphore`, `mutex`, `block/wakeup`
- language-level: `monitor`

## ✅ Busy waiting(spin lock)이란?

- 프로세스가 `CS`에 들어가지 못하는 상황에서도
- `while`문을 돌며 계속 들어갈 수 있는지 체크하며 기다리는 것
- 👎🏻 CPU, memory를 계속 쓰면서 기다린다

## ✅ `Peterson's Algorithm`에 대해 설명해주세요.

- `turn`: 프로세스 순서 번호
- `boolean flag`: `CS`에 들어가고자 하는 의사 표현
- `boolean flag` 들어 의사 표현하고,
- 만약 `flag` 들고있는 프로세스가 2개 이상이라면 `turn`을 확인하여 순서 정하기

- 👎🏻 busy waiting(spin lock)

## ✅ `TAS` 에 대해 설명해주세요.

- `Test And Set`이라는 함수
- `read, lock, write`과정을 `atomic`하게 실행

## ✅ 뮤텍스(Mutex)에 대해 설명해주세요.

- 공유 자원을 `lock`, `unlock`하는 방식으로 자원에 대한 접근 제한
- 공유 자원을 쓰기 전에 `lock`
- `CS`에서 나오면서 `unlock`해서 다른 자원이 사용할 수 있도록

## ✅ 세마포어에 대해 설명해주세요.

- `synchronization`을 제공하는 추상 자료형
- `semaphore variable`: 자원 개수
- 자원의 개수를 세고 남은 개수만큼 프로세스에게 할당
- `P`(자원 할당, `S--`), `V`(자원 반납, `S++`)연산을 atomic하게 실행
- 👎🏻 spinlock문제는 해결 못함
- 👎🏻 프로그래머가 `P`, `V`연산을 실수하면 모든 자원에 대해 `deadlock`
- 💊 고수준 동기화 기능을 제공하는 monitor

## ✅ 자원의 개수를 세는 걸 굳이 세마포어 변수로 하는 이유는?

- `P`연산과 `V`연산이 atomic하게 실행된다고 가정하기 때문

## 뮤텍스(Mutex) 🆚 이진 세마포어의 차이에 대해 설명해주세요.

- 뮤텍스는 공유 자원에 `lock`을 건 프로세스만 `unlock`할 수 있고
- 이진 세마포어는 `lock`, `unlock`하는 프로세스가 다를 수 있음

## ✅ 세마포어의 종류

- counting semaphore
- binary semaphore

## ✅ `block/wakeup`에 대해 설명해주세요.

- 세마포어 ➕ Busy waiting(spin lock) 문제 해결
- 세마포어를 일종의 `list`처럼 만들고
- 프로세스는 `CS`에 들어갈 수 있는지 확인
- 못 들어간다고 판단되면 `block` 되어 `queue`에서 기다리다가
- 여유 자원이 생겨 들어갈 수 있게 되면 `wakeup`
- 👍🏻 자원 기다릴 때 CPU, memory 소모 ❌

## Busy wait 🆚 Block/wakeup

- 일반적으로 `block/wakeup`이 효율적
- 만약 `CS`에 대한 경쟁이 많이 없다면 `Busy wait`해도 됨

## ✅ 모니터에 대해 설명해주세요.

- `synchronization`을 더 쉽게 구현하고자,
- `language level`에서 synchronization을 제공
- 모니터 내부에` 공유 자원`, `공유 자원 접근 procedure`이 있고
- 모니터 내부에는 단 하나만의 프로세스만 존재 가능
- 모니터 진입 가능 여부에 따라 `큐`에 프로세스 대기시키고, 깨우기

<br>

- 모니터가 공유 자원 접근을 관리, 책임
- 👍🏻 프로그래머가 `lock`, `P, V연산` 등 신경쓸 필요가 없음, 간편하게 `synchronization` 문제 해결!

## ✅ 동기화의 고전적인 문제

- Bounded Buffer Problem(Consumer, Producer problem)
- Readers and writers Problem
- Dining Philosophers Problem

## ✅ 데드락이 무엇인가요?

- 프로세스가 자신이 가진 자원은 내놓지 않으면서 다른 자원을 요청할 때
- 다른 프로세스는 내 프로세스가 가진 자원을 요청하면서
- 프로세스 실행이 block

## ✅ Deadlock example

- 자원1, 자원2를 가져야 수행 가능한 프로세스1, 프로세스2
- 프로세스 1은 자원1을 가지고, 프로세스2는 자원2를 가지고
- 서로가 자원을 반납할 때를 기다리는데
- 수행 완료 전에는 자기 자원을 절대 내놓지 않음

- 💊 자원 얻는 순서 정하기
- 💊 둘 다 가질 수 있는 상황에서만 가지기

## ✅ 데드락에서 말하는 자원이란?

- 하드웨어, 소프트웨어 자원 등 포함

## ✅ 프로세스가 자원을 얻고 사용하는 절차

- Request
- Allocate
- Use
- Release

## ✅ Deadlock이 생기는 이유?

- 공유 자원에는 한 번에 한 개의 프로세스만 접근 가능하고
- 프로세스는 자신의 자원을 내놓지 않으며
- 프로세스의 자원을 강제로 빼았을 수 없기 떄문

## ✅ 데드락 발생 조건 4가지를 설명해 주세요.

- mutual exclusion: 한번에 한 프로세스만 자원 접근 가능
- hold and wait: 할당된 자원을 가진 상태에서 다른 자원 요청
- non-preemption: 프로세스에게 할당된 자원은 뺴앗을 수 없음
- circular wait: 점유와 대기하는 프로세스가 순환 형태를 이룬다

## ✅ Resource allocation graph란?

- 자원 할당을 그래프로 표현
- 자원 당 인스턴스 1개 ➡️ cycle 있으면 `deadlock`
- 자원 당 인스턴스 여러개 ➡️ `deadlock`일 수도 있음

## ✅ 데드락을 막는 방법에 대해 설명해주세요.

- deadlock prevention: 4가지 조건 중 하나라도 불만족
- deadlock avoidance: `deadlock`이 생기지 않는 상황에서만 자원 할당

## ✅ deadlock prevention 방법에 대해 설명해주세요

- 앞선 데드락 발생 조건 4가지 중 한개라도 위배
- mutual exclusion: 위배 불가
- hold and wait: 실행 불가하면 반납하기 💊 시작할 때 모든 자원 할당 💊 추가요청할 떄는 가진 자원 내려놓고 다시 요청
- non-preemption: 실행 불가하면 빼앗기기 👎🏻 모든 자원을 preempt할 수는 없음
- circular wait: 자원 할당 순서 정하기

## ✅ deadlock avoidance 방법에 대해 설명해주세요

- 프로세스의 미래 최대 자원 사용량을 미리 알고 `deadlock`이 생기지 않는다고 판단될 때만 자원 할당
- `safe state`에 있을 때만 할당, `safe sequence`가 있는 상태
- `safe sequence`: 현재 가용자원 ➕ 미래 반납될 자원으로 프로세스 모두 처리 가능한가?

- 자원 당 인스턴스 1개: `Resource allocation graph`의 점선도 포함해서 `safe`한지 판단 후 할당
- 자원 당 인스턴스 여러개: `Bankers algorithm`사용해서 `safe`한지 판단 후 할당

## ✅ deadlock detection and recovery 방법에 대해 설명해주세요.

- `deadlock` 발생 허용, 감지 후 회복
- `Resource allocation graph` 또는 `banker's algorithm`을 사용해 `deadlock`을 `detect`하고
- `terminate`, `preemption`을 통해 `deadlock recovery`
- 👎🏻 starvation 발생 가능

## ✅ `Bankers algorithm`이란?

- allocation: 현재 프로세스에게 할당된 자원
- max: 최대 자원 사용량
- available: 현재 가용 자원
- need: 각 프로세스가 미래에 추가 요청할 수 있는 자원량

- `deadlock avoidance`에서는 `available > need` 일 때만 자원 할당

## ✅ deadlock ignorance 방법에 대해 설명해주세요.

- `deadlock` 방치
- 대부분 OS가 채택하는 방식
- 사람이 프로세스를 멈추는 등 사람이 해결하도록 한다.

## ✅

## ✅

## ✅

## ✅
