---
title: KOCW_CPU Scheduling
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ CPU burst and I/O burst

<img width="265" alt="Screenshot 2025-01-06 at 13 02 18" src="https://github.com/user-attachments/assets/745b99f3-b686-4eda-aba5-0e325cd3e0ea" />

- 사용자 프로그램이 수행되는 과정은 `CPU burst`와`I/O burst`이 **번갈아 반복**되는 것으로 구성된다.
- `CPU burst`: CPU에서 기계어 실행 (비교적 빠름)
- `I/O burst`: I/O 작업을 하는 단계 (비교적 느림)

## ✅ CPU burst time

> CPU를 한번에 얼마나 오래 쓰느냐

- ✔️ **CPU bound job**:
- CPU를 길~게 쓰는 작업 `과학/수학 연산`
- _few long CPU burts_

- ✔️ **I/O bound job**:
- CPU를 짧게짧게 쓰는 작업
- _many short CPU bursts_
- `interactive job`, `사람 유저와 통신을 자주 하는 작업, 키보드로 입력하면 출력하고...`
  <br>

- ❓ 우리가 사용하는 프로세스는 어떤 프로세스들일까?
- 우리가 사용하는 프로세스들은 `CPU bound job`과 `I/O bound job`이 **균일하지 않게** 섞여였다.
- 따라서 `time sharing`을 통해 해결하는 등 `CPU scheduling`이 반드시 필요하다.

- ❓ 그러면 `CPU bound job`과 `I/O bound job`중 누구에게 CPU를 먼저, 얼마나 줘야 할까?
- `CPU burts`가 짧은 `I/O bound job`에게 우선적으로 CPU를 할당해줘서 응갑시간을 높이고, `I/O`장치의 효율성을 높일 수 있다.
- 이런식으로 여러 종류의 `job(process)`가 섞여 있기 때문에 `CPU scheduling`이 필요하다.

## ✅ CPU Scheduling

> 누가 먼저 CPU를 쓸 것인가? <br>

#### 📌 `CPU Scheduler`:

- OS내부 **소프트웨어**로, `ready`상태의 프로세스 중 이번에 CPU를 줄 프로세스를 **고르는 운영체제 코드**
- *결정*하는 역할

## ✅ Dispatcher

- `CPU Scheduler`가 새롭게 선정한 프로세스가 CPU를 할당받고 작업을 수행할 수 있도록 **환경설정을 하는 운영체제 코드**
- `CPU Scheduler`가 프로세스를 고르면, CPU제어권을 넘긴다.
- *실행*하는 역할

#### 📌 `context switching`: `Dispatcher`이 CPU제어권을 넘기는 과정

- 새롭게 선정된 프로세스의 `context`를 `PCB`로부터 복원하고, 그 프로세스에게 CPU제어권을 넘긴다

```
1. Dispatcher는 실행중이던 프로세스 context를 PCB에 저장
2. 새롭게 선택된 프로세스 context를 PCB에서 불러옴
3. 새롭게 선택된 프로세스에게 CPU제어권 넘김
```

#### 📌 `dispatch 지연 시간`:

- 하나의 프로세스를 정지시키고, 다음 프로세스에게 CPU제어권을 넘기는데 걸리는 시간
- `dispatch 지연 시간`의 대부분은 `context switching overhead`에 해당

#### ☑️ CPU scheduling이 필요한 이유

- CPU를 기다리는 작업에는 `CPU bound job`과 `I/O bound job`이 **섞여 있다.**
- `I/O bound job`은 CPU를 짧게 쓰니까 `I/O bound job`에게만 CPU를 주면, `CPU bound job`는 실행을 못한다.
- 그렇다고 `CPU bound job`에게만 CPU를 주면, 유저와 자주 interact 하는 `I/O bound job`은 유저를 기다리게, 답답하게 한다.
- 따라서 두 종류의 작업을 골고루 효율적으로 사용하게 하기 위해 `운영체제`가 `CPU scheduling`를 해야 한다.

## ✅ CPU Scheduling 종류

- `nonpreemptive`: 프로세스가 CPU를 자발적으로 반납하기 전까지는 빼앗지 않음 ❌
- `preemptive`: CPU를 강제로 빼앗아서 ⭕️ 다른 프로세스에게 넘김

## ☑️ CPU scheduling이 필요한 경우

> CPU scheduling이 필요한 경우 프로세스 상태 변화

> 즉 CPU를 다른 프로세스에게 주려고 하는 경우

