---
title: PART7_Router
categories: [Computer Science, CISCO networking]
tags: [cs]
---

## 1️⃣ Router

- 지능을 가진 경로 배정기 <br>
  가야할 주소가 주어진다면 자신이 가야할 길을 자동으로 찾아가는 능력을 가진 기기 <br>

### ✅ 라우터의 기능

#### 1. Path Determination 경로결정

데이터 패킷이 목적지까지 갈 수 있는 길을 검사하고 어떤 길로 가는 것이 가장 적절한지 결정 <br>
이를 위해 라우팅 알고리즘(라우터 프로토콜) 사용 <br>
라우터 프로토콜은 라우팅 테이블 만들어 관리 <br>

#### 2. Switching 스위칭

그 길이 결정되면 그쪽으로 데이터 패키지 스위칭 <br>

### ✅ 인터페이스

라우터에 나와있는 접속 가능한 포트 <br>
<br>

- 이더넷: 내부 네트워크와 접속(내부 허브, 스위치) LAN과 연결 <br>
- TP: 케이블 <br>
- 시리얼(Serial): WAN과 접속(외부 네트워크) <br>
- DSU: 전용선용 모뎀 <br>

## 2️⃣ AS, ASBR, IGP, EGP

AS안에 있는 라우터들은 AS에 속해 있는 라우터에 대한 정보만 가지고 있다가 <br>
AS안에서는 IGP사용하다가, AS밖으로 나갈 때는 AS안에 있는 ASBR에게 정보를 물어봐서 EGP로 서로 라우팅 정보를 주고받는다. <br>

#### ✔️ AS: Autonamous System

하나의 네트워크 관리자에 의해서 관리되는 라우터의 집단 <br>
하나의 관리 규정 아래서 운용되는 라우터의 집단 <br>

#### ✔️ ASBR: Autonamous System Boundary Router

문지기 라우터 <br>

#### ✔️ IGP: Interior Gateway/ Routing Protocol

- **RIP**(Routing Information Protocol) <br>
- **IGRP**(Interior Gateway Routing Protocol) <br>
  AS 내부에서 사용하는 라우팅 프로토콜 <br>
- **OSPF**(Open Shortest Path First) <br>
- **EIGRP** <br>

#### ✔️ EGP: Exterior Gateway/ Routing Protocol

- **BGP**
  AS 외부에서 사용하는 라우팅 프로토콜 <br>

## 3️⃣ 라우팅 테이블

⭐️ 라우팅 테이블: 라우터가 경로를 찾을 때 사용하는 지도 <br>
라우팅 테이블에 목적지와 목적지로 가려면 어느 인터페이로 가야 하는지 적어둠 <br>
라우터는 항상 최적의 경로를 찾아 이것을 라우팅 테이블에 저장 <br>
✔️ 라우팅 테이블은 사용하는 **라우터 프로토콜**에 따라 달라짐 <br>
✔️ 라우팅 테이블은 RAM위에 올라가기 때문에 전원이 꺼지면 초기화 <br>
`show up route` <br>
<br>
자신이 찾아갈 경로에 대한 정보를 라우팅 테이블에 기억 <br>
일종의 메모리 <br>
계속 업데이트함 <br>
<br>

- 목적지 <br>
- 목적지까지의 거리 <br>
- 어떻게 갈 것인가 등 저장 <br>

## 4️⃣ Routing Protocol

### 🆚 라우티드 프로토콜

라우팅을 당한 <br>
라우터가 라우팅을 해 준 고객 <br>

### 라우팅 프로토콜 🟰 라우팅 알고리즘

프로토콜들에게 목적지까지 가장 좋은 길을 안내 <br>
**라우팅 알고리즘**은 **라우팅 프로토콜을 조건으로** 목적지까지 가장 빠르고 안전한 길을 찾아냄 <br>

### 💡 라우팅 프로토콜 분류 1

라우팅 프로토콜 분류 1 기준: **누가 경로를 정해주는가** <br>

#### ✅ Static Routing Protocol

사람이 정해준 경로만을 간다. <br>
👍🏻 라우터가 할 일은 줄어 속도⬆️ 메모리 ⬇️ <br>
👎🏻 사람이 일일이 구성해 줘야 하는 단점 <br>
👎🏻 정해진 길에 문제가 생겨도 사람이 수정해주기 전까지는 문제가 해결되지 않음 <br>

#### ✅ Dynamic Routing Protocol

👍🏻 라우터가 알아서 길을 찾음 <br>
👎🏻 라우터가 할 일이 많음 <br>

