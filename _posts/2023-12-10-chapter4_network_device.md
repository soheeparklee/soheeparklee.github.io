---
title: CISCO_PART4_네트워크 장비(NIC/Hub/Switch/Bridge/Router/Gateway)
categories: [Computer Science, Network]
tags: [lan, hub, switch, bridge, looping, router]
---

![IMG_13073D626D18-1](https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/77ac6927-691d-4f65-8f04-5a0e6ea5a964)

## 0️⃣ Repeater

> **Amplify** signal over same network before the signal becomes too weak/corrupted

- sinal can become weak due to trasmisison length
- operate at phisical layer

## 1️⃣ 랜카드 NIC

> Network Interface Card(NIC): 랜카드 <br>
> connect computer to network

- installed in the computer to establish a LAN
- operate on datalink layer
- 유저의 데이터를 케이블에 실어서 허브나 스위치, 혹은 라우터 등으로 전달해주고 <br>
- 자신에게 온 데이터를 CPU에게 전달 <br>

#### 랜카드 구분하기

✔️ 어떤 환경에서 사용하는가에 따른 구분 - 대부분 이더넷용 <br>
✔️ PC의 버스(bus)방식에 따른 구분 - 현재는 대부분 PCI방식 - 버스: 컴퓨터에서 데이터가 날아다니는 길 <br>
✔️ 속도에 따른 구분 - 요즘은 1000Mbps 또는 1Gbps용 - 네트워크 상에서 날아다니는 데이터의 양이 많아졌기 때문이다. <br>
✔️ 카드에 접속하는 케이블의 종류 - UTP 타입을 일반적으로 쓰는 추세 <br>

## 2️⃣ 허브

> multi-port-repeater <br>

- connect multiple wires coming from different branches
- cannot filter data
- one hub, one collision domain

허브의 포트 ➡️ 케이블 ➡️ 랜카드에 설치된 PC ➡️ 랜카드에 맥 어드레스 <br>
허브에 연결된 PC끼리 통신이 가능하다. **(쉐어드 허브 방식)** <br>

### 허브 기능

- **multi port** <br>
- **repeater** <br>
  케이블은 전송 거리의 한계가 있음 <br>
  이를 허브 연결을 통해 해결 <br>
  리피터: 중간에서 들어온 데이터를 다른 쪽으로 전달해 주는 역할 <br>

### ⭐️ 쉐이드 허브 방식

> **같은 허브**로 연결된 PC들은 **같은 콜리전 도메인**에 있다. <br>

- 같은 허브로 연결된 PC끼리 통신 가능하다. <br>

## 💥 콜리젼 도메인

한 PC가 데이터 보내고 있는데 또 다른 PC가 데이터 보내려고 하면 콜리젼 발생 <br>
**같은 허브**에 연결되어 있는 모든 PC들은 **같은 콜리젼도메인**에 있다. **(쉐어드 허브 방식)** <br>
🟰 허브에 붙어있는 하나의 PC가 통신을 하게 되면 다른 모든 PC는 통신을 중단해야 한다. <br>
허브에 붙은 PC의 수 ⬆️ 콜리전 도메인의 크기 ⬆️ <br>
콜리전 도메인을 나누는 방식으로는 **스위치**와 **브리지**가 있음. <br>

## 3️⃣ 허브의 한계

### 쉐어드 허브 방식의 한계

허브에 연결된 PC의 수가 많아질수록 콜리젼 도메인도 더 많이 발생. <br>
아무리 랜카드, 허브 속도, 케이블 속도를 올리더라도 또 그만큼 PC가 많이 연결된다면 그대로 <br>
콜리전 도메인이 너무 커지게되면 속도 👎🏻 <br>

## 4️⃣ 허브의 종류

- active hub: used to extend maximum distance between node
- passive hub: collect wiring from nodes, relay singnals onto network
- intelligent hub

### 인텔리전트 허브

- 관리 기능을 제공 <br>
- NMS(네트워크 관리 시스템)을 통해서 관리 <br>
- NMS통해서 모든 데이터 분석, 제어도 가능 <br>
- 멀리서도 허브의 동작 감시, 조정 <br>

### Auto Partition

  <br>
만약 한 🖥️가 고장이 나서 계속 이상한 데이터를 끊임없이 보낸다!  <br>
그러면 그 PC랑 같은 허브로 연결된 PC들은 모두 통신이 불가능한 상태가 되어 버림. (이더넷의 CSMA/CD 프로토콜)  <br>
이 때 ✨인텔리전트 허브✨는 이런 문제의 PC를 자동으로 Isolation 해 버린다. "너 문제되니까 방출"  <br>
그러면 그 PC는 통신을 못 하게 되겠지만 나머지 PC들은 정상적인 통신 가능~  <br>
또 분리된 PC는 램프로 표시되기 때문에 어떤 PC인지 알고 조치를 취할 수 있음  <br>

### 세미 더미 허브

더미 허브 안에 인텔리전트 허브와 연결하면 자기도 인텔리전트 허브가 됨 <br>