- 1️⃣ `running` ➡️ `blocked` : CPU쓰다가 I/O 같이 오래걸리는 작업 요청하는 `system call`, **non-preemptive**
- 2️⃣ `running` ➡️ `ready` : CPU할당 시간이 만료되어 `timer`, **preemptive**
- 3️⃣ `blocked` ➡️ `ready` : I/O 완료 후 인터럽트한 프로세스가 현재 수행중인 프로세스보다 우선순위가 높아서, **preemptive**
- 4️⃣ `terminated` : **non-preemptive**

- 1, 4번은 `nonpreemptive, 강제로 빼앗지 않고 자진 반납`
- all other scheduling is `preemptive`

## ✅ Scheduling criteria, 성능평가

> Scheduling performance index/measure <br>
> 다양한 Scheduling방법이 있을텐데, 그 방법들을 판단하는 기준 <br>

- ✔️ `CPU utilization` **이용률** ⬆️:

  - 전체 시간 중 CPU가 놀지 않고 일한 비율
  - keep CPU as busy as possible
  - CPU를 더 많이 써서 비율이 높을 수록 좋음

- ✔️ `Throughput` **처리량** ⬆️:

  - 단위시간 당 처리량
  - 시간 당 프로세스를 몇 개 처리했는가?
  - 주어진 시간 동안 `ready queue`에서 기다리고 있는 프로세스 중 몇 개를 처리했는가
  - number of processes that complete their execution per time unit
  - 프로세스를 더 많이 처리할수록 좋음

- ✔️ `Turnaround time` **소요시간, 반환 시간** ⬇️:

  - amount of time to execute a particuliar process
  - CPU에서 실행한 시간 ➕ CPU를 기다린 시간

- ✔️ `Waiting time` **대기 시간** ⬇️:

  - 대기 시간: amount of time a process has been waiting in the ready queue
  - 프로세스가 기다린 시간
  - CPU를 기다린 시간들의 총 합(여러번 CPU를 뺏기고 얻기까지 기다렸을 테니까)
  - 기다리는 시간은 짧을 수록 좋다

- ✔️ `Response time` **응답 시간** ⬇️:

  - amount of time it takes from when a request was submitted until the first response is produced, **not** output
  - CPU를 쓰러 큐에 들어와서 **처음으로** CPU를 얻을 때까지 걸린 시간

## 💡 FCFS

> First Come First Served <br>
> 먼저 온 프로그램이 CPU를 먼저 쓴다. <br>

- `non-preemtive`: CPU를 뺐지 않는다.

- 👎🏻 효율적이지 않다. 짧은 CPU시간을 가진 프로세스도 오래 기다려야 함. `convoy effect`

```
p1: burst time 24초
p2: burst time 3초
p3: burst time 3초

1️⃣ situation: p1 ➡️ p2 ➡️ p3
waiting time: p1: 0초/ p2: 24초/ p3: 27초
average waiting time: 17초

2️⃣ situation: 2. p2 ➡️ p3 ➡️ p1
waiting time: p1: 5초/ p2: 0초/ p3: 3초
average waiting time: 3초
```

- 👍🏻 `CPU bound job`같이 `CPU burst time`이 긴 프로세스들만 수행할 떄는, 괜히 `context switching`만 자주 일어나게 프로세스를 바꾸는 것보다 그냥 오는 순서대로 길게씩 수행하는게 나을 수도 있음.
- 그래서 `multi level queue`의 `background queue`에서는 `FCFS`를 쓸 수도 있다

- 👎🏻 `convoy effect`:
  - `CPU burst time`이 긴 프로세스가 먼저 오면, 짧은 프로세스도 많이 기다려야 함.
  - short process behind long process
  - 👎🏻 long process하나 때문에 뒤에 오는 short process가 다 기다려야 하는 현상
  - 👎🏻 `I/O`장치들의 이용률까지도 동반 하락

## 💡 SJF, SRTF

> Shortest Job First, Shortest Remaining Time First <br>
> SJF: nonpreemptive, SRTF: preemptive <br>
> CPU 사용시간 `burst time`이 가장 짧은 프로세스부터 CPU사용 <br>

- 각 프로세스의 다음번 `CPU burst time`을 가지고 스케쥴링
- `CPU burst time`이 긴 프로세스에게는 손해

#### ☑️ `non-preemtive` SJF

- 일단 CPU를 잡으면 이번 `CPU burst`가 완료될 때까지는 CPU를 선점(preemtive) 당하지 않음

