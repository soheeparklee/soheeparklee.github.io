---
title: KOCW_Deadlock
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ Deadlock

> 교착 상태 <br>
> 한 프로세스가 자원을 가지고 있으면서 다른 프로세스의 자원을 기다림 <br>
> 일련의 프로세스들이 서로가 가진 자원을 기다리며 block된 상태

- ❓ **Deadlock이 생기는 이유?**
- 자원을 동시에 여러개 얻어야 하는데,
- 내 자원은 내놓지 않으면서
- 얻기만 하려고 하니까 문제가 생김

## ✅ Resource

- Deadlock에서 이야기하는 Resource는 하드웨어/소프트웨어 등을 포함하는 개념
- 예시: `I/O device`, `CPU cycle`, `memory space`, `semaphore`

- ✔️ **프로세스가 자원을 얻고, 사용하는 절차**
- 자원 사용 일련의 과정: `Request`, `Allocate`, `Use`, `Release`
- `Request`: 요청
- `Allocate`: 할당 받음
- `Use`: 사용
- `Release`: 반납

## ✅ Deadlock발생의 4가지 조건

- ✔️ **mutual exclusion**: 매 순간 하나의 프로세스만 자원 사용 가능, 공유 불가
- ✔️ **no preemption**: 자원 빼앗을 수 없음
- ✔️ **hold and wait**: 내가 보유한 자원은 절대 놓지 않고 가지고 있음
- ✔️ **circular wait**: 자원을 기다리는 프로세스 간에 사이클이 형성되어야 함

## 💡 Resource Allocation Graph

> 자원 할당 그래프 <br>
> 자원과 프로세스의 관계를 그림으로 나타내기

<img width="421" alt="Image" src="https://github.com/user-attachments/assets/a78e8813-8cfe-4f0a-b8cb-8cb6efebe7d6" />

- 프로세스: 원
- 자원: 사각형
- 인스턴스: 점(하나의 자원 안에 인스턴스가 n개 있으면 n개 프로세스가 쓸 수 있음)
- `P1` ➡️ `R1`: 프로세스 `P1`이 자원`R1`을 기다리고 있다.
- `R2` ➡️ `P1`: 자원`R2`가 프로세스`P1`에게 가 있다.
- `P1`은 2번 자원을 쓰면서 1번 자원을 쓰려고 기다리고 있음

<img width="445" alt="Image" src="https://github.com/user-attachments/assets/77ff1e1d-17d5-43e8-8acd-f956498ff744" />

- 왼쪽 Resource Allocation Graph는 deadlock이 맞음
- 오른쪽은 `cycle`이 있지만, 인스턴스가 2개 있고 싸이클 안에 포함되지 않은 프로세스가 점유하고 있으므로 deadlock이 아니다.

## ✅ Deadlock 처리 방법

#### ☑️ Deadlock Prevention

- `deadlock`방지
- 앞선 `Deadlock발생의 4가지 조건`중 하나 이상을 불충족하도록 한다

- ✔️ **mutual exclusion**: 불충족할 수가 없음, 공유해서는 안되는 자원의 경우 반드시 성립해야 함
- ✔️ **no preemption**:
  - 프로세스가 기다려야 하는 상황이 생기면 이미 보유한 자원을 빼앗김
  - 모든 필요한 자원을 얻을 수 있을 때 그 프로세스 다시 시작
  - 하지만 모든 자원을 빼앗을 수 있는 건 아님
  - `state`를 쉽게 `save`하고 `restore`할 수 있는 자원은 뺴앗아도 됨(CPU, memory)
  - 하지만 빼앗을 수 없는 자원도 있음(도중에 뺴앗으면 결과가 이상해진다던가)
- ✔️ **hold and wait**:
  - 프로세스가 기다려야 하는 상황이 생기면 가진 자원을 내놓는다
  - 프로세스가 자원을 요청할 때 다른 어떤 자원도 가지고 있지 않아야 한다.
  - 방법 1: 프로세스 시작 시 모든 필요한 자원 할당 👎🏻 자원 낭비 심함
  - 방법 2: 자원이 필요할 셩우 보유 자원을 모두 놓고 다시 요청
- ✔️ **circular wait**:

  - 모든 자원 유형에 할당 순서를 정해서
  - 정해진 순서대로만 자원을 할당받을 수 있다.
  - 1번 자원을 얻어야만 2번 자원 얻을 수 있음

- 👎🏻 `Deadlock Prevention`는 utilization 저하
- 👎🏻 throughput 감소
- 👎🏻 starvation 문제

#### ☑️ Deadlock Avoidance

- `deadlock`방지
- 자원 요청에 대한 **부가 정보**를 이용해서 자원 할당이 `deadlock`으로부터 안전`safe`한지를 동적으로 조사하고
- 안전한 경우에만 자원 할당
- 프로세스가 필요로 하는 **각 자원별 최대 사용량**을 미리 선언하도록 하는 방법이 가장 일반적

- ✔️ **safe state**
- 시스템 내의 프로세스들에 대한 `safe sequence`가 존재하는 상태

- ✔️ **safe sequence**

#### 💡 Deadlock Avoidance에서 Resource Allocation Graph

<img width="433" alt="Image" src="https://github.com/user-attachments/assets/dd21b912-b2fb-4062-b698-5b0eb0ac5456" />
- 점선: 프로세스가 자원을 요청할 수도 있다(현재 요청한건 아님)
- 실선: 프로세스가 해당 자원을 실제로 요청
- 따라서 `cycle`이 생겨도 점선으로 이루어져 있으면 `deadlock`이 아니다

- Deadlock Avoidance는 이런 점선도 고려해서 자원을 줄지, 말지 결정

#### ☑️ Deadlock Detectoin and recovery

- `deadlock`발생 허용 후 recovery

#### ☑️ Deadlock Ignorance

- `deadlock`발생 허용

## ✅

## ✅

## ✅

CPU
