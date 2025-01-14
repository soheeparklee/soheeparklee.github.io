---
title: Interview_CPU scheduling
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

### ✅ 기아 상태가 무엇인가요?

- starvation
- 우선순위가 낮은 프로세스가 계속 CPU를 얻지 못하는 상태

### ✅ 기아 상태를 어떻게 해결할 수 있나요?

- aging
- priority feedback queue

### ✅ CPU 스케줄링에 대해 설명해주세요.

- `ready`상태의 프로세스 중 어떤 프로세스가 CPU제어권을 얻을지 결정

### ✅ CPU scheduling이 왜 필요한가요?

- `CPU burst time`이 긴 `CPU bound job`과
- `CPU burst time`이 짧은 `I/O bound job`이 균일하지 않게 섞여있어서

### ✅ 스케쥴링 종류는 무엇이 있나요?

- `preemptive`: 자발적으로 CPU반납하기 전까지는 빼앗지 않음
- `non-preemptive`: 우선순위 더 높은 프로세스 있으면 빼앗음

### ✅ 스케쥴링이 필요한 경우는 어떤 경우인가요?

- 프로세스가 CPU쓰다가 `system call`로 `block` ➡️ `non-preemptive`
- 프로세스가 CPU쓰다가 `timer` ➡️ `preemptive`
- 프로세스가 CPU쓰다가 `interrupt`로 `ready` ➡️ `preemptive`
- 프로세스 terminate `non-preemptive`

### ✅ 스케쥴러 성능 평가 척도는?

- CPU utilization ⬆️
- throughput ⬆️
- turnaround time ⬇️
- waiting time ⬇️
- response time ⬇️

### ✅ `Response time` 🆚 `Waiting time` 🆚 `Turnaround time`

- `Response time`: 처음으로 CPU얻을 때까지 걸린 시간
- `Waiting time`: CPU사용하려고 기다린 시간 총 합
- `Turnaround time`: 프로세스가 수행을 마칠 때까지 걸린 시간 (`Waiting time` ➕ `CPU burst time`)

### ✅ 스케줄러의 종류는 무엇이 있나요?

- 장기: memory scheduling, 어떤 프로그램이 메모리에 올라가 프로세스가 될지 결정, `degree of programming`
- 중기: memory scheduling, 일단 모든 프로그램은 메모리에 올리고, 메모리가 차면 쫒아내기, `degree of programming`
- 단기: CPU scheduling

### ✅ 선점형 `Preemptive` 스케줄링과 비전형 `Non-Preemptive` 스케줄링의 차이가 무엇인가요?

- `preemptive`: 자발적으로 CPU반납하기 전까지는 빼앗지 않음
- `non-preemptive`: 우선순위 더 높은 프로세스 있으면 빼앗음

### ✅ 선입선출 스케줄링(FCFS)에 대해 설명해주세요.

- 먼저 오는 프로세스가 먼저 실행
- `non-preemptive`
- 👍🏻 똑같은 길이의 프로세스가 오면 `context switching`이 적은 `FCFS`가 제일 효율적이라
- 👍🏻 `MLQ background queue`에서는 자주 쓰임
- 👎🏻 `convoy eefect`: 짧은 `CPU burst time`의 프로세스도 오래 기다려야 하는 비효율성
- 👎🏻 `I/O장치`들의 이용률도 동반 하락

### ✅ 최단 작업 우선 스케줄링(SJF)에 대해 설명해주세요.

- 가장 짧은 `CPU burst time`을 가진 프로세스 부터 실행
- `Non-preemptive`: 프로세스가 실행 중일 때는 더 짧은 프로세스가 와도 수행 보장
- 👍🏻 `minimum average waiting time` 보장
- 👎🏻 `CPU burst time`긴 작업에게는 불리
- 👎🏻 starvation

### ✅ 최소 잔류 시간 우선 스케줄링(SRTF) 방식에 대해 설명해주세요.

- `SJF Preemptive`: 더 짧은 프로세스 오면 CPU실행하다가 뺏김
- 👍🏻 `minimum average waiting time` 보장
- 👎🏻 starvation