```
p1: arrival time 0초 burst time 7초
p2: arrival time 2초 burst time 4초
p3: arrival time 4초 burst time 1초
p4: arrival time 5초 burst time 4초

SJF non-preemptive : p1 ➡️ p2 ➡️ p3 ➡️ p4
(p1이 burst time이 제일 길지만, 도착한 시점에는 제일 짧은 프로세스였기 때문에 제일 먼저 실행되고, burst time동안에는 더 짧은 프로세스가 와도 수행 시간을 보장해준다. )

average waiting time = (0+6+3+7)/4 = 4
```

#### ☑️ `preemtive` SRTF

- SJF를 `preemtive`방식으로 구현한 것
- 현재 수행중인 프로세스의 `남은 burst time`보다 더 짧은 `burst time`을 가진 새로운 프로세스가 오면 CPU를 빼앗김
- `preemtive SJF`를 `SRTF(Shortest Remaining Time First)`라고 부르기도 한다.

```
p1: arrival time 0초 burst time 7초
p2: arrival time 2초 burst time 4초
p3: arrival time 4초 burst time 1초
p4: arrival time 5초 burst time 4초

SJF preemptive : p1 ➡️ p2 ➡️ p3 ➡️ p2 ➡️ p4 ➡️ p1

average waiting time = (9+1+0+2)/4 = 3
- 👍🏻 CPU scheduling 방법 중 average waiting time이 제일 짧은 방법이다.
```

- 👍🏻 `minimum average waiting time`을 보장
- 👍🏻 `SJF` is optimal: SJF보다 `minimum average waiting time`이 짧을 수는 없다.
- 특히 `SJF` 중에서도 `SRTF`방식이 기다리는 시간이 제일 짧다

- 👎🏻 **Starvation** 기아현상 발생
  - low priority process can never be executed
  - 👎🏻 형평성
  - 오래 걸리는 `burst time`가 긴 프로그램은 CPU를 절대 못 쓴다.

<br>

- 👎🏻 프로세스의 `CPU burst time`을 모를 수 있다.
  - 모르는데 제일 짧은 프로세스를 어떻게 알고 먼저 CPU를 주냐?
  - 그 프로세스의 **과거**를 보고 `CPU burst time`을 대략적으로 예측

#### ☑️ SJF가 CPU burst time을 예측하는 방법

- 만약 `n+1`째의 `CPU burst time`을 예측하고 싶다면 `n`번의 `CPU burst`했을 때 시간을 가지고 구함
- expotential averaging(예측값)
- `n`번의 `CPU burst`했을 때 시간 반영, 처음 에측했던 값 반영
- 1보다 작은 값끼리 곱해서, 결국 더 오래된 `CPU burst`는 적게 반영, 직전의 `CPU burst`는 더 많이 반영해서 추정

<img width="416" alt="Screenshot 2025-01-06 at 23 01 23" src="https://github.com/user-attachments/assets/ebbb10b1-f4ba-4ee9-ac49-656e45be2751" />

## 💡 Priority Scheduling

> A priority number(integer) is associated with each process <br>
> smaller priority number, higher priority <br>

- highest priority를 가진 프로세스에게 CPU 할당
- smallest number = highest priority

- ✔️ `preemptive`: CPU줬는데 더 우선순위 높은 프로세스 오면 CPU뺐음
- ✔️ `non-preemptive`: 우선순위 높아서 CPU주고 기다림

- SJF도 일종의 Priority Scheduling
- SJF의 priority: predicted next CPU burst time

- 👎🏻 **Starvation**: low priority process may never execute
- 💊 **Aging**: as time progresses increase priority of process
  - 나이를 먹으면 좀 우대를 해 주자
  - 우선순위 낮은 프로세스도 언젠가는 수행될 수 있도록

## 💡 Round Robin

> 각 프로세스는 동일 크기의 CPU를 사용할 수 있는 시간`time quantum`이 할당됨 <br>
> 시간이 지나면 프로세스는 CPU를 빼앗김 ➡️ 인터럽트, preemptive <br>

- 각 프로세스는 CPU를 사용할 수 있는 동일한 크기의 할당 시간 `time quantum`을 가짐
- `time quantum`: 10~100 ms
- 할당 시간이 끝나면 인터럽트 발생
- `timer`이 붙어있음!
- 프로세스는 CPU를 뺏김
- 프로세스는 `preemptive` 당하고
- `CPU ready 큐`의 제일 뒤에 줄을 선다.

- `preemptive` 방법: `timer`을 가지고 있다.

```
n개의 프로세스가 ready 큐에 있고
할당 시간이 q time unit인 경우
각 프로세스는 최대 q time unit 단위로 CPU 시간의 1/n을 얻는다.
- 👍🏻 어떤 프로세스도 (n-1) * q time unit 이상 기다리지 않는다.
```

