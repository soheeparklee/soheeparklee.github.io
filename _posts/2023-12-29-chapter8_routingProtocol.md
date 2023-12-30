---
title: PART7_Routing Protocol
categories: [Computer Science, CISCO networking]
tags: [cs]
---

## 1️⃣ RIP: Routing Information Protocol

표준 라우팅 프로토콜: 모든 라우터에서 지원

- Routing protocol
- Dynamic protocol
- Interior Gateway Protocol 내부용 라우팅 프로토콜
- Distance Vecoor
  Distance거리, Vector방향으로 길을 찾아간다.
- Hop 카운트: 좋은 길을 결정하는 기준
- 최대 홉 카운트 개수: 15개
- 라우팅 업테이트 주기: 30초

### ☑️ RIP 장단점

👍🏻 라우터의 메모리를 적게 사용
👍🏻 소규모 네트워크에서는 효율적
👎🏻 RIP는 가장 홉 카운트 낮을수록 ⬇️ 더 좋은 경로라고 믿음.
그래서 회선의 속도, 신뢰도, 회선의 로드 등을 확인하지 않음.
오로지 홉 카운트만 확인하다보니 가장 좋은 경로가 아닌데도 계속 그 길을 감.
👎🏻 최대 라우팅할 수 있는 거리가 짧다
15개 이상의 라우터를 거치는 목적지는 Unreachable
👎🏻 커다란 네트워크에서는 사용 ❌
👎🏻 VLSM 지원 불가

### ☑️ 로드 밸런싱

로드를 분산해서 보내는 것

## ☑️ Administratice Distance

라우터의 한 쪽은 RIP 프로토콜, 다른 한 쪽은 IGRP를 쓴다면
라우터는 어떤 경로 정보를 RIP와 IGRP에서 동시에 받음.
그러면 어떤 라우팅 프로토콜에서 온 정보를 이용해서 경로를 찾아야 할까❓

정답: **Administratice Distance**값을 보고 디스턴스 값이 더 작은 쪽의 말을 듣는다.
라우팅 프로토콜별로 디스턴스 값을 가지고 있다.
디스턴스 값이 낮으면 낮을수록⬇️ 신뢰성 높다⬆️

예를 들어, RIP는 120, IGRP는 100
따라서 IGRP 프로토콜 말을 들을 것이다.

## 👎🏻 Distance Vector 라우팅 알고리즘의 문제점

- RIP
- IGRP

🆚 Link State

- OSPF

### 👎🏻 문제점: Convergence Time

업데이트가 모든 네트워크에 전달되는 시간(Convergence Time)이 많이 걸린다.

Distance Vector 알고리즘은 업데이트 주기를 가지고 있는데, 이 주기가 지나야 다른 네트워크들은 네트워크에 변화가 생겼다는 것을 인지

### 👎🏻 문제점: 루핑

#### 루핑 발생 이유

1. 한 라우터가 라우팅 정보에 대한 모든 정보를 가지고 있지 못하고
2. 이웃 라우터로부터 업데이트 Convergence Time 때문에 느리게 이루어져서

네트워크로 향하는 데이터가 뱅글뱅글 돌기만 할 뿐 목적지에 도착하지 못해 네트워크에 엄청난 트래픽 발생

## ✅ Distance Vector 라우팅 알고리즘 해결책

하나의 루핑 방지 방법만 쓰는게 아니라 여러 가지 방식을 적절히 섞어서 활용

### 💡 Maximum hop count

Maximum hop count를 예를 들어 15로 정해놓으면 루핑이 발생하더라도 16까지 이르면 멈추게 된다.
또 flush time지나면 라우팅 테이블에서 아예 경로 삭제
👎🏻 그러나 네트워크 규모가 커지는 경우 15넘어서는 네트워크 경로에 대해서는 아예 도달 못하게 된다는 단점.

### 💡 Hold down timer

Hold down timer가 동작하고 있을 때 외부에서 해당 네트워크에 대한 라우팅 경로가 들어오면
원래 가지고 있던 메트릭 값보다 큰 값이 들어오면 무시해버림 😑

Hold down timer가 종료되거나
목적지에 대한 새로운 값이 지금 내가 가지고 있는 메트릭과 **같거나 더 좋으면** 업데이트 받아들임. 👌🏻

Hold down timer사용해서 어떤 경로가 죽었다고 판단되면 이 경로에 대한 상태를 바로 바꾸지 않고 ❌
일정 시간이 지나는 동안 기다렸다가 바꾸겠다.

#### 메트릭 값: 목적지까지의 거리에 대한 값

RIP의 경우 Hop count

### 💡 Split Horizon ⭐️⭐️⭐️

