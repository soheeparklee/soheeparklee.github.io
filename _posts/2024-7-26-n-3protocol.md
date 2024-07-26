---
title: TCP/IP Protocol, Traffic control
categories: [Computer Science, Network]
tags: [cs, network, supercoding] # TAG names should always be lowercase
---

## ✅ 네트워크

둘 이상의 컴퓨터/장치/물질이 서로 **정보를 주고받는** 구조 <br>

#### ☑️ LAN WAN ISP

inter 네트워킹<br>
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

## 💡 애플리케이션 프로토콜 선택

속도, 신뢰성 고려해서 **TCP/UDP** 선택<br>
네트워크 모델 고려해서 **서버 클라이언트/ P2P/ 중앙 집중 구조** 중 선택<br>
보안성 강한 HTTPS 골라도 좋음<br>

## ✅ TCP/IP 프로토콜

#### ☑️ 프로토콜

프로토콜: 둘 이상의 장치가 정보전달 시 **의사소통하는 규칙과 규약 집합** <br>
컴퓨터 네트워크에서 **패킷 생성/전송/해석/처리** 관련 규칙과 규약 집합 <br>

- UTP 포로토콜: 게임<br>
- SMTP 프로토콜: 이메일<br>

#### ☑️ TCP/IP 프로토콜

<img width="753" alt="스크린샷 2024-01-06 오후 3 49 29" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/b4d34997-0113-431f-b177-63bd2248df8a">

## ✅ TCP/IP Layers

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

### ⭐️ Transport Layer

데이터의 안정적인 전송을 담당,<br>
포트 번호를 사용하여 통신을 제공한다.<br>
데이터를 어떻게 전달할 것인지<br>

**주요 프로토콜**
✔️ TCP<br>
✔️ UDP<br>

### ⭐️ Internet Layer

네트워크 주소 기반 데이터 전송<br>
IP version에 대한 정보 저장<br>
✔️ IP version<br>
✔️ NCP(IP이전에 사용하던 주소)<br>

### ⭐️ Network Interface

가장 기계에 가까움<br>
물리적 프로토콜<br>
컴퓨터의 **물리적** 네트워크 연결<br>
✔️ 와이파이<br>
✔️ 전선<br>
✔️ Ethernet<br>

## ✅ TCP/IP Process

1. Application Layer: sender application layer writes data on socket <br>
2. Transport Layer: data wrapped with segment, handed over to Netwoek Layer <br>
3. sent to revieving node. Sender save data on sender buffer, reciever saves data on recieve buffer. <br>
4. When application is ready, starts reading data on buffer <br>
5. Flow control should not make **reciever buffer overloaded** <br>
6. Reciever promotes **RWND(Recieve WiNDoW)**: how much left on reciever buffer <br>

## ✅ TCP/IP Traffic control

> Transmission Control Protocol
>
> > reliable, connection-oriented protocol in network communication <br>
> > network congestion avoidance algorithm <br>

<br>

> Problems of reliable network
>
> > packet loss <br>
> > packet order miss <br>
> > congestion <br>
> > reviever overloaded <br>

## ☑️ Flow Control in TCP

> ⚠️ sender speed > reciever speed <br>
> configure data **speed** according to reciever <br>
> need to ensure reciever doesnt recieve too much packets <br>
> reciever sends feedback of state to sender <br>

### 💊 Solution

1. Stop and Wait

- only send next packet when recieved message

2. Sliding window
   <img width="604" alt="Screenshot 2024-07-27 at 00 59 08" src="https://github.com/user-attachments/assets/e52725fa-128c-4f43-80bb-41601033800b">

- only can packet size according to reciever
- packet on air = sliding window
  - sliding window= last sent byte - last checked byte

## ☑️ Congestion Control in TCP

> configure host, router to prevent congestion

### 💊 Solution

1. AIMD(Additive Increase/Multiplicative Decrease)

- send `n` packet, if arrives successfully, send `n+1`
- if fail, packet send speed `/2`

2. Slow Start

- send `n` packet, if arrives successfully, send `n+1`
- if fail, `window size =1`(여기서 말하는 윈도우는 슬라이딩 윈도우)

3. Fast Retransmit

- if reciever recieves the wrong packet, send ACK
- but in this ACK, send the number of packet that reciever missed to recieve
- sender will acknowledge he didnt sent this packet, and send.
- if repeated w same number packet more than three times, reduce `window size`

4. Fast Recovery

- if congestion, increase `window size`

## 💡 Reference

<https://gyoogle.dev/blog/computer-science/network/%ED%9D%90%EB%A6%84%EC%A0%9C%EC%96%B4%20&%20%ED%98%BC%EC%9E%A1%EC%A0%9C%EC%96%B4.html>