- 👍🏻 `대기시간`이 프로세스의 `CPU사용시간`에 비례한다.
- 따라서 `CPU burst time`이 긴 프로세스, 짧은 프로세스에게 모두 공평하다

  - 👍🏻 짧은 프로세스는 할당 시간 내에 일 끝냄
  - 👍🏻 짧은 프로세스는 기다리는 시간도 짧음
  - 👍🏻 오래 걸리는 프로세스도 조금조금씩 언젠가는 끝냄
  - 👍🏻 오래 걸리는 프로세스는 기다리는 시간도 길다

- 👍🏻 n개의 프로세스가 있을 때 어떤 프로세스도 `(n-1)*할당시간` 이상 기다리지 않음

- 👍🏻 `RR`은 `SJF`보다 `response time`이 짧다!
- 따라서 `interactive` 한 시스템에서 빨리빨리 응답할 수 있다.

- 👎🏻 `RR`은 `I/O bound job`, `CPU bound job`이 섞여 있을 떄만 의미가 있다.
- 예를 들어 모든 프로세스가 `10초`걸리는 일인데 `time quantum`이 `1초`라면, 그냥 `10초`씩 진행하면 될걸, 굳이 `1초`씩 끊어서 10번 진행하는 셈이 된다.
- 오히려 `오버헤드`만 커진다.
- 따라서 `RR`은 여러 종류의 프로세스가 섞여 있을 때 효율적이다.

#### ❓ 할당 시간 `time quantum`은 어떻게 정할까?

- `time quantum`이 너무 길면, `FCFS`랑 똑같게 된다.
- `time quantum`이 너무 짧으면, `context switching`의 `오버헤드`가 커진다
- 적당한 시간이란: `CPU burst time`이 짧은 `I/O작업`은 한번에 실행될 수 있지만, `CPU bound job`은 여러번에 걸쳐 실행될 수 있는 정도

## 💡 MLQ

> Multi Level Queue <br>
> CPU는 한 개인데 Ready Queue는 **여러개로** 분할 <br>
> 프로세스가 하나의 `queue`에 줄을 서면, `queue`를 바꿀 수 **없음** <br>

- ➡️ 여러개의 `queue`가 있으니 `queue`에 대한 `scheduling`이 필요하다.
  - 어떤 `queue`에 서 있는 프로세스를 우선적으로 스케쥴링 할 것인가?
  - 프로세스가 도착했을 때 어떤 `queue`에 세울 것인가?

#### ☑️ `queue`**의 종류**

- ✔️ `foreground`: interactive, 대화형 작업
- ✔️ `background`: batch-no human interaction, CPU를 길게 쓰는 작업, 계산 작업

- 프로세스가 하나의 `queue`에 줄을 서면, `queue`를 바꿀 수 없음
- 프로세스 A가 `foreground queue`에 서면 A는 평생 `foreground`

- 각 `queue`는 독립적인 `CPU scheduling`알고리즘을 가진다.
  - `foreground`: `RR`
  - `background`: `FCFS`, `response time`이 크게 중요하지 않기 때문이다, `context switching overhead`줄이기

#### ☑️ `queue`에 대한 `scheduling`

- ✔️ **Fixed priority scheduling**

  - 큐별로 `fixed priority` 부여
  - serve all from foreground then from background
  - foreground `queue`가 비어야만 background `queue` 실행
  - 우선순위가 낮은 `queue`는 우선순위가 높은 `queue`가 비어있을 때만 실행 가능
  - 👎🏻 starvation

- ✔️ **Time slice**

  - 각 `queue`에 `CPU time`을 적당한 비율로 할당
  - 예를 들어 `CPU time` 중 80%는`foreground`, 나머지 20%는 `background`
  - 👍🏻 기아현상 방지

## 💡 MFQ

> Multilevel Feedback Queue <br>
> 마찬가지로 여러 개의 `queue`를 가지지만, 프로세스가 `queue`를 바꿀 수 있음 <br>
> starvation 해결을 위한 **aging**을 이 방식으로 구현 가능

- `aging`을 이와 같은 방식으로 구현 가능
- 오래 기다린 프로세스는 우선순위가 높은 `queue`로 옮겨갈 수 있도록 한다.

- 오래 걸리는 프로세스는 더 오래 걸리게 구현하는 Multilevel Feedback Queue