### stackable 허브

  <br>
스택을 위해 케이블로 연결될 수 있는 허브  <br>

### ✅ stackable 스위치/ 허브

서로 간의 연결이 훨씬 효울적으로 설게되어 있음 <br>

- **Backplane**: (장비 간 데이터 전송을 위해 연결된 일종의 고속도로)가 훨씬 빨라짐 <br>
- 연결된 장비 중 하나가 고장나도 다른 장비에 영향을 주지 않음 <br>
- 혼자 있는 것보다 여러 대가 스택으로 연결되면 훨씬 더 좋은 성능 발휘 <br>
- NMS 네트워크 관리 시스템을 이용했을 때도 전체 스택 장비들을 한 대의 장비처럼(IP주소 하나로) 관리 가능 <br>

🆚 반대되는 개념은 **standalone** <br>
작은 규모일떄는 standalone 쓰는 것이 합리적 <br>

## 6️⃣ 브리지

- repeater ➕ filter content by reading **MAC adderss** of the source, destination
- connect two LANs on same protocol
- operate at datalink layer

브리지가 스위치의 원조격 <br>
브리지는 허브로 만들어진 **콜리전 도메인 사이를 반으로 나누고** 중간에서 다리 역할 <br>
중간에 서서 **브리지 테이블**을 보면서 통신이 다리 한쪽에서만 이루어지면 다리를 못 건너가게 하고, 통신이 다리를 건너야 하면 그 때만 다리를 건너게 해 준다. <br>
이렇게 **콜리전 도메인을 나누어** 놓는다. <br>

## 5️⃣ 스위치 Switched Ethernet

- multiport bridge
- operate at datalink layer
- error checking, does not forward packets with error
  Shared Ethernet방식인 허브의 한계를 보완 <br>
  스위치는 브리지에서 출발하여 기능을 더한 것 <br>

스위치는 **포트별로 콜리전 도메인이 나뉘어져 있다.** <br>
허브: 1,2번 PC가 통신중이면 3번은 기다려야 함. <br>
스위치: 3번도 동시에 통신 가능, 콜리전 도메인을 나눠주었기 때문. <br>

### ✔️ 스위치의 기능

1. 콜리전 문제 해결 <br>
2. 허브에 비해 데이터를 처리하는 방법이 우수하다 <br>
3. 데이터의 전송 에러 복구 <br>

### ✔️ 스위치 종류

switches can operate at different OSI levels <br>
<br>

**Layer 2 Swtich(L2 Switch)** <br>

- operate at datalink layer
- use **MAC address**
- forward data between same network
- LANs

**Layer 3 Swtich(L3 Switch)** <br>

- operate at network layer
- switching ➕ routing
- use **IP address**
- route data between **different subnet**
- routing table
- bigger network that L2 switch

**Layer 7 Swtich(L7 Switch)** <br>

- operate at application layer
- forward data based on **application data**(HTTP request, FTP request, email header)
- load balancing, content filtering, firewalls, deep packet inspection

## 7️⃣ 브리지/스위치의 기능

✔️ **learning** <br>
무엇을? 맥 어드레스 <br>
브리지나 스위치는 **출발지의 맥 어드레스**를 읽어서 자신의 **브리지 테이블**에 저장 <br>
<br>

✔️ **flooding** <br>
이 맥 어드레스 주소 처음 보는데? 나의 브리지 테이블에 없어. ➡️ flooding <br>
한 번도 통신을 해 보지 않은 주소라서 브리지가 출발지 주소를 learning하지 못했음 <br>
출발지를 제외한 나머지 포트로 뿌림 <br>
들어온 포트를 빼고 모든 포트로 프레임을 뿌림 <br>

➡️ broadcast, multicast일 때도 flooding발생 <br>
<br>

✔️ **forwarding** <br>
목적지의 맥 어드레스를 자신의 브리지 테이블에 가지고 있음! <br>
그런데 다리를 건너야 함(다른 세그먼트에 있음) <br>
해당 포트쪽으로만 프레임을 뿌리는데, 그 포트가 다리 넘어에 있음 <br>
<br>

✔️ **filtering** <br>
filtering이 바로 **콜리젼 도메인을 나눠주는 기능** <br>
목적지의 맥 어드레스를 자신의 브리지 테이블에 가지고 있음! <br>
그리고 그 목적지는 브리지를 넘어갈 필요가 없음. <br>
출발지와 목적지가 같은 세그먼트에 있다는 뜻이다. <br>
브리지를 건너가지 않아도 통신이 일어날 수 있으니 다리를 막는다. <br>
💡 브리지의 필터링 기능 덕분에 양쪽 세그먼트에서 동시에 통신이 가능한 것. <br>
<br>

✔️ **aging** <br>
브리지는 춟발지의 맥 어드레스를 자신의 브리지 테이블에 저장하는데, 평생 기억할 수는 없음. <br>
일정 시간(5분)이 지나면 맥 어드레스 정보를 브리지 테이블에서 지움. <br>
그래야지 또 새로운 맥 어드레스를 기억하니까. <br>
<br>

