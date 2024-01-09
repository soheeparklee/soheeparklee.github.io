---
title: TCP/IP Protocol
categories: [Computer Science, Network]
tags: [cs, network, supercoding] # TAG names should always be lowercase
---

## ✅ 네트워크

둘 이상의 컴퓨터/장치/물질이 서로 **정보를 주고받는** 구조 <br>

#### ☑️ LAN WAN ISP

인터 네트워킹<br>
➖ LAN: 자기만의 구역에서 연결 <br>
➖ WAN: 구역끼리 라우터로 연결, 인터넷 <br>
➖ 인터넷: 각 국가 WAN을 인터네트워킹 한 것 <br>
➖ ISP: Internet Service Provider로부터 인터넷 제공받는다. <br>

#### ☑️ WWW

WWW: 전세계에 인터넷 보급하는데 핵심 역할 <br>
web: 인터넷을 통해 사람들과 정보를 공유하는 공간 <br>
인터넷에서는 WWW(웹) 이외에도 많은 것들이 돌아간다. <br>

## ✅ 패킷

#### ☑️ 회선 교환방식

정보를 전달하는 동안 계속해서 회선을 점유하는 방식<br>
**회선을 이용한 정보 전달의 한계:** 회선을 점유하니 이미 연결중인 장치는 또 다른 장치와 연결을 할 수가 없음.<br>

#### ☑️ 패킷 교환방식

주고받는 정보를 '패킷'이라고 하는 작은 소포로 만들어 나누어 전송하기 <br>
컴퓨터가 한 번에 여러 패킷 수진, 전송 가능 <br>

#### ☑️ 패킷 구조

**Header + Body**
<img width="744" alt="스크린샷 2024-01-06 오후 3 38 43" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/e439e1d8-5eac-4126-814b-c33278f49a4d">

- Header: 프로토콜, mac address, IP address, Port <br>
  ➖ mac address: 네트워크 이용하는 장비의 고유 식별자(주소) <br>
  ➖ IP address: 인터넷, 로컬 네트워크에서 장치들의 식별자(주소) <br>
  ➖ Port: 네트워크 포트는 네트워크 장치의 데이터를 주고받는 통로, 특정 프로세스와 통신하는데 사용되는 번호 <br>
- Body: 보내고자 하는 정보가 작은 단위로 나뉘어 저장되어 있음 <br>
  ➖ body protocol안에 HTTP 들어있음 ⬅️ 개발자가 이것을 바꿈 <br>

## ✅ 소켓 프로그래밍

IP address + port + HTTP(프로토콜) 생성 <br>
프로세스에세 HTTP 정보 통로를 열어둔다. <br>

## ✅ TCP/IP 프로토콜

#### ☑️ 프로토콜

프로토콜: 둘 이상의 장치가 정보전달 시 **의사소통하는 규칙과 규약 집합** <br>
컴퓨터 네트워크에서 **패킷 생성/전송/해석/처리** 관련 규칙과 규약 집합 <br>

- UTP 포로토콜: 게임<br>
- SMTP 프로토콜: 이메일<br>

#### ☑️ TCP/IP 프로토콜

<img width="753" alt="스크린샷 2024-01-06 오후 3 49 29" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/b4d34997-0113-431f-b177-63bd2248df8a">

### ⭐️ Network Interface

가장 기계에 가까움<br>
물리적 프로토콜<br>
컴퓨터의 **물리적** 네트워크 연결<br>
✔️ 와이파이<br>
✔️ 전선<br>
✔️ Ethernet<br>

### ⭐️ Internet Layer

네트워크 주소 기반 데이터 전송<br>
IP version에 대한 정보 저장<br>
✔️ IP version<br>
✔️ NCP(IP이전에 사용하던 주소)<br>

### ⭐️ Transport Layer

데이터의 안정적인 전송을 담당,<br>
포트 번호를 사용하여 통신을 제공한다.<br>
데이터를 어떻게 전달할 것인지<br>

**주요 프로토콜**
✔️ TCP<br>
✔️ UDP<br>

### ⭐️ Application Layer

데이터를 어떻게 해석할 것인가 <br>
많은 종류의 프로토콜이 있음 <br>
➖ TCP <br>
✔️ HTTP <br>
✔️ SMTP <br>
✔️ Telnet <br>
<br>
➖ TCP<br>
✔️ DMS<br>
✔️ RTSP<br>
✔️ RTP<br>

<img width="750" alt="스크린샷 2024-01-06 오후 3 50 00" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/483faafc-08be-4400-a76f-7d3606e58a1e">

### 💡 애플리케이션 프로토콜 선택

속도, 신뢰성 고려해서 **TCP/UDP** 선택<br>
네트워크 모델 고려해서 **서버 클라이언트/ P2P/ 중앙 집중 구조** 중 선택<br>
보안성 강한 HTTPS 골라도 좋음<br>

<img width="824" alt="스크린샷 2024-01-06 오후 5 58 08" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/2386982e-10dc-46d7-9117-41f473cb3a68">

## 🆚 TCP, UDP

### ☑️ TCP: Transmission Control Protocol

예의바른 프로토콜<br>
"데이터 전송해도 될까요?" 물어보고 문제 없다고 하면 그제야 보냄.<br>
보낸 후 "감사합니다" 인사까지 하고 물러간다.<br>

연결 지향형 프로토콜 <br>
데이터 **안정성**을 위해 **신뢰성/흐름**을 제어하는 전송 계층 프로토콜 <br>
UDP에 비해서는 느림 <br>
정확성 필요하면 TCP <br>

#### 💡 연결과정 3-way-handshake

1. SYN: 나 데이터 보내도 돼?<br>
2. SYN/ACK: 응 보내<br>
3. ACK: 그제야 데이터 보낸다.<br>

#### 💡 데이터 송수진 시 동작

1. 데이터(패킷) 순서 보장 <br>
2. 데이터 흐름 제어 <br>
3. 데이터 신뢰성 보장(재전송) <br>

#### 💡 연결 해제 과정 4-way-handshake

1. FIN <br>
2. ACK <br>
3. FIN <br>
4. ACK 하고 나서야 연결 해제 <br>

### ☑️ UDP: User Datagram Protocol

막무가내 프로토콜<br>
그냥 일단 데이터 보냄.<br>
받으면 받는거고 안 받으면 안 받는겨~<br>
<br>
데이터 신뢰성보다는 **속도와 간단한 통신을** 중시하는 전송계층 프로토콜<br>
속도 중요하면 UDP<br>

- 연결과정 3-way-handㅜshake **생략**<br>
- 데이터(패킷) 순서 보장 ❌<br>
- 데이터 흐름 제어 ❌<br>
- 데이터 신뢰성 낮음<br>
- 연결 해제 과정 4-way-handshake **생략**<br>
