---
title: KOCW_Thread
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ Thread

> thread is a lightweight process <br>
> basic unit of CPU utilization <br>
> 프로세스 내에서 CPU의 수행 단위 <br>

- thread는 프로세스 내에서 실행되는 흐름의 단위
- thread는 프로세스의 특정한 수행 경로
- thread는 프로세스가 할당받은 자원을 이용하는 실행의 단위

- 👍🏻 thread는 프로세스의 자원과 메모리를 공유한다.
  - 👍🏻 쓰레드 간 효율적인 통신 가능
  - 👍🏻 쓰레드는 생성이 빠르다
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

## ✅ TCB

> Thread Control Block <br>
> 쓰레드 제어 블록 <br>

- 각 thread는 별도의 `stack`, `TBC`를 가진다.
- `TBC`에는 `쓰레드 상태 정보`, `register`, `우선순위`등을 포함한다.

## ✅ Thread의 장점

- 👍🏻 **resource sharing**
- share binary code, data, resource of process
- communication among thread
- 쓰레드는 `자원을 공유하기 때문`에 `쓰레드 간 교환`이 `프로세스 간 교환`보다 빠르고 효율적이다.

- 👍🏻 **communication**
- 프로세스 간 통신은 `kernel`이 개입해야 하지만
- 같은 프로세스 간 통신은 `메모리와 파일을 공유`하기 때문에 커널 호출 없이 효율적으로 통신 가능

- 👍🏻 **responsiveness**
- 응답성이 빠르다
- if one thread is blocked(network) another thread continues
- `다중 thread` 태스크에서는 하나의 서버 thread가 `blocked(waiting)`상태여도 동일한 태스크 내의 다른 thread가 `running`할 수 있다.
- 만약 thread가 없다면, 프로세스가 I/O를 하면 `blocked(waiting)`상태가 될 것이다. 프로세스는 CPU를 빼앗기게 된다.
- 하지만 `다중 thread`에서는 하나의 thread가 I/O를 해도 다른 thread가 `running`, CPU를 빼앗기지 않는다.
- 예를 들어, 검색창에 URL을 넣고 새로운 페이지를 불러올 때 I/O작업이므로 프로세스를 `blocked`하고 기다리면, 유저는 답답🙁
- 따라서 `html`만이라도 하나의 `thread`가 빨리 불러오고, 또 다른 `thread`가 이미지 URL을 불러와서 유저 입장에서 빨리 보여지는 것처럼 보이게 한다.

- 👍🏻 **economy**
- `creating`, `CPU switching thread` is much lightweight than `process creation and context switching`
- 프로세스는 `fork`를 통해 자식에게 모든 정보를 복사해야 함
- 하지만 쓰레드는 공유하지 않는 일부만 복사해서 생성할 수 있음 `pthread_create()`
- ➡️ _multithreading_

- 👍🏻 **Utilization of MP Architectures**
- 여러개의 CPU가 있는 환경에서는 병렬성을 추가할 수 있다
- each thread may be running parallel on a different processor

- 👍🏻 비동기식 I/O를 가능하게 한다.
- 하나의 `thread`가 I/O 요청하고 결과 기다리는 동안, 다른 `thread`는 결과가 필요 없는 다른 일을 먼저 한다.

---

- ❓ **왜 쓰레드 간 교환이 더 빠를까?**
- 쓰레드 간에는 `공유 데이터`가 존재하기 때문에
- 공유하지 않는 부분만 교환하면 된다.

- ❓ **왜 쓰레드 간 교환이 더 효율적일까?**
- 프로세스 간 `context switching`가 일어나면 이전에 `cache`에 저장되어 있던 데이터는 의미가 없어짐
- 프로세스 간에는 공유 데이터가 없기 때문 ❌(`프로세스 A`의 캐시 데이터는 `프로세스 B`에게는 의미가 없음)
- 하지만 쓰레드는 `프로세스 자원`을 공유
- 쓰레드 간 `switching`이 일어난 경우 이전 쓰레드의 `공유자원에 대한 cache`는 의미있는 정보이다.
- (`쓰레드 A`의 캐시 데이터가 `쓰레드 B`에게도 의미가 있음)
- 따라서 쓰레드 간에는 `공유하는 데이터`가 있기 때문에 `switching`이 일어나도 이전 `cache`에 대한 이점이 있다.

## ✅ Multithreading

- 여러개의 쓰레드가 프로세스의 자원을 공유하며 작동
- 👎🏻 쓰레드 간 `race condition`발생 가능
- 👎🏻 쓰레드 간 공유자원에 대한 동기화 필요
- 👎🏻 멀티쓰레딩은 디버깅이 까다롭다.

## ✅ Implementation of threads 쓰레드 구현 방법

- ✔️ **kernal-level thread**
- `kernel`이 `thread`의 존재를 알게 구현
- threads supported by kernel
- `kernel`이 쓰레드와 관련된 모든 작업 수행
- `kernel`이 `thread A`에서 `thread B`로 CPU를 넘겨야지 정함
- 👍🏻 `쓰레드 단위`로 스케쥴링 할 수 있다.
- 👍🏻 따라서 멀티프로세서 환경에서 여러 쓰레드를 동시에 처리 가능
- 👎🏻 쓰레드 간 `context switching`이 자주 발생, 오버헤드

- ✔️ **user-level thread**
- thread supported by library
- 프로그래머가 `쓰레드 라이브러리`를 사용해서 멀티쓰레딩 프로그램 작성
- 운영체제 `kernel`은 thread의 존재를 모른다.
- 운영체제는 그냥 process에게 CPU를 주고, 그 process내에서 thread끼리
  CPU넘기기
- `쓰레드 라이브러리`는 `쓰레드 생성/제거`, `쓰레드 간 메세지/데이터 전달`, `쓰레드 스케쥴링`, `쓰레드 간 교환`에 대한 코드를 포함한다.
- 🆚 `쓰레드 간 교환`에서 `kernel`은 `프로세스 단위`로 스케쥴링을 한다
- `쓰레드 간 context switching`도 `쓰레드 라이브러리`가 제공
- `kernel`의 개입이 필요 없음
- 👎🏻 만약 한 프로세스의 특정 쓰레드가 `block`되면, `kernel`은 프로세스를 통째로 `block`
- 👎🏻 그래서 나머지 쓰레드도 다 `block`

- ✔️ **real time thread**

#### kernal-level thread 🆚 user-level thread

- kernal-level thread
  - `kernel` realizes thread
  - scheduling done by `thread unit`
- user-level thread
  - `kernel` does not realize thread
  - scheduling done by `process unit`