✔️ **aging reflash** <br>
만약 브리지 테이블에서 맥 어드레스 지우기 전에 또 통신을 했다면? <br>
aging타이머가 끝나기 전에 같은 출발지를 가진 녀석이 또 브리지로 들어오면 브리지는 타이머 리셋, 처름부터 다시 카운트 <br>

## 브리지 🆚 스위치

브리지, 스위치는 허브보다 한 수 위의 장비 <br>
공통점: 콜리전 도메인을 나누어 주는 역할을 한다. <br>

**1. 처리 방식 차이** <br>

🌉 브리지: 소프트웨어 방식, 느림 <br>
🎛️ 스위치: **하드웨어 방식, 빠름** <br>
ASIC: Application Specific Integrated Circuit 미리 칩에 구워서 하드웨어 방식으로 만듦. <br>

**2. 포트 속도 차이** <br>

🌉 브리지: 모든 포트 같은 속도 <br>
🎛️ 스위치: 포트마다 다른 속도 지원 가능, 서로 다른 속도 연결 가능 <br>

**3. 포트 수 차이** <br>

🌉 브리지: 적음 <br>
🎛️ 스위치: 많음 <br>

**4. 프레임을 처리하는 방식 차이** <br>

🌉 브리지: store and foward <br>
🎛️ 스위치: store and foward && cut-through <br>

## ☑️ 브리지, 스위치의 프레임을 처리하는 방식

#### ✔️ store and foward: 에러 복구 능력

스위치나 브리지는 일단 들어온 프레임 다 받음 <br>
전체 프레임이 다 들어올 떄까지 기다렸다가... <br>
프레임이 다 들어왔는지, 에러는 없는지, 출발지 주소, 목적지 주소 확인 <br>
에러 발견하면 프레임 버리고 재전송 요구 <br>
**에러 복구 능력** 👍🏻 <br>

#### ✔️ cut-through: 빠름

처음 48비트만 확인하고 목적지 확인해 프레임을 목적지로 전송해 버림. <br>
에러 찾아내기 어려움 <br>

#### ✔️ fragment free

처음 512비트까지 확인함. <br>
에러 감지 능력이 컷스루에 비해서는 우수 <br>

## 8️⃣ Looping 뺑뻉이

### 루핑:

스위치나 브리지에 목적지까지의 경로가 두 개 이상 존재하면 프레임이 빙빙 도는 루핑 발생 <br>
루핑이 발생하면 다른 PC들은 데이터를 보낼 수가 없음 <br>

### 스패닝 트리 알고리즘:

루핑 막는 알고리즘 <br>
MST <https://soheeparklee.github.io/posts/DS-mst/> <br>

## ☑️ Fault Tolerant, Load Balancing

### ✔️ Fault Tolerant

네트워크 상에 어떤 문제가 발생했을 때를 대비해 장애 대비를 해 두는 것 <br>
라우터를 두 대 연결해 두어 한 대가 죽었을 때 대비하기 <br>

### ✔️ Load Balancing

로드를 분산한다.
두 개의 인터넷 회선을 사용해 속도 2배, 동시에 폴트 톨러런트 <br>
대부분의 로드 밸런싱은 폴트 톨러런트가 가능하나, 폴트 톨러런트는 로드 발랜싱이 안 되는 경우도 있음. <br>

## 9️⃣ Spanning Tree Algorithm 스패닝 트리 알고리즘

루핑을 미리 막기 위해 두 개 이상의 경로가 발생하면 하나를 제외하고 나머지 경로를 자동으로 막아 두었다가 <br>
기존 경로에 문제가 생기면 막아놓은 경로를 풀어 데이터 전송 <br>

### 시스코의 이더 채널

여러 개의 링크가 마치 하나의 링크처럼 인식되게 한다. <br>

## 🔟 라우터의 기능

> **Router** <br>
>
> > connect different network, manage traffic <br>
> > route data between network based on IP address <br>
> > 👮🏻 direct data packet to the right destination <br>

- operate at Network Layer

**라우터의 기능**

- 브로드캐스트 도메인 나누기
  - 스위칭이 콜리전 도메인을 나눴다면, 라우팅은 **브로드캐스트 도메인**을 나눈다. <br>
- 라우터로 브로드캐스트 도메인을 나눠주지 않으면 한 번의 브로드캐스트가 모든 영역에 영향을 준다. <br>
- 패킷 피터링 기능(보안 기능)
- 불필요한 트래픽 전송 막기
- 로드 분배
- Quality Of Service
  - 프로토콜, 데이터 크기, 중요도 등 상황에 따라 트래픽의 전송 순서 조절

### Router 🆚 Switch

**Switch** <br>

- used within single network to connect devices(computer/printer/server)
- enables these devices to communicate with each other
- Layer 2(DataLink Layer)

## ✅ Gateway

> passage to connect two networks <br>
> networks that work upon different networking models <br>

- take data from one system -> interprete -> transfer to another system
- also called protocol converters
