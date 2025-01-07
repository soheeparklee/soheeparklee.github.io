---
title: KOCW_Scheduling
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ Scheduler

> CPU또는 memory를 어떤 프로그램에게 어떻게 할당할지 결정 <br>
> 운영체제 안에 있는 `code`중 일부 <br>

#### ☑️ Long-term scheduler: job scheduler

> **memory**

- 시작 프로세스 중 어떤 것들을 `ready queue`로 보낼지 결정
- 즉, 디스크 내 작업을 어떤 순서로 **메모리**에 가져올지 결정
- ⭐️ 프로세스에 `memory, 각종 자원`을 할당하는 문제

- `degree of Multiprogramming`을 제어
  - `degree of Multiprogramming`: 메모리에 올라간 프로그램이 몇 개냐
  - 메모리는 한정되어 있기 때문에 프로그램이 너무 많이 올라가도, 너무 적게 올라가도 비효율적
  - 이를 관리해주는 것이 바로 `long-term scheduler`
- 프로세스가 생성되고 `admitted`, 즉 `메모리에 올라오게 해 주는`과정

- time sharing system에는 보통 장기 스케쥴러가 없다.
- 장기 스케쥴러는 과거 메모리가 작던 시절에 사용했음
- 프로세스는 무조건 `ready`상태가 된다.
- 즉, 최근 OS는 프로세스가 생성되면 무조건 메모리에 올라오게 된다.
- 최근 OS는 `장기 스케쥴러`가 없는 대신❌ `중기 스케쥴러 Swapper`를 둔다⭕️

#### ☑️ Medium-term scheduler: Swapper

> **memory** 뺏기

- 최근 OS는 프로그램이 실행되면 무조건 메모리로 올라옴, 상태 `ready`
- 하지만 메모리는 한정적이기 때문에 다 올라올 수는 없음!
- 따라서 여유 공간 마련을 위해 프로세스를 통째로 메모리에서 **디스크로 쫒아냄**
- 프로세스에서 **메모리를 뺏는** 문제
- 우선은 메모리에 모든 프로세스를 올리고, `Swapper`가 메모리에 적재된 프로그램 수를 관리
- `degree of Multiprogramming`을 제어

- `swap in`: 메모리에 다시 들어옴
- `swap out`: 메모리에서 쫒겨남

- `Swapper`때문에 프로세스 상태 `suspended`가 생겼다.
- 프로세스 상태 `suspended`: 프로세스가 수행이 정지된 상태
  - 운영체제 swapper때문에 메모리에서 쫒겨나서 정지
  - 또는 사용자가 프로세스를 잠시 정지시킴

#### ☑️ Short-term scheduler: CPU scheduler

> **CPU**

- 어떤 프로세스를 다음번에 `running`시킬지 결정
- 프로세스에세 **CPU**를 주는 문제
- 자주 호출된다.
- 따라서 충분히 빨라야 한다. (ms 단위)
- `Short-term scheduler`가 프로세스를 선정하면, `dispatcher`이 `CPU`를 해당 프로세스에게 할당한다.
