---
title: PART8_Routing Protocol
categories: [Computer Science, CISCO networking]
tags: [cs]
---

## 1️⃣ RIP: Routing Information Protocol

표준 라우팅 프로토콜: 모든 라우터에서 지원 <br>

- Routing protocol <br>
- Dynamic protocol <br>
- Interior Gateway Protocol 내부용 라우팅 프로토콜 <br>
- Distance Vecoor <br>
  Distance거리, Vector방향으로 길을 찾아간다. <br>
- Hop 카운트: 좋은 길을 결정하는 기준 <br>
- 최대 홉 카운트 개수: 15개 <br>
- 라우팅 업테이트 주기: 30초 <br>

### ☑️ RIP 장단점

👍🏻 라우터의 메모리를 적게 사용 <br>
👍🏻 소규모 네트워크에서는 효율적 <br>
👎🏻 RIP는 가장 홉 카운트 낮을수록 ⬇️ 더 좋은 경로라고 믿음. <br>
그래서 회선의 속도, 신뢰도, 회선의 로드 등을 확인하지 않음. <br>
오로지 홉 카운트만 확인하다보니 가장 좋은 경로가 아닌데도 계속 그 길을 감 <br>. <br>
👎🏻 최대 라우팅할 수 있는 거리가 짧다 <br>
15개 이상의 라우터를 거치는 목적지는 Unreachable <br>
👎🏻 커다란 네트워크에서는 사용 ❌ <br>
👎🏻 VLSM 지원 불가 <br>

#### ☑️ 로드 밸런싱

로드를 분산해서 보내는 것 <br>

## 2️⃣ IGRP: Interior Gateway Routing Protocol

- Routing Protocol <br>
- Dynamic Routing Protocol <br>
- Interior Gateway Protocol <br>
- Distance Vector protocol <br>
- 90초에 한번씩 라우팅 테이블 업데이트 <br>
- Only sisco routers <br>
- 다양한 요인들을 따져 경로 결정 <br>

### 🆚 RIP

- RIP는 표준 프로토콜, 모든 라우터가 RIP 지원 <br>
- IGRP는 시스코 라우터에서만 사용 가능 <br>
- RIP는 hop 카운트만 따져서 경로 결정 <br>
- IGRP는 5개 요인들을 따져서 경로 결정 <br>
- RIP는 최대 홉 카운트 15개 <br>
- IGRP는 홉 타운트 15개 넘어갈 수 있음 <br>

💡 공통점<br>

- Distance Vector Protocol <br>
- VLSM 지원 불가<br>

### ☑️ IGRP가 경로 결정하는데 고려하는 요소

#### ✔️ Bandwidth 속도(대역폭)

Kbps 속도<br>
최적의 경로 찾기 위해 Bandwidth고려<br>

#### ✔️ Delay 지연

경로를 통해서 도착할 때까지 지연되는 시간<br> <br>

#### ✔️ Reliability 신뢰성

케이블이나 전용선 등 전송 매체 통해 패킷 보냈을 때, 생기는 에러율<br>
목적지까지 제대로 도착한 패킷과 에러가 발생한 패킷의 비율<br>
keepalive: 출발지와 목적지 사이의 신뢰도 측정<br>
keepalive 수치 ⬆️ 신뢰도 ⬆️<br>

#### ✔️ Load 부하, 하중

출발지와 목적지 사이에 얼마나 부하가 생기는가?<br>

#### ✔️ MTU: Maximum Transmission Unit

경로의 최대 전송 유닛 크기, 바이트<br> <br>

### ☑️ IGRP 장단점

👍🏻 5가지 요인을 고려하니 RIP보다 지능적으로 경로 찾음 <br>
👍🏻 홉 카운트 15개 넘어가도 데이터 전송 가능 <br>
👎🏻 VLSM 지원 불가 <br>
👎🏻 sisco 라우터에서만 사용 가능 <br>

## ☑️ Administratice Distance

