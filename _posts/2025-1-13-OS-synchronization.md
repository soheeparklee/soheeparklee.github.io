---
title: KOCW_Race Condition/ Process Synchronization
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ 데이터의 접근

- 읽고
- count 연산
- 저장
- 이 과정은 `atomic`하게 실행될 수가 없다
- 이 도중에 `Race Condition`발생 가능

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

> preempt a process running in kernel <br>

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

## ✅ Critical Section Problem

- `n`개의 프로세스가 공유 데이터를 동시에 사용하기 원하는 경우
- 각 프로세스의 `code segment`에는 공유 데이터에 **접근하는 코드** `critical section`이 존재

<img width="378" alt="Screenshot 2025-01-14 at 00 55 11" src="https://github.com/user-attachments/assets/f5154ac1-02b4-47e8-bc86-d929fcb61656" />

- 💊 하나의 프로세스가 `critical section`에 있을 때 다른 모든 프로세스는 `critical section`에 **들어갈 수 없어야** 한다.
- 💊 예를 들어 `critical section`에 들어가기 전에 `lock`을 걸고, 나올 때는 `lock`을 풀기

<img width="127" alt="Screenshot 2025-01-14 at 11 43 43" src="https://github.com/user-attachments/assets/9d883220-564c-4fbf-81e3-9164afe92c0c" />

## ✅ 프로그램적 해결법의 충족 조건 3

- ✔️ **Mutual Exclusion**
- 프로세스가 동시에 `critical section`에 들어가면 안 된다.
- 하나의 프로세스가 `critical section`를 실행중이면
- 다른 모든 프로세스들은 `critical section`에 들어가면 안 된다.

- ✔️ **Progress**
- 아무로 `critical section`에 들어가 있지 않은 상태에서
- `critical section`에 들어가고자 하는 프로세스가 있으면
- `critical section`에 들어가게 해 주어야 한다.

- ✔️ **Bounded Waiting**
- 프로세스가 `critical section`에 들어가려고 기다리는 시간이 *유한*해야 한다.
- 특정 프로세스만 `critical section`에 영원히 못 들어가는 문제가 생기면 안 된다.
- 프로세스가 `critical section`에 들어가려고 요청한 순간부터 그 요청이 허용될 떄가지 다른 프로세스들이 `critical section`에 들어가는 횟수가 *제한*되어야 한다.

- ✔️ 가정
  - 모든 프로세스의 수행 속도는 0보다 크다
  - 프로세스 간의 상대적인 수행 속도는 가정하지 않는다

## 💡 Algorithm 1

- 내 차례인지 확인하고 `turn 변수`
- 내 차례가 아니면 기다리고
- 내 차례면 `critical section` 실행
- 나올 때 상대방 차례로 바꿔주기

```C
int turn;
turn = 0 ;

do{
  while(turn !=0 ); //my turn? 내 차례인가?
  critical section
  turn = 1; //now it is your turn 상대방 차례로 바꿔주기
  remainder section
} while(1);
```

- 👍🏻 둘 이상의 프로세스가 `critical section`에 들어가는 일은 없다
- 👎🏻 **과잉양보**: 특정 프로세스가 `critical section`에 더 자주 들어가야 한다면 문제 발생

  - 왜냐하면 반드시 한번씩 교대로 들어가야만 하기 때문 `swap turn`
  - 상대가 `turn 변수`를 내 값으로 바꿔줘야만 내가 들어갈 수 있음
  - 특정 프로세스가 `critical section`에 더 빈번하게 들어가야 한다면?
  - 또는 상대방이 `critical section`에 안들어가면, 영원히 내 차례는 안 온다.

- 💡 따라서 이 알고리즘은 `Progress`를 만족하지 못했음 ❌

- `Mutual exclusion` ⭕️
- `Progress` ❌

## 💡 Algorithm 2

- 프로세스가 `critical section`에 들어가고 싶으면 깃발 `boolean flag`를 든다.
- initially `flag[모두] = false;` 아무도 `CS`에 없음
- 프로세스가 `CS` 들어가고 싶으면 `flag[i]==true`

```C
boolean flag[2];

do{
  flag[i]==true; //나 CS들어갈래 깃발 들기, 의사표현
  while (flag[i]); //너도 들어가고 싶니? 그럼 나 기다릴게
  critical section
  flag[i] = false; //나 이제 나왔으니 깃발 내림
  remainder section
} while(1);
```

- `Mutual exclusion` ⭕️
- `Progress` ❌
- 👎🏻 두 개 프로세스가 2행까지 수행 후 끊임없이 양보하는 상황 발생
- 2행에서 프로세스가 `CS`는 들어간게 아니라 의사표현만 한건데, 들어간 것으로 생각하고 눈치만 보다가 아무도 `CS`에 못 들어감

## 💡 Peterson's Algorithm

- 깃발을 사용해 `CS`에 들어가고자 하는 의사표현
- 상대 프로세스가 `CS`에 들어갔는지 확인
- 동시에 두 프로세스가 깃발을 들면, 깃발을 든 것에 한해서 `turn`을 확인해 번갈아 들어감

```C
do{
  flag[i]==true; //나 CS들어가고 싶다고 깃발 들기
  turn = j; //상대 프로세스 차례로 바꾼다
  while (flag[i] && turn == j ); //내 차례 아니면 기다리기
  critical section
  flag[i] = false; //나 이제 나왔으니 깃발 내림
  remainder section
} while(1);
```

- `Mutual exclusion` ⭕️
- `Progress` ⭕️
- `Bounded waiting` ⭕️

## ✅

## ✅

## ✅

## ✅