### 💡 라우팅 프로토콜 분류 2

라우팅 프로토콜 분류 2 기준: **라우팅 테이블 관리 방법** <br>

### ✅ Distance Vector

Distance(거리), Vector(방향)만을 위주로 만들어진 라우팅 알고리즘 <br>
목적지까지의 모든 경로 저장 ❌ <br>
목적지까지의 **거리(홉 카운트)**, 목적지까지 가려면 어떤 **인접 라우터(Neighbor Router)** 거칠지 **방향**만 저장 <br>
<br>
👍🏻 메모리 절약(모든 경로 저장 안하니까) <br>
👍🏻 구성이 간단 <br>
👎🏻 라우팅 테이블에 변화 없어도 무조건 업데이트 해야해 트래픽 낭비 <br>
👎🏻 Convergence Time: 라우팅 테이블에 변화 있으면 이를 알아차리는 시간(Convergence Time) 오래걸림 <br>
👎🏻 RIP 경우는 시간 오래걸림, 최대 홉 카운트 15넘지 않음, 라우터 15개 넘으면 인식 못함 <br>
➡️ 작은 규모 네트워크에 적합 <br>
<br>

- **RIP**(Routing Information Protocol) <br>
- **IGRP**(Interior Gateway Routing Protocol) <br>

### ✅ Link State

한 라우터가 목적지까지 모든 경로 다 저장 <br>
**토플러지 데이터베이스**에 모든 경로 정보 저장 <br>
이 토플러리 데이터베이스 가지고 **SPF(Shortest Path First)**라는 알고리즘 계산 <br>
**SPF 트리**: 출발지에서 목적지까지를 나뭇가지처럼 펼쳐놓은 뒤 가장 빠른 경로 찾기 <br>
👍🏻 목적지까지 모든 경로 아니까 중간에 링크의 변화가 생겨도 금방 알아낼 수 있다. <br>
👍🏻 라우터 간 라우팅 테이블 교환 적게 발생 <br>
👍🏻 라우팅 테이블 교환할 때도 테이블에 변화가 있는 부분만 교환해 트래픽 발생 ⬇️ <br>
👎🏻 메모리 소모 ⬆️ <br>
👎🏻 SPF 트리 걔선허누러 라우터 CPU 일 ⬆️ <br>
➡️ 커다란 네트워크의 고용량 라우터 <br>
<br>

- **OSPF**(Open Shortest Path First) <br>

## ☑️ SPF(Shortest Path First) 알고리즘

각 라우터들은 공통의 Link-State Database로부터 자신을 루트로 하는 각각의 트리 구성 <br>
이 트리로부터 routing table구성 <br>
routing table로부터 목적지까지의 경로 구성 <br>

## 5️⃣ 라우터 구성

#### ✔️ Console Cable

맨 처음 라우터 구성할 때 사용 <br>

#### ✔️ 모뎀 AUX

원격지에서 라우터 조정 다능 <br>
Auxilary Port에 모뎀 연결 <br>

#### ✔️ Telnet

일단 IP주소가 세팅된 다음에 네트워크 통해서 접속 <br>

#### ✔️ 네트워크 관리 시스템 NMS

#### ✔️ TFTP 서버

미리 구성된 파일을 저장했다가 나중에 라우터로 다운로드 <br>

## 6️⃣ 라우터 모드

#### ✔️ 유저 모드

라우터의 현재 상태 볼 수 있으나 <br>
라우터의 구성 파일을 보거나 구성을 바꿀 수 없음 <br>

#### ✔️ Previlaged Mode 운영자 모드

라우터에게 명령 가능 <br>
유저 모드는 명령의 제한이 있었다면, 운영자 모드는 없음 <br>
`enable`해서 유저 모드에서 운영자 모드로 들어온다. <br>

#### ✔️ Congig Mode 구성 모드

라우터의 구성 파일을 변경하는 경우 <br>
만들어야 할 모든 구성 파일을 만듦. <br>
오직 **운영자 모드**에서만 구성 모드로 들어갈 수 있다. <br>
구성모드에서 명령이 효과를 발휘하는 시점은 명령 줄을 입력하자마자 <br>

#### ✔️ 셋업 모드

처음 부팅할 때 자동으로 셋업 모드 <br>
라우터에 어떤 구성 파일도 저장되어 있지 않을 떄 라우터가 이를 인식하고 자동으로 들어가는 모드 <br>
질문과 답변을 통해서 라우터가 자동으로 구성 파일 만든다. <br>