라우터의 한 쪽은 RIP 프로토콜, 다른 한 쪽은 IGRP를 쓴다면 <br>
라우터는 어떤 경로 정보를 RIP와 IGRP에서 동시에 받음. <br>
그러면 어떤 라우팅 프로토콜에서 온 정보를 이용해서 경로를 찾아야 할까❓ <br>
<br>

정답: **Administratice Distance**값을 보고 디스턴스 값이 더 작은 쪽의 말을 듣는다. <br>
라우팅 프로토콜별로 디스턴스 값을 가지고 있다. <br>
디스턴스 값이 낮으면 낮을수록⬇️ 신뢰성 높다⬆️ <br>
<br>
예를 들어, RIP는 120, IGRP는 100 <br>
따라서 IGRP 프로토콜 말을 들을 것이다. <br>

## 👎🏻 Distance Vector 라우팅 알고리즘의 문제점

- RIP <br>
- IGRP <br>

🆚 Link State <br>

- OSPF <br>

### 👎🏻 문제점: Convergence Time

업데이트가 모든 네트워크에 전달되는 시간(Convergence Time)이 많이 걸린다. <br>
Distance Vector 알고리즘은 업데이트 주기를 가지고 있는데, 이 주기가 지나야 다른 네트워크들은 네트워크에 변화가 생겼다는 것을 인지 <br>

### 👎🏻 문제점: 루핑

#### 루핑 발생 이유

1. 한 라우터가 라우팅 정보에 대한 모든 정보를 가지고 있지 못하고<br>
2. 이웃 라우터로부터 업데이트 Convergence Time 때문에 느리게 이루어져서<br>
   <br>
   네트워크로 향하는 데이터가 뱅글뱅글 돌기만 할 뿐 목적지에 도착하지 못해 네트워크에 엄청난 트래픽 발생<br>

## ✅ Distance Vector 라우팅 알고리즘 해결책

하나의 루핑 방지 방법만 쓰는게 아니라 여러 가지 방식을 적절히 섞어서 활용<br>

### 💡 Maximum hop count

Maximum hop count를 예를 들어 15로 정해놓으면 루핑이 발생하더라도 16까지 이르면 멈추게 된다.<br>
또 flush time지나면 라우팅 테이블에서 아예 경로 삭제<br>
👎🏻 그러나 네트워크 규모가 커지는 경우 15넘어서는 네트워크 경로에 대해서는 아예 도달 못하게 된다는 단점.<br>

### 💡 Hold down timer

Hold down timer가 동작하고 있을 때 외부에서 해당 네트워크에 대한 라우팅 경로가 들어오면<br>
원래 가지고 있던 메트릭 값보다 큰 값이 들어오면 무시해버림 😑<br>
<br>
Hold down timer가 종료되거나<br>
목적지에 대한 새로운 값이 지금 내가 가지고 있는 메트릭과 **같거나 더 좋으면** 업데이트 받아들임. 👌🏻<br>
<br>
Hold down timer사용해서 어떤 경로가 죽었다고 판단되면 이 경로에 대한 상태를 바로 바꾸지 않고 ❌<br>
일정 시간이 지나는 동안 기다렸다가 바꾸겠다.<br>

#### 메트릭 값: 목적지까지의 거리에 대한 값

RIP의 경우 Hop count<br>

### 💡 Split Horizon ⭐️⭐️⭐️

⭐️ 라우팅 정보가 들어온 곳으로는 같은 정보를 내보낼 수 없다.<br>
<br>
⭐️ 다만, 모든 라우팅 업데이트를 내보내지 않는다는 것은 아니고!!! ❌<br>
들어온 정보에 대한 라우팅 정보만 내보내지 않는 다는 것<br>
<br>
⭐️ 만약 하나의 라우터가 어느 네트워크 정보를 인접한 라우터A에게서 받았다면, 그 인접한 라우터A가 네트워크에 더 가까이 있을 것이므로 정보를 다른 라우터들로부터 받을 필요가 없을 것이다.<br>
<br>
⭐️ 두 라우터 간의 루핑만을 막기 위해 만들어진 기술<br>
따라서 전체 라우터 네트워크의 루핑을 Split Horizon이 막을 수는 없다. ❌<br>
라우팅 루프를 자기 라우터랑 붙어있는 인접 라우터에서만 방지 가능<br>