⭐️ 라우팅 정보가 들어온 곳으로는 같은 정보를 내보낼 수 없다.

⭐️ 다만, 모든 라우팅 업데이트를 내보내지 않는다는 것은 아니고!!! ❌
들어온 정보에 대한 라우팅 정보만 내보내지 않는 다는 것

⭐️ 만약 하나의 라우터가 어느 네트워크 정보를 인접한 라우터A에게서 받았다면, 그 인접한 라우터A가 네트워크에 더 가까이 있을 것이므로 정보를 다른 라우터들로부터 받을 필요가 없을 것이다.

⭐️ 두 라우터 간의 루핑만을 막기 위해 만들어진 기술
따라서 전체 라우터 네트워크의 루핑을 Split Horizon이 막을 수는 없다. ❌
라우팅 루프를 자기 라우터랑 붙어있는 인접 라우터에서만 방지 가능

### 💡 Routing Poisoning

다운된 네트워크의 메트릭 값을 먼저 무한대치로 만들어 버려서 사용할 수 없는 값으로 만든다.
대신 라우팅 테이블에서 지워버리지는 않음

### 💡 Poison Reverse

Split Horizon 변형
라우팅 정보를 되돌려보내기는 하되, 이 값을 무한대 값으로 쓴다.
경로 정보를 아주 없애는 것보다 무한대 홉 값을 포함해 라우팅 업데이트를 실시한다면 다른 모든 라우터들은 실수로 잘못된 경로 정보 사용하는 경우 줄일 수 있으므로

## ☑️ VLSM: Variable Length Subnet Mask

IP주소의 효율적 이용을 위해 한 라우터에 접속되는 네트워크마다 서로 다른 서브넷 마스크를 줄 수 있도록 만든 규칙
라우터의 각 인터페이스별로 Subnet Mask가 전부 제각각
이더넷쪽 Subnet Mask와 시리얼쪽 Subnet Mask를 같지 않게 한다.
RIP, IGRP는 VLSM ❌
static routing protocol, EIGRP, OSPF에는 VLSM ⭕️

## 2️⃣ IGRP: Interior Gateway Routing Protocol

- Routing Protocol
- Dynamic Routing Protocol
- Interior Gateway Protocol
- Distance Vector protocol
- 90초에 한번씩 라우팅 테이블 업데이트
- Only sisco routers
- 다양한 요인들을 따져 경로 결정

### 🆚 RIP

- RIP는 표준 프로토콜, 모든 라우터가 RIP 지원
- IGRP는 시스코 라우터에서만 사용 가능
- RIP는 hop 카운트만 따져서 경로 결정
- IGRP는 5개 요인들을 따져서 경로 결정
- RIP는 최대 홉 카운트 15개
- IGRP는 홉 타운트 15개 넘어갈 수 있음

공통점

- Distance Vector Protocol
- VLSM 지원 불가

### ☑️ IGRP가 경로 결정하는데 고려하는 요소

#### ✔️ Bandwidth 속도(대역폭)

Kbps 속도
최적의 경로 찾기 위해 Bandwidth고려

#### ✔️ Delay 지연

경로를 통해서 도착할 때까지 지연되는 시간

#### ✔️ Reliability 신뢰성

케이블이나 전용선 등 전송 매체 통해 패킷 보냈을 때, 생기는 에러율
목적지까지 제대로 도착한 패킷과 에러가 발생한 패킷의 비율
keepalive: 출발지와 목적지 사이의 신뢰도 측정
keepalive 수치 ⬆️ 신뢰도 ⬆️

#### ✔️ Load 부하, 하중

출발지와 목적지 사이에 얼마나 부하가 생기는가?

#### ✔️ MTU: Maximum Transmission Unit

경로의 최대 전송 유닛 크기, 바이트

### ☑️ IGRP 장단점

👍🏻 5가지 요인을 고려하니 RIP보다 지능적으로 경로 찾음
👍🏻 홉 카운트 15개 넘어가도 데이터 전송 가능
👎🏻 VLSM 지원 불가
👎🏻 sisco 라우터에서만 사용 가능

## ✅ PPS: Packet Per Second

초당 전송하는 패킷 수

- IFG Inter Frame Gap
  프레임과 프레임 사이의 간격
- Preamble Time
  프레임 앞에 붙는 서론 시간

## ✅ DHCP: Dynamic Host Configuration Protocol

PC나 호스트가 자신의 IP주소 가지고 있지 않음
부팅되면 DHCP서버로부터 하나씩 다이내믹하게 IP주소를 받는다.
👍🏻 IP주소 자동으로 배정
👍🏻 IP주소 효율적으로 관리

## 3️⃣ OSPF
