---
title: KOCW_Race Condition/ Process Synchronization
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ Race Condition

- 여러 프로세스들이 동시에 공유 데이터를 접근하는 상황에서
- 데이터 최종 연산 결과가 마지막에 그 데이터를 쓴 프로세스에 따라 달라지는 문제

- 💊 to prevent `race condition`, `concurrent processes` needs to be `synchronized`

## ✅ Race Condition이 언제 발생하는가

- 분명 프로세스 간에는 `memory address space`를 공유하지 않는다고 했는데
- 왜 `Race Condition`이 발생하나요?

#### 1️⃣ **kernel 수행 중 인터럽트 발생 시**

> interrupt 🆚 kernel mode

- `프로세스 A`가 커널모드 실행중이었는데 인터럽트가 발생해 `인터럽트 처리루틴`이 실행됨
- 그러면 `프로세스 A`, `인터럽트 처리루틴` 모두 커널 코드이므로 `kernel address space`공유

<img width="425" alt="Screenshot 2025-01-14 at 00 36 01" src="https://github.com/user-attachments/assets/ab3c8b6b-f006-4463-bc1f-7fb99fc99c76" />

- 💊 프로세스가 `kernel mode`에서 실행중일 때는 인터럽트를 `disable`시키고
- `kernel mode` 끝나면 인터럽트 `enable`시킨다.

#### 2️⃣ **context switch가 일어나는 경우**

> preempt a process running in kernel

- 커널 내부 데이터를 접근하는 루틴들 간에 발생
- `프로세스 A`, `프로세스 B`의 각 `memory address space` 간 `data sharing`이 없음!
- 그러나 `system call`을 하는 동안에 `kernel address space`의 `data`를 `access/share`하게 됨
- 이 작업 중간에 CPU를 `preement`!!!
- 예를 들어 `timer`
- 그러면 `race condition` 발생
- 커널의 데이터를 건드리던 도중에 프로세스가 바뀌어 다른 루틴 실행

  <img width="423" alt="Screenshot 2025-01-14 at 00 31 14" src="https://github.com/user-attachments/assets/c5e8af0d-168b-41e2-a011-707553a64d35" />

- 💊 프로세스가 `kernel mode`에서 실행중일 때는 CPU를 `preement`하지 않는다.
- `kernel mode`에서 `user mode`로 돌아갈 때 `preement`한다.
- `preement disable/enable`

#### 3️⃣ `Multi processor system`, CPU가 여러개 있는 상황

- `shared memory`내의 `OS kernel data`
- 공유 메모리를 사용하는 프로세스들
- `memory address space`를 공유하는 `CPU process`가 여럿 있는 경우 `race condition`의 가능성이 있다.
- 여러개 CPU 프로세스가 동시에 `OS kernel data`에 접근한다
- `Multi processor system`의 경우 `interrupt disable/enable`로 해결되지 않음

- 💊 방법 1: 한번에 하나의 CPU만이 `kernel`에 들어갈 수 있게 허용
  - 운영체제 **전체에** `lock`을 걸어서 하나의 CPU만 독점해서 쓰기
  - 👎🏻 여러개 CPU 중 하나만 `kernel mode`에 들어갈 수 있게 하면 나머지 CPU는 기다리느라 오버헤드가 크다
- 💊 방법 2: 커널 내부에 있는 각 공유 데이터에 접근할 때마다 그 데이터에 대해 `lock/unlock`
  - 운영체제 `kernel`의 **각 데이터마다** `lock`을 걸어서 사용
  - 👍🏻 그 데이터를 건드리지만 않는다면 다른 CPU가 `kernel`쓰고 있어도 나도 사용 가능

## ✅ Process Synchronization

- 공유 데이터`shared data`의 동시 접근`concurrent access`은 데이터 불일치 문제`inconsistency`를 발생시킬 수 있음
- `consistency`유지를 위해 협력 프로세스`cooperating process`간의 실행 순서 `orderly execution`을 정해주는 메커니즘 필요

## ✅

## ✅

## ✅

## ✅

## ✅

CPU
