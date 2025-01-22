---
title: KOCW_Deadlock
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ Deadlock

> 교착 상태 <br>
> 한 프로세스가 자원을 가지고 있으면서 다른 프로세스의 자원을 기다림 <br>
> 일련의 프로세스들이 **서로가 가진 자원을 기다리며** block된 상태 <br>

- ❓ **Deadlock이 생기는 이유?**
- 자원을 동시에 여러개 얻어야 하는데,
- 내 자원은 내놓지 않으면서
- 얻기만 하려고 하니까 문제가 생김

- ✔️ **Deadlock 예시**
- 시스템에 자원 `R1`, `R2`가 있다.
- 프로세스 `P1`, `p2`모두 2개의 자원을 할당받아야 수행할 수 있다.
- 각각 하나씩 가지고 다른 프로세스가 반납하기를 기다리고 있다.
- 두 프로세스는 데드락 상황이다.

```
P1       P2
P(R1)   P(R2)
P(R2)   P(R1)
```

## ✅ Resource

- Deadlock에서 이야기하는 Resource는 하드웨어/소프트웨어 등을 포함하는 개념
- 예시: `I/O device`, `CPU cycle`, `memory space`, `semaphore`
  <br>

- ✔️ **프로세스가 자원을 얻고, 사용하는 절차**
- 자원 사용 일련의 과정: `Request`, `Allocate`, `Use`, `Release`
- `Request`: 요청
- `Allocate`: 할당 받음
- `Use`: 사용
- `Release`: 반납

## ✅ Deadlock발생의 4가지 조건

> 4가지 조건을 모두 만족해야 deadlock발생

- ✔️ **mutual exclusion**: 매 순간 하나의 프로세스만 자원 사용 가능, 공유 불가
- ✔️ **no preemption**: 자원 강제로 빼앗을 수 없음
- ✔️ **hold and wait**: 내가 보유한 자원은 절대 놓지 않고 다른 자원을 기다림
- ✔️ **circular wait**: 자원을 기다리는 프로세스 간에 사이클이 형성되어야 함

## 📌 Resource Allocation Graph

> 자원 할당 그래프 <br>
> 자원과 프로세스의 관계를 그림으로 나타내기 <br>

<img width="421" alt="Image" src="https://github.com/user-attachments/assets/a78e8813-8cfe-4f0a-b8cb-8cb6efebe7d6" />

- 프로세스: 원
- 자원: 사각형
- 인스턴스: 사각형 안의 까만점(하나의 자원 안에 인스턴스가 n개 있으면 n개 프로세스가 쓸 수 있음)
- `P1` ➡️ `R1`: 프로세스 `P1`이 자원`R1`을 요청하고 있다.
- `R2` ➡️ `P1`: 자원`R2`가 프로세스`P1`에게 할당되어 있다.
- `P1`은 2번 자원을 쓰면서 1번 자원을 쓰려고 기다리고 있음

<img width="445" alt="Image" src="https://github.com/user-attachments/assets/77ff1e1d-17d5-43e8-8acd-f956498ff744" />

- ✔️ **자원 할당 그래프에 cycle이 존재하는 경우**
- 왼쪽 그래프:

  - 자원 당 인스턴스가 1개라면 deadlock ⭕️
  - Resource Allocation Graph는 deadlock이 맞음 ⭕️

- 오른쪽 그래프:
  - 자원 당 인스턴스가 여러개라면, deadlock 일 수도 있고, 아닐 수도 있다.
  - `cycle`이 있지만, 인스턴스가 2개 있고
  - 싸이클 안에 포함되지 않은 프로세스가 점유하고 있으므로 deadlock이 아니다.

<br>

- ✔️ **자원 할당 그래프에 cycle이 존재하지 않는 경우**
- deadlock ❌

## ✅ Deadlock 처리 방법

- Deadlock prevention: `deadlock`발생 조건 불만족
- Deadlock avoidance: 자원요청에 대한 부가정보를 사용해 `deadlock`가능성이 없을 때만 자원 할당
- Deadlock detection: `deadlock` 발생 허용, 이후 terminate/preempt
- Deadlock ignorance

## ☑️ Deadlock Prevention