#### ✔️ RXBOOT 모드

문제 발생시 복구용 <br>

## 7️⃣ 라우터 내부 구성

#### ☑️ RAM

volatile(전원 꺼지면 정보 날아감?) ⭕️ <br>
라우터의 프로그램들이 올라오는 **무대** <br>
RAM위로 운영 체제, 구성파일, 라우팅 테이블 등이 올라와 실제 라우터를 움직인다. <br>
✔️ 라우팅 테이블 (백업X, 일시적 보관, 전원 꺼지면 다 지워지니까) <br>

#### ☑️ NVRAM(Non Volatile)

✔️ 라우터의 구성 파일 configuration file 저장 <br>
volatile ❌ <br>

#### ☑️ Flash Memory

✔️ IOS Internetwork Operating System 저장 <br>
✔️ 특히 IOS이미지 <br>
NVRAM에 비해 Flash Memory가 용량이 크다. <br>
volatile ❌ <br>

#### ☑️ ROM

✔️ 라우터의 가장 기본적인 내용 저장 <br>

#### ☑️ 인터페이스

#### ☑️ 콘솔 포트

#### ☑️ Auxilary Port

## Static Routing 🆚 Defualt Routing으로 라우터 구성하기

### Static Routing

갈 수 있는 경로가 하나밖에 없을 떄(연결된 라우터가 1개) Stub 라우터용으로 많이 사용x <br>
특정 목적지로 가기 위한 구성 <br>
Stub 네트워크: 오직 하나의 경로만을 통해서 외부 망과 연결된 네트워크, 이 때 Static Routing이 적합하다. <br>

### Defualt Routing

경로를 찾아내지 못한 네트워크는 모두 이곳으로 가라고 미리 정해놓기 <br>
특정 목적지를 정해놓지 않고 그냥 모든 목적지가 디폴트로 지정한 곳으로 간다는 차이가 있다. <br>
디폴트 라우터를 만들 <br>
<br>

- 인터넷을 사용하는 라우터 <br>
- Stub 네트워크에 있는 라우터 <br>

## 8️⃣ 라우터의 패스워드 구성

### ✔️ enable password

라우터의 유저 모드에서 previleged mode로 들어가기 위해 필요한 password <br>
패스워드가 라우터의 구성 파일에서 그대로 보임 <br>

### ✔️ enable secret

라우터의 유저 모드에서 previleged mode로 들어가기 위해 필요한 password <br>
자동으로 암호화가 되어 구성 파일에서 안보임 <br>
enable password과 enable secret 둘다 있으면 enable secret만 물어봄 <br>

### ✔️ 콘솔, Virtual Terminal(텔넷 접속), AUX 포트 패스원드

콘솔, Virtual Terminal포트에 타임아웃 걸어서 사용 안하는 포트는 끊어줄 수도 있음 <br>

## 9️⃣ CDP Cisco Discovery Protocol

CDP: Cisco 라우터와 스위치에서 직접 연결된 시스코 장비 찾아내는 기능 <br>
(다른 장비 통해서 연결된 장비는 못 찾음) <br>
CDP는 Data Link 계층에 올라가는 프로토콜 <br>
멀티캐스트 사용해서 시스코 장비 찾아냄 <br>

## 🔟 Ping, Trace

라우터 구성 후 네트워크 연결에 이상 없는지 테스트 <br>
출발지에서 목적지까지 연결에 이상 없는지 <br>
문제 있다면 어디에서 발생했는지 <br>
문제 없으면 **느낌표!** 문제 있으면 **점.** <br>

### ✅ Ping

단순형 핑: 목적지 주소는 바꿔도 출발지 주소는 랑상 라우터를 떠나는 인터페이스로 설정됨 <br>
확장형 핑: 에코 패킷의 출발지 지정 가능, 에코 패킷의 크기 변경 가능, 핑을 몇 번 보낼지도 설정 가능 <br>
확장형 핑 사용하면 출발지 주소 변경 가능 <br>

### ✅ Trace

출발지에서 목적지뿐만 아니라 중간에 거친 경로에 대한 정보와 소요 시간까지도 확인 <br>
목적지까지 경로 한하나 분석해 줌 <br>

#### TTL(Time To Live)

라우터 하나를 거칠 떄마다 1씩 감소해서 0이 되면 패킷 버리며 에러 발생 <br>
TTL이란 값을 하나씩 증가시키면서 돌아오는 에러 메세지를 가지고 경로 확인 <br>
무한히 루핑 도는 현상 막기 위해 TTL사용 <br>