### 💡 Routing Poisoning

다운된 네트워크의 메트릭 값을 먼저 무한대치로 만들어 버려서 사용할 수 없는 값으로 만든다.<br>
대신 라우팅 테이블에서 지워버리지는 않음

### 💡 Poison Reverse

Split Horizon 변형<br>
라우팅 정보를 되돌려보내기는 하되, 이 값을 무한대 값으로 쓴다.<br>
경로 정보를 아주 없애는 것보다 무한대 홉 값을 포함해 라우팅 업데이트를 실시한다면 다른 모든 라우터들은 실수로 잘못된 경로 정보 사용하는 경우 줄일 수 있으므로<br>

## ☑️ VLSM: Variable Length Subnet Mask

IP주소의 효율적 이용을 위해 한 라우터에 접속되는 네트워크마다 서로 다른 서브넷 마스크를 줄 수 있도록 만든 규칙<br>
라우터의 각 인터페이스별로 Subnet Mask가 전부 제각각<br>
이더넷쪽 Subnet Mask와 시리얼쪽 Subnet Mask를 같지 않게 한다.<br>
RIP, IGRP는 VLSM ❌<br>
static routing protocol, EIGRP, OSPF에는 VLSM ⭕️<br>

## ✅ PPS: Packet Per Second

초당 전송하는 패킷 수<br>

- IFG Inter Frame Gap<br>
  프레임과 프레임 사이의 간격<br>
- Preamble Time<br>
  프레임 앞에 붙는 서론 시간<br>

## ✅ DHCP: Dynamic Host Configuration Protocol

PC나 호스트가 자신의 IP주소 가지고 있지 않음 <br>
부팅되면 DHCP서버로부터 하나씩 다이내믹하게 IP주소를 받는다. <br>
👍🏻 IP주소 자동으로 배정 <br>
👍🏻 IP주소 효율적으로 관리 <br>

## 3️⃣ OSPF: Open Shortest Path First

- 표준 라우팅 프로토콜<br>
- 링크스테이트 라우팅 알고리즘<br>

#### 👍🏻 convergence time ⬇️

convergence time: 라우터 간에 서로 변경된 정보를 주고받는데 걸리는 시간 <br>
👍🏻 OSPF는 변화가 생기면 바로바로 전달하기 때문에 훨씬 빠름 <br>
👍🏻 큰 네트워크에 적합 <br>
특히 **area**라는 개념을 사용해 전체 OSPF영역을 작은 영역으로 나누어 관리하여 효율적으로 관리 <br>
🆚 RIP는 convergence time 30초였음 👎🏻 <br>

#### 👍🏻 VLSM 지원

👍🏻 VLSM 지원으로 IP주소 효울적으로 사용 <br>
👍🏻 라우팅 테이블 줄임 <br>
**Route Summurization**: 여러 개의 라우팅 경로를 하나로 묶어준다. <br>
🆚 RIP는 VLSM 지원 못함 👎🏻 <br>

#### 👍🏻 네트워크 크기 ⬆️

홉 카운트 제한 없음 <br>
멀리 떨어진 곳까지 데이터 전달 가능 <br>
🆚 RIP는 홉 카운트 최대 15개 <br>

#### 👍🏻 네트워크 대역폭

네트워크 변화가 있을 때만 정보가 날아가고, <br>
그 정보도 멀티캐스트로 날아가기 떄문에 실용적 <br>
🆚 RIP는 30초마다 브로드캐스트 발생해 네트워크 대역폭 낭비 <br>

#### 👍🏻 경로 결정

많은 요소들을 합쳐서 경로 결정해 정확한 경로 결정 가능 <br>
🆚 RIP는 홉 카운트만 따져서 잘못된 경로 결정 할 때 많음 <br>

### ☑️ Topology

어떤 네트워크 타입에서 적용 가능한가?<br>

#### ✔️ Broadcast Multi Access Topology

