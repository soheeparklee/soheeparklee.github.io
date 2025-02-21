---
title: KOCW_Memory, Disk Scheduling / Caching
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ 메모리 작동

- 메모리: 휘발성
- 메모리는 비어 있음
- 컴퓨터가 켜지면, 메모리 위에 운영체제가 올라감
- 프로그램은 디스크에 저장되어 있다가(`디스크의 파일시스템`)
- CPU가 필요하면
- 가상 메모리를 만들고(`페이지`)
- 지금 당장 필요한 부분만 실제 물리적인 메모리 위에 올라가게 됨

- 그러다가 메모리가 꽉 차면
- 안 쓰는 프로세스 `페이지`는 디스크(`스왑 영역`)으로 쫒겨난다.

#### 디스크 파일시스템 🆚 디스크 스왑 영역

- 파일시스템: 파일들 저장, 컴퓨터 꺼져도 유지
- 스왑 영역:
  - 디스크의 연장 느낌
  - 컴퓨터 꺼져도 남아는 있으나, 메모리가 사라졌기에 의미 없는 정보
- 메모리: 휘발성

## ✅ 메모리 Scheduling

> 메모리가 꽉 찼는데, 어떤 페이지를 메모리에서 쫒아낼까? <br>

- 미래에 사용될 가능성이 많은 프로세스는 메모리에 두고,
- 미래에 안 사용될 것 같은 프로세스는 쫒아내야 함

### 💡 LRU

> Least Recently Used <br>

- 가장 오래 전에 사용된 페이지 삭제

### 💡 LFU

> Least Frequently Used <br>

- 제일 적게 사용된 페이지 삭제

## ✅ 디스크 Scheduling

- 디스크는 디스크 헤드가 이동하며 데이터를 읽어오는데,
- 따라서 이 헤드의 이동 동선을 최소화하는게 중요함(엘레베이터처럼)
- seek time을 최소화하는게 목표

### ✔️ 디스크 access time

- **탐색 시간 seek time**
- 디스크 헤드가 해당 트랙(실린더)으로 움직이는데 걸리는 시간

- **회전 지연 rotational latency**
- 헤드가 원하는 섹터에 회전에 도달하기까지 걸리는 시간

- **전송 시간 transfer time**
- 실제 데이터의 전송 시간

### 💡 SSTF

> Shortest Seek Time First <br>

- 큐에 들어온 데이터 중 가까운 위치부터 간다.
- 내가 5번에 있는데 순서대로 `10, 7`번이 들어오면 7번부터 간다.
- 👎🏻 Starvation: 멀리 있는 데이터는 안 감, 오래 기다림

### 💡 SCAN

> 헤드는 디스크 한쪽 끝에서 다른쪽 끝으로 쭉 이동 <br>

- 가는 길목에 있으면 처리
- 한 쪽에 도달하면 역방향으로 이동
- 또 가는 길목에 있는 데이터 처리
- 엘리베이터처럼, 1층에서 5층까지 가는데 3층에 불 들어오면 데리고 올라감

- 👍🏻 기아현상 발생 ❌

## ✅ 캐싱

> 빠른 CPU와 느린 I/O장치 간 속도 차이를 어떻게 극복할 것인가? <br>
> caching: copying information into faster storage system <br>

- 여러번 요청되는 데이터는 secondary에서 primary의 캐시에 저장을 해 두고,
- 매번 secondary에서 찾아올 필요 없이 빨리빨리 가져다 쓰자
- 👍🏻 속도가 다른 저장장치의 완충 역할
- 하지만 캐시는 작기 때문에 모든걸 다 저장할 수는 없음

## ✅ Flash Memory

- 반도체장치
- SSD

- 👍🏻 nonvolatile
- 👍🏻 low power consumption 전력소모 적음
- 👍🏻 shock resistance 물리적 충격 잘 견딤
- 👍🏻 작다
- 👍🏻 가볍다
- 👎🏻 쓰기 횟수 제약: 썻다 지웠다 일정 횟수 후에 사용 불가
- 👎🏻 시간이 많이 지나면 데이터가 사라질 수 있음, 전하가 빠져나가서

- 휴대폰에 임베디드
- USB

## ✅