### ✅ `CPU burst time`을 어떻게 알 수 있는가?

- 프로세스 과거 `CPU burst time`을 바탕으로 예측
- 최근 `CPU burst time`은 많이 반영, 예전 `CPU burst time`는 적게 반영

### ✅ 우선순위 스케줄링에 대해 설명해주세요.

- 프로세스마다 우선순위가 있음
- SJF, SRTF, RR, MLQ, MFQ
- 👎🏻 starvation 우선순위가 낮으면 CPU를 영원히 얻지 못함
- 💊 aging

### ✅ 라운드 로빈 스케줄링에대해 설명해주세요.

- 각 프로세스는 동일한 CPU할당 시간 `time quantum`을 가짐
- `time quantum`이 지나면 `timer`이 CPU 뺏음, `preemptive`한 방법
- 👍🏻 `Response time` 짧음, `interactive`한 시스템에서 좋다
- 👍🏻 `waiting time`이 `CPU burst time`에 비례
- 👎🏻 만약 프로세스의 `CPU burst time`이 모두 동일하다면, `context switching overhead`만 커지는 역효과

### ✅ `time quantum`은 어떻게 정할까?

- `time quantum`이 너무 길면 `FCFS`
- `time quantum`이 너무 짧으면 `context switching overhead`커짐
- 따라서 `I/O bound job`은 한번에 실행될 수 있지만, `CPU bound job`은 여러번에 걸쳐 실행될 수 있는 정도

### ✅ 멀티 레벨 큐 스케줄링에 대해 설명해주세요.

- 여러개의 큐가 있고 큐마다 우선순위가 다름
- 큐에 대한 스케쥴링 필요: 프로세스가 어떤 큐에 줄을 설 것인가? 어떤 큐가 우선순위 가질 것인가? 큐마다 스케쥴링 기법 다름
- 프로세스는 큐를 바꿀 수 없음
- 👎🏻 우선순위 낮은 큐에 있는 프로세스는 오래 기다려야 함

- 큐의 종류

  - foreground RR: interactive I/O job
  - background FCFS: CPU bound job

- 큐에 대한 스케쥴링

  - fixed priority: 👎🏻 starvation
  - timeslice

### ✅ 멀티 레벨 피드백 큐 스케줄링에 대해 설명해주세요.

- 멀티 레벨 큐 ➕ 큐를 바꿀 수 있음

- 먼저 가장 우선순위 높은 RR 큐에 줄을 서고,
- 주어진 `time quantum`내에 일을 마치지 못하면
- `CPU burst time`이 길다고 판단, 다음 우선순위 큐로 넘어감
- 우선순위 낮은 큐는 `FCFS`로 구현하여 `context switching overhead`줄일 수 있음

- 👍🏻 RR보다 발전된 형태로, 짧은 프로세스일수록 더 빨리 서비스, 긴 프로세스는 `context switching`없이 구현
- 👍🏻 aging을 이렇게 구현 가능

### ✅ Multilevel queue 에서 `background`큐는: `FCFS`쓰는 이유?

- 어짜피 `CPU burst time`이 긴 프로세스 이니까
- `context switching overhead`줄이기

### ✅ Multi processor Scheduling은 어떻게 구현?

- homogeneous:

  - 한 줄에 서서 프로세스가 꺼내감
  - 👎🏻 특정 CPU에서 실행되어야 하는 프로세스는?

- load sharing:

  - CPU마다 줄을 각각 선다
  - 👎🏻 CPU별 부하가 적절히 분산되도록 해야 함

- symmetric:
  - 각 CPU가 알아서 스케쥴링 결정
- asymmetric:
  - 하나의 CPU가 다른 CPU의 스케쥴링, 데이터 접근 조절

### ✅ Real time scheduling

- hard real time systems
- soft real time computing

### ✅ Thread Scheduling

- local scheduling: thread library
- globals scheduling: kernel

### ✅ How to evaluate algorithms?

- queueing models
- implementation & measurement
- simulation