네트워크에 2개 이상의 라우터가 연결되는 경우<br>
하나의 메세지를 내보내면 이 네트워크 상에 있는 모든 라우터들이 정보를 받아볼 수 있음<br>
브로드캐스트 능력 있음 ⭕️<br>

- 이더넷 세그먼트<br>

#### ✔️ Point to point Topology

네트워크에 한 쌍의 라우터만 존재<br>

#### ✔️ NBMA: Non Broadcast Multiple Access

네트워크에 2개 이상의 라우터 연결되어 있고<br>
브로드캐스트 능력은 없음 ❌<br>

- 프레임릴레이<br>
- X.25 네트워크<br>

### ☑️ OSPF의 Neighbor

Neighbor: 주위에 있는 OSPF 라우터들<br>
Neighbor관계가 형성되어야 비로소 통신을 시작할 수 있다.<br>
<br>
1️⃣ OSPF 라우터A: Neighbor을 찾기 위해 **Hello 패킷**을 내보낸다.<br>
이 때 각 OSPF를 구분하기 위한 **라우터 ID**도 함께 보낸다.<br>
**멀티캐스트**로 보낸다.<br>
<br>
Hello 패킷은 10초에 한 번씩 발생하고, 이웃이 되기 위해서 꼭 일치해야 하는 정보가 들어있다<br>
헬로 패킷으로 DR, BDR의 주소도 알 수 있음<br>
<br>
⭐️**라우터 ID**를 이용해서 라우터끼리 식별하기 때문에 중요하다.<br>
라우터 ID는 통상 그 라우터의 살아있는 IP주소 중 가장 **높은** IP주소를 사용한다.<br>
<br>
⭐️**Loopback 인터페이스**: IP주소에 상관없이 Loopback주소가 라우터 ID가 된다.<br>
라우터 ID를 쓸 때 IP주소가 게속 죽어서 바뀌는 것에 따라 라우터 ID가 바뀌지 않도록 **고정**하기 위함<br>
<br>
2️⃣ **Init 과정** OSPF 라우터B: OSPF Neighbor A를 Neighbor List에 저장한다.<br>
<br>
3️⃣ OSPF 라우터B가 OSPF 라우터A에게 **유니캐스트**로 나의 정보를 보낸다.<br>
<br>
4️⃣ OSPF 라우터A는 Neighbor로부터 받은 정보를 Neighbor 리스트에 저장한다.<br>

#### ✔️ OSPF의 Neighbor 유의사항

**Hello 패킷 안에 있는 정보** 중 적어도 Neighbor끼리 이것은 **같아야** 이웃으로 인정<br>

- hello/dead intervals<br>
- Area-ID<br>
- password<br>
- Stub area flag<br>

### ☑️ DR, BDR

- Link State공유할 때 트래픽 발생 최소화하기 위해 DR이 관리<br>
- Link State를 Sync(일치성)하기 위해<br>

#### DR: Besignated Router 반장

⭐️**LSU: Link State Update**<br>
각 라우터들이 OSPF에 참여하면 DR, BDR에게 자신의 LSA: Link State Advertisement를 알린다.<br>
목적: 라우터들 각자가 Link State공유하면 트래픽 발생 ⬆️, Link State Sync(일치성) 관리가 어려움<br>
DR은 전달받은 Link State 관리하며 Link State Sync(일치성)상태를 항상 일치시킨다.<br>

#### BDR: Backup Designated Router 부반장

DR이 업무 수행 잘 하는지 관찰<br>

#### ⭐️ Adjacency

모든 라우터가 DR, BDR과 Link State를 Sync(일치성)해야 한다.<br>

#### DR, BDR 선출

DR, BDR은 선거를 통해서 선출<br>
라우터 ID와 라우터의 Priority가지고 선출<br>
아무리 Priority가 높다고 해도 이미 DR, BDR가 선출된 이후에 들어온 라우터는 반장 되지 못함.<br>
라우터들 전부 꺼졌다가 켜졌을 때 DR, BDR될 기회 얻을 수 있음<br>
<br>
❓ 어떤 라우터가 영원히 DR, BDR 되지 못하게 하려면? 라우터의 Priority를 0으로 만든다.<br>
