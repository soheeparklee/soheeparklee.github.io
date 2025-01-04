---
title: KOCW_Thread
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ Thread

> thread is a lightweight process <br>
> basic unit of CPU utilization <br>
> 프로세스 내에서 CPU의 수행 단위

- 👍🏻 context switching을 줄인다(overhead⬇️)

```
- 예를 들어, 웹서핑을 하는데/워드 파일을 편집하는데 여러 개의 창을 띄워놓고 하고 있다고 가정해보자
- 만약 한 개의 창마다 각각의 process라고 한다면
- 실행되는 code는 모두 같고
- 각 process의 data, stack만 다를 것이다.
👎🏻 비효율적

👍🏻 동일한 프로그램을 쓸 때는 프로세스를 여러개 만들지 말고, 한개만 만들자
그래서 code, data, stack은 하나만 만들고,
대신 PC(프로그램에 어디를 실행하고 있는가)만 다르게 하자.
```

## ✅ Thread의 구성

- ✔️ **Thread가 독자적으로 가지는 부분(CPU 관련 부분)**
- PC program counter
- register set
- stack set: 함수호출과 관련된 부분

- ✔️ **Thread가 공유하는 부분(task)**
- 나머지 부분들은 동일 프로세스 안에 있는 Thread끼리 공유한다.
- code section
- data section
- OS resources

## ✅ Thread의 장점

- 👍🏻 **responsiveness**
- 응답성이 빠르다
- if one thread is blocked(network) another thread continues
- `다중 thread` 태스크에서는 하나의 서버 thread가 `blocked(waiting)`상태여도 동일한 태스크 내의 다른 thread가 `running`할 수 있다.
- 만약 thread가 없다면, 프로세스가 I/O를 하면 `blocked(waiting)`상태가 될 것이다. 프로세스는 CPU를 빼앗기게 된다.
- 하지만 `다중 thread`에서는 하나의 thread가 I/O를 해도 다른 thread가 `running`, CPU를 빼앗기지 않는다.
- 예를 들어, 검색창에 URL을 넣고 새로운 페이지를 불러올 때 I/O작업이므로 프로세스를 `blocked`하고 기다리면, 유저는 답답🙁
- 따라서 `html`만이라도 하나의 `thread`가 빨리 불러오고, 또 다른 `thread`가 이미지 URL을 불러와서 유저 입장에서 빨리 보여지는 것처럼 보이게 한다.

- 👍🏻 **resource sharing**
- share binary code, data, resource of process

- 👍🏻 **economy**
- creating, CPU switching thread is much lightweight than process creation and context switching

- 👍🏻 **Utilization of MP Architectures**
- 여러개의 CPU가 있는 환경에서는 병렬성을 추가할 수 있다
- each thread may be running parallel on a different processor

- 👍🏻 비동기식 I/O를 가능하게 한다.
- 하나의 `thread`가 I/O 요청하고 결과 기다리는 동안, 다른 `thread`는 결과가 필요 없는 다른 일을 먼저 한다.

## ✅ Implementation of threads 쓰레드 구현 방법

- ✔️ **kernal thread**
- kernel이 thread의 존재를 알게 구현
- threads supportes by kernel
- thread A에서 thread B로 CPU를 넘겨야지

- ✔️ **user thread**
- thread supported by library
- 운영체제는 thread를 모른다.
- 운영체제는 그냥 process에게 CPU를 주고, 그 process내에서 thread끼리
  CPU넘기기

- ✔️ **real time thread**

## ✅

## ✅

## ✅

CPU