> 자원 할당 시 `Deadlock발생의 4가지 조건`중 어느 하나가 만족되지 않도록 한다.

- 🆚 `deadlock`방지
- 앞선 `Deadlock발생의 4가지 조건`중 하나 이상을 불충족하도록 한다

- ✔️ **mutual exclusion 조건 위배하기**:

  - _조건 위배 결과: 프로세스들은 공유 자원에 동시에 접근할 수 있다._
  - 불충족할 수가 없음, 공유해서는 안되는 자원의 경우 반드시 성립해야 함
    <br>

- ✔️ **no preemption 조건 위배하기**:

  - _조건 위배 결과: 프로세스가 기다려야 하는 상황이 생기면 이미 보유한 자원을 빼앗긴다_
  - 모든 필요한 자원을 얻을 수 있을 때 그 프로세스 다시 시작
  - 👎🏻 하지만 모든 자원을 빼앗을 수 있는 건 아님
  - `state`를 쉽게 `save`하고 `restore`할 수 있는 자원은 뺴앗아도 됨(CPU, memory)
  - 하지만 빼앗을 수 없는 자원도 있음(도중에 뺴앗으면 결과가 이상해진다던가)
    <br>

- ✔️ **hold and wait 조건 위배하기**:

  - _조건 위배 결과: 자원을 요청할 때 다른 어떤 자원도 가지고 있지 않아야 한다._
  - 프로세스가 자원을 요청하고 싶으면/기다려야 하면 가진 자원을 내놓는다
  - 프로세스가 자원을 요청할 때 다른 어떤 자원도 가지고 있지 않아야 한다.
  - 💊 방법 1: 프로세스 시작 시 모든 필요한 자원 할당 👎🏻 자원 낭비 심함
  - 💊 방법 2: 자원이 필요할 경우 보유 자원을 모두 놓고 다시 요청

<br>

- ✔️ **circular wait 조건 위배하기**:

  - _조건 위배 결과: 모든 자원 유형에 순서를 정하여 정해진 순서대로만 자원을 할당한다._
  - 💊 모든 자원 유형에 할당 순서를 정해서
  - 정해진 순서대로만 자원을 할당받을 수 있다.
  - 1번 자원을 얻어야만 2번 자원 얻을 수 있음
    <br>

- 👎🏻 `Deadlock Prevention`는 utilization 저하
- 👎🏻 throughput 감소
- 👎🏻 starvation 문제

## ☑️ Deadlock Avoidance

> 프로세스의 **최대 자원 사용량**을 미리 알고, `deadlock`에 들어가지 않는 안전한 경우에 한해서 자원 할당 <br>
> 즉, 프로세스가 자원을 요청했을 때 <br> > **그 프로세스가 최대 요청할 수 있는 자원보다 현재 가용 자원량이 클 경우에만 할당해준다.** <br>
> 시스템이 `unsafe state`에 들어가지 않는 것을 보장 <br>

- 🆚 `deadlock`방지
- 자원 요청에 대한 **부가 정보**를 이용해서`미래 자원 사용량`
- 자원 할당이 `deadlock`으로부터 안전`safe`한지를 동적으로 조사하고
- 안전한 경우에만 자원 할당
- 프로세스가 필요로 하는 **각 자원별 최대 사용량**을 미리 선언해서 부가 정보로 활용

<br>

- 시스템이 `safe state`에 있으면 ➡️ no deadlock ➡️ 자원 할당 ⭕️
- 시스템이 `unsafe state`에 있으면 ➡️ possibility of deadlock ➡️ 자원 할당 ❌

<br>

- ✔️ **safe state**
  - 시스템 내의 프로세스들에 대한 `safe sequence`가 존재하는 상태
  - `deadlock`이 발생하지 않는 상태
- ✔️ **safe sequence**
  - 프로세스의 `sequence<P0, P1...Pn`이 `safe`하려면 `Pi(1<= i <= n)` 프로세스의 자원 요청이 `가용 자원 + Pj(j<1)프로세스의 총 보유 자원`에 의해 충족되어야 함
  - 위 조건을 만족하면 다음 방법으로 모든 프로세스의 수행 보장
  - `Pi`의 자원 요청이 즉시 충족될 수 없으면 모든 `Pj(j<i)`가 종료될 때까지 기다린다

