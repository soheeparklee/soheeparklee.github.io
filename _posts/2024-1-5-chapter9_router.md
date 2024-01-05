---
title: PART9_Router
categories: [Computer Science, CISCO networking]
tags: [cs, router]
---

## 1️⃣ Access List

네트워크에 접근을 하게 해 줄지, 말지를 정해놓은 리스트 <br>
즉, 라우터의 문지기<br>
만약 접근 불가라고 판단되면? Access List가 **Host Unreachable**이라는 메세지를 띄운다.<br>
목적: 보안<br>

**종류**<br>

- 스탠더드 액세스 리스트
- 익스텐디드 액세스 리스트

## 2️⃣ Access List 4대 규칙

### 1. 액세스 리스트는 윗줄부터 하나씩 차례대로 수행된다.

맨 윗줄부터 그 다음 줄, 그 다음 줄 차례대로 수행<br>

### 2. 액세스 리스트의 맨 마지막에는 deny all 생략되어 있음

액세스 리스트의 맨 마지막 Line에 permit any를 넣지 않은 경우는 defualt, 어느 액세스 리스트와도 매치되지 않은 나머지 address는 deny<br>
<br>
액세스 리스트의 맨 마지막 줄: deny all 다 막아버린다.<br>
따라서 어떤 주소가 내가 가진 액세스 리스트의 항목에도 어떤 해당하지 않는다면 맨 마지막 줄까지 내려온 후 deny all<br>
(액세스 리스트는 정의되어 있는데, 자기가 속할 액세스 리스트가 없는 것)<br>

### 3. 액세스 리스트의 새로운 line은 항상 맨 마지막으로 추가되며, 액세스 리스트 line의 선택적 추가나 제거는 불가능

액세스 리스트 중간에 **선택적 추가(selective add)**<br>
또는 **제거(remove)**는 불가능하다.<br>
액세스 리스트의 중간에 있는 Line을 지우려고 하면 액세스 리스트 다 지워짐!<br>

### 4. interface에 대한 액세스 리스트가 정의되어 있지 않은 경우에는 permit any

인터페이스에 액세스 리스트 명령 없으면 permit any<br>
<br>
즉, interface에 access group 명령이 들어있지 않은 경우<br>
액세스 리스트가 정의되어 있지 않은 인터페이스는 액세스 리스트를 거치지 않고 바로 통과 **permit any**<br>
(아예 액세스 리스트 **정의조차 안 됨**)<br>

## 3️⃣ Congestion 혼잡

네트워크의 전체 대역폭(Bandwidth)보다 그 네트워크를 지나는 데이터가 많이 몰리게 된 경우<br>

#### 💥**Bustry(버스티) 트래픽**:

데이터가 갑자기 폭주하는 것<br>

#### 🚥 **Congestion Management**:

네트워크 혼잡을 해결<br>

1. 사용자와 애플레케이션에 대한 필터링<br>
   모든 사용자, 모든 애플리케이션이 통과하면 네트워크 트래픽이 너무 증가하니까 골라서 통과시킨다.<br>
   이것을 위해 **액세스 리스트** 사용<br>
2. 브로드캐스트 막아주기<br>
3. 타이머 맞추기<br>
   일정 시간마다 한 번씩 일어나는 일을 조정하기(일어나는 주기 시간을 늘린다든지)<br>
4. 라우팅 테이블 관리<br>
   라우팅 정보 교환 너무 자주 하지 않도록, 일부를 스태틱으로 조정<br>
5. 트래픽의 우선 순위 매기기<br>

## ☑️ Standard Access List

출입 통제를 할 때 출발지 주소 **(Source Address)**만 참고한다.<br>
인터페이스에 액세스 리스트 없다면 ➡️ permit all<br>
인터페이스에 액세스 리스트 있다면 ➡️ 패킷의 출발지 주소 비교<br>
액세스 리스트에 정의된 주소와 패킷의 출발지 주소 일치 ➡️ 액세스 리스트 수행<br>
<br>
스탠더드 액세스 리스트의 위치는 Destination Router, 항상 목적지에 제일 가까운 라우터에 적용한다.<br>

## 4️⃣ VTY PORT의 액세스 리스트

텔넷 접속을 하는 사용자 제어 위함<br>
텔넷을 한다 🟰 Virtual Terminal 포트로 접속한다.<br>

## ☑️ Extended Access List

출발지, 목적지, 프로토콜, 사용 번호 등 다양한 것을 고려한 후 통과 여부를 결정한다.<br>
<br>
인터페이스에 액세스 리스트 없다면 ➡️ permit all<br>
인터페이스에 액세스 리스트 있다면 ➡️ 패킷의 출발지 주소, 목적지 주소, 프로토콜 등 관리하는 항목 여러가지 비교<br>
따라서 Extended Access List가 Standard Access List보다 정교한 액세스 제어 가능<br>

### Standard Access List 🆚 Extended Access List

Standard Access List: 출발지 주소(Source Address)만 제어<br>
Extended Access List: 출발지, 목적지 주소(Destination Address) **모두** 제어<br>
Standard Access List: TCP/IP에 대한 제어만<br>
Extended Access List: ip/tcp/udp/icmp등 **특정 프로토콜 지정**해서 제어 가능<br>
Standard Access List: 1~99까지 번호를 access list 번호로 사용<br>
Extended Access List: **100~199**까지 번호를 access list 번호로 사용<br>

## 5️⃣ HSPR: Hot Standby Routing Protocol

시스코 장비에서만 사용<br>
라우터가 고장났을 때 대비해 라우터 한 대를 구성에 더 포함시키고,<br>
라우터가 고장나면 자동으로 두 번째 라우터가 작동하도록 하는 것<br>
<br>
HSPR는 실제 존재하지 않는 가상의 라우터 IP주소를 디폴트 게이트웨이로 세팅한 후,<br>
그 주소에 대해 Active, Standby 라우터를 각각 둔다.<br>
Active 라우터가 즈 주소의 역할을 대신 수행하다가 💥 문제 생기면<br>
Standby 라우터가 Active 라우터의 역할을 대신한다.<br>
만약 Active 라우터가 다시 살아나면 Standby 라우터는 다시 스탠바이로 복귀<br>
따라서 디폴트 게이트웨이를 고치지 않아도 항상 인터넷 접속 가능<br>

## 6️⃣ NAT: Network Address Translation

한쪽 네트워크의 IP주소가 다른 네트워크로 넘어갈 때 변환이 되어서 넘어가는 것<br>
Inside Local주소를 Inside Global 주소로 바꾸어주는 과정<br>

### ❓ 왜 NAT이 필요한가?

- 내부의 네트워크에는 비공인 IP주소를 사용하고, 외부 인터넷으로 나가는 경우에만 공인 IP주소 사용<br>
- 기존에 사용하던 ISP에서 새로운 ISP로 바꾸면서 내부의 전체 IP를 바꾸지 않고 기존의 IP주소를 그대로 사용하고자 하는 경우<br>
- 2개의 인트라넷을 서로 합치다보니 두 네트워크의 IP가 겹치는 경우<br>
- TCP 로드 분배가 필요한 경우

## ✔️ wildcard mask

OSPF 라우팅 프로토콜을 사용할 때나, 지금처럼 액세스 리스트 사용할 때 사용되는 일종의 마스크<br>
서브넷 마스크가 무엇을 하면 그 반대로 한다.<br>