```
1. RR queue quantum = 8초
2. RR queue quantum = 16초
3. FCFS

- 모든 프로세스는 처음에 우선순위가 가장 높은 [quantum = 8]큐에 줄을 서게 된다.
- CPU사용 시간이 짧은 대화형 프로세스는 우선순위 높은 RR큐에서 빠르게 서비스 받고 나감

- 그런데 실행시간 8초 안에 작업을 못 끝내면
- [quantum = 16]큐로 강등되어 줄을 서야 함
- 또 못 끝내면 [FCFS]에 가서 줄을 서야 함

- 우선순위는 [quantum = 8]이 가장 높으므로,
- 오래 걸리는 작업은 뒤로 밀리게 됨.
```

- 👍🏻 `CPU burst time`이 짧은 프로세스부터 빨리빨리 처리해 나갈 수 있음
- 👍🏻 `RR`을 더 발전시켜, 프로세스 `CPU burst time`을 다단계로 분류함으로써,
- 짧은 프로세스일수록 더 빠른 서비스가 가능하도록 하고
- 작업이 긴 프로세스는 `context switching`없이 CPU작업에만 열중할 수 있도록 `FCFS`

#### ☑️ Multilevel Feedback Queue Scheduler를 정의하는 파라미터들

- `queue`의 수
- 각 `queue`의 `scheduling algorithm`
- `process`를 상위 `queue`로 보내는 기준
- `process`를 하위 `queue`로 보내는 기준
- 프로세스가 CPU서비스를 받으려 할 때 들어갈 `queue`를 결정하는 기준

## ✅ Multiple Processor Scheduling

> CPU가 여러개인 경우 Scheduling은 더욱 복잡!

- ✔️ **Homogeneous processor**

  - `queue`에 *한 줄*로 세워서 각 프로세스가 꺼내가게 구현
  - 👎🏻 반드시 특정 `processor`에서 수행해야 하는 프로세스가 있는 경우 복잡😓

- ✔️ **Load Sharing**

  - CPU별로 줄 세우기
  - 👎🏻 특정 CPU한테 프로세스가 편중되는 것을 막기 위해 _각 CPU별 부하가 적절히 분산되도록_ 하는 `부하균형 메커니즘` 필요

- ✔️ **Symmetric Multiprocessing SMP**
  - 각 CPU가 알아서 스케쥴링 결정
  - 모든 CPU가 동일/동등

<br>

- ✔️ **Asymmetric Multiprocessing**
  - 하나의 CPU가 다른 모든 CPU의 스케쥴링 및 데이터 접근을 책임지고
  - 나머지 CPU들은 거기에 따른다.

## ✅ Real Time Scheduling

> Real Time Job: 시간 제한 `deadline` 이 있어서 그 시간 내에 꼭 끝마쳐야 하는 일 <br>

- ✔️ **Hard real-time systems**

  - 정해진 시간 `deadline`내에 끝마치지 않으면 큰일 남💣
  - 반드시 `deadline`를 지키도록 한다.
  - CPU Scheduling을 미리 해두고 그것을 그대로 따라가도록 한다.
  - (이미 어떤 일이 올 것인지 알고 있음)

- ✔️ **Soft real-time computing**

  - 정해진 시간 `deadline`내에 끝마치지 않으면 작은 문제가 생김(동영상 끊김)
  - 일반 프로세스에 비해 높은 priority를 가지도록 한다.

## ✅ Thread Scheduling

- ✔️ **Local Scheduling**

  - user-level thread
  - 사용자 수준의 `thread library`에 의해 어떤 thread를 스케쥴링할지 결정
  - `thread library`가 어떤 thread에게 CPU줄지 결정

- ✔️ **Global Scheduling**

  - kernel-level thread
  - 운영체제가 thread의 존재를 알고 있으므로 OS가 어떤 thread에게 CPU줄지 결정

## 📌 Algorithm Evaluation

> 어떤 CPU scheduling algorithm이 좋을까? 평가하기

- ✔️ **Queueing models**

  - `확률 분포`로 주어지는 `arrival rate`와 `service rate`등을 통해 각종 `performance index`값을 계산
  - 이론적인 계산 방법
  - 복잡한 수식을 계산해 얻어낸 값
  - throughput, waiting time등 계산

- ✔️ **Implementation & Measurement**

  - 구현 & 성능 측정
  - 실제 시스템에 알고리즘 구현 후 실제 작업`workout`에 대해서 성능을 측정, 비교
  - 내가 만든 알고리즘이 기존 알고리즘에 비해 좋은가?
  - 어렵고 복잡하 방법

- ✔️ **Simulation**

  - 실제 시스템을 구현하는게 아니라 가상으로 구현
  - 알고리즘을 모의 프로그램으로 구현 후 비교
  - 여러 상황`trace`를 실제 상황과 비슷하게 주고 실험
  - `Implementation & Measurement`은 너무 어렵고 복잡하니까