```
Banker's Algorithm에서

먼저 가용자원(놀고 있는 여유자원)으로 최대 자원 사용량을 만족해 끝낼 수 있는 프로세스를 찾는다(Pj)
그 프로세스가 자원 사용이 끝나면 자원을 반납할 것이고
그러면 가용 자원은 늘어날 것이다(기존 가용 자원 + Pj가 반납한 자원)
이를 또 반복해 최대 자원 사용량을 만족해 끝낼 수 있는 프로세스를 하나하나 끝내다보면
모든 프로세스(Pi)를 끝낸다

- 이 떄 우리는 safe sequence가 있다고 하고
- 이 상태를 safe state라고 한다.
```

- 👎🏻 `Deadlock Prevention`는 utilization 저하
- 👎🏻 throughput 감소
- 👎🏻 starvation 문제

### 💡 Single instance per resource types

> Deadlock Avoidance에서 Resource Allocation Graph 사용

- 하나의 자원에는 인스턴스도 한 개

<br>

- 프로세스가 자원을 **미래에** 필요로할지도 고려해 자원 할당 <br>
- 그래프 `Resource Allocation Graph`의 점선까지 판단해서 `deadlock`이 될 가능성이 있으면 자원 할당 ❌ <br>

<img width="433" alt="Image" src="https://github.com/user-attachments/assets/dd21b912-b2fb-4062-b698-5b0eb0ac5456" />

- **점선**: 프로세스가 자원을 요청할 수도 있다 **(현재 요청한건 아님)**
- 실선: 프로세스가 해당 자원을 실제로 요청
- 따라서 `cycle`이 생겨도 점선으로 이루어져 있으면 현재 `deadlock`은 아니다
  <br>

- 하지만 Deadlock Avoidance는 현재 여유 자원이 있음에도 불구하고
- `deadlock`이 될 가능성이 있다고 판단되면, 자원을 할당하지 않는다 ❌
- 따라서 `자원2`는 현재 놀고있지만, `프로세스2`에게 할당해주지 않음
  <br>

- Deadlock Avoidance는 `Resource Allocation Graph`을 고려해서 자원 할당 결정
- Deadlock Avoidance는 이런 **점선**도 고려해서 자원을 줄지, 말지 결정

### 💡 Multiple instance per resource types

> Banker's Algorithm 사용

- 하나의 자원에 여러개 인스턴스 있는 경우
- 프로세스가 미래에 자원을 얼마나 추가 요청할지 판단해서 자원 할당해줄지 말지 판단

<img width="363" alt="Image" src="https://github.com/user-attachments/assets/8da5e6de-e825-44a1-902a-608334ea1534" />

- `Allocation`: 현재 프로세스에 할당된 자원 개수
- `Max`: 각 프로세스가 평생동안 최대 요청할 자원 개수(`Deadlock avoidance`는 프로세스의 **최대 자원 사용량**을 미리 알고 있음)
- `Available`: 현재 사용 가능한 자원(놀고 있는 여유 자원)
- `Need(Max-Allocation)`: 각 프로세스가 미래에 추가로 요청할 수 있는 자원(`Max` - `Allocation`)

<img width="363" alt="Image" src="https://github.com/user-attachments/assets/6403f572-880e-48cb-89aa-0d025e2a3e02" />

```
현재 프로세스 P0은 자원(A, 0), (B, 1), (C, 0)개 가지고 있음
그리고 자원(A, 3), (B, 3), (C, 2)개가 놀고 있음

❓ 이 상황에서 P0이 C를 요청하면?
Banker's Algorithm에서는 (C, 2)개 놀고있지만, 주지 않는다. ❌
왜냐하면 P0은 C를 최대 3개까지 요청할 수 있기 때문에,
그리고 P0은 non-preemptive하다고 생각하기 때문에,
2개 줘버렸다가 3개까지 추가 요청해버리면 deadlock이 걸릴 수 있기 때문이다
따라서 C가 3개 이상 있을 때 P0에게 C자원을 할당해 줄 것

❓ 반면, P1이 C를 요청하면
P1는 C를 최대 2개까지만 쓰기 때문에 할당해준다.
```

- `sequence<P1, P3, P4, P2, P0>`이 존재하므로 시스템은 `safe state`에 있다.

## ☑️ Deadlock Detection and recovery

> `deadlock`발생은 허용하되, 그에 대한 `detection`루틴을 두어 <br>
> 만약 `deadlock`발생 시 `recover` <br>

- 🆚 `deadlock`발생 허용 후 recovery
- 💁🏻‍♀️ `deadlock`이 자주 생기지도 않는데, 생길까봐 여유 자원을 안주는 것도 비효율적이잖아?
- 여유자원 있으면 그냥 바로바로 할당, 그냥 `deadlock` 생기게 두고,
- 생겼을 때 recovery

- 👎🏻 deadlock detection overhead
- 👎🏻 starvation

### 💡 Deadlock Detection and Recovery

> deadlock이 생겼나, 안 생겼나 판단하고 recover

#### ✔️ **Single instance per resource types**

- `Resource Allocation Graph`에 `cycle`이 있으면
- `deadlock`이라고 판단

- 📌 **Wait-for graph**
- `resource allocation graph`에서 자원을 생략하고 간단하게 표시
- `Wait-for graph`에서 cycle이 존재한다면, `deadlock`
- `DFS` 또는 `BFS` 알고리즘을 활용하여 cycle을 찾을 수 있다

<img width="583" alt="Image" src="https://github.com/user-attachments/assets/de7ff60d-b9ec-4ef8-bc09-636cb8cd9ec7" />

#### ✔️ **Multiple instance per resource types**

- Banker's Algorithm과 유사한 방법 활용
- `deadlock detection`에서는 프로세스가 자원을 요청하면 그냥 준다.
- 자원 추가 요청을 하지 않는 프로세스는 보유한 자원을 반환할 것이라고 가정한다.
- 그러다가 모든 자원이 할당이 되어 여유가 없고
- 프로세스들은 계속 자원을 추가요청하며 자신의 자원은 내어놓지 않는 상태라면
- `deadlock`이라고 판단
- 🆚 `deadlock avoidance`와는 다르게 그냥 여유자원이 생기면 바로바로 할당해줘버렸기 때문에 이런 문제가 발생

<img width="361" alt="Image" src="https://github.com/user-attachments/assets/7bb32795-5472-4116-bec1-e8f013be6761" />

```
이 경우 P0, P2는 추가 요청을 하고 있지 않음
따라서 수행 후에는 자원을 내어 놓을 것임
그러면 여유 자원이 생기고, 이 자원들로 나머지 프로세스 추가 요청을 수행
따라서 sequence<P0, P2, P3, P1, P4>순서로 작동하므로 deadlock이 아니다
```

### 💡 Deadlock Recovery

#### ✔️ **Process termination**

- 방법 1: `deadlock`에 연류된 프로세스는 다 죽이기
- abort all deadlocked processes
  <br>

- 방법 2: 프로세스를 하나하나 죽이며 `deadlock`이 해결되는지 살펴보기
- abort one process at a time until the `deadlock cycle` is eliminated

<br>

#### ✔️ **Resource preemption**

- `deadlock`에 연류된 프로세스의 자원 뻇기
- 비용을 최소화할 `victim`선정
- `safe state`로 `rollback`하여 `process restart`
- 👎🏻 Starvation
- 동일한 프로세스가 계속 `victim`으로 선정되는 경우
- `cost factor`에 `rollback` 횟수도 고려해야 함

## ☑️ Deadlock Ignorance

> `deadlock`을 시스템이 책임지지 않음 <br>
> UNIX등 대부분 OS가 채택하는 방식<br>

- 🆚 `deadlock`발생 허용
- `deadlock`은 자주 일어나지 않으니, 그냥 무시
- `deadlock`은 매우 드물게 발생하므로, `deadlock`에 대한 조치 자체가 더 큰 `overhead`라고 생각
- 만약 시스템에 `deadlock`이 발생한 경우, 사람이 답답함을 느끼고, 사람이 직접 프로세스를 죽이는 방법으로 대처
