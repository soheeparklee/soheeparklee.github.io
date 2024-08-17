---
title: Protocol / TCP/IP  / Traffic control / Flow control
categories: [Computer Science, Network]
tags: [cs, network, supercoding] # TAG names should always be lowercase
---

## ☑️ 프로토콜

프로토콜: 둘 이상의 장치가 정보전달 시 **의사소통하는 규칙과 규약 집합** <br>
컴퓨터 네트워크에서 **패킷 생성/전송/해석/처리** 관련 규칙과 규약 집합 <br>

- UTP 포로토콜: 게임<br>
- SMTP 프로토콜: 이메일<br>

## 💡 애플리케이션 프로토콜 선택

속도, 신뢰성 고려해서 **TCP/UDP** 선택<br>
네트워크 모델 고려해서 **서버 클라이언트/ P2P/ 중앙 집중 구조** 중 선택<br>
보안성 강한 HTTPS 골라도 좋음<br>

## ✅ TCP/IP 프로토콜

- define how data is transmitted over network
- divide data into packets at the sender's end
- and recombine at the reviever's end

## ✅ TCP/IP Layers

<img width="753" alt="스크린샷 2024-01-06 오후 3 49 29" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/b4d34997-0113-431f-b177-63bd2248df8a">

### 4️⃣ Application Layer

> 사용자에게 네트워크 애플리케이션 제공 <br> > <br>

> shield upper layer from the complexities of data <br>
> HTTP, HTTPS, NTP(Network Time Protocol, synchrnoize clock on computer) <br>

- 데이터를 어떻게 해석할 것인가 <br>
- 많은 종류의 프로토콜이 있음 <br>
- Encapsulation

### 3️⃣ Transport Layer(TCP/UDP)

> 프로세스 간 데이터 전송 <br>

**주요 프로토콜** <br>
✔️ TCP<br>
✔️ UDP<br>

- reliable data transmission
- exchange data
- retransmit data for missing packets

- 데이터의 안정적인 전송을 담당,<br>
- 포트 번호를 사용하여 통신을 제공한다.<br>
- 데이터를 어떻게 전달할 것인지<br>

### 2️⃣ Internet Layer

> 호스트 간 통신 경로 확보 <br>

✔️ IP version <br>
✔️ NCP(IP이전에 사용하던 주소) <br>

- connect two hosts
- Routing of data packets between devices

- 네트워크 주소 기반 데이터 전송<br>
- IP version에 대한 정보 저장<br>

### 1️⃣ Link Layer

> 데이터를 물리적 전송 매체를 통해 전송 <br>

✔️ 와이파이<br>
✔️ 전선<br>
✔️ Ethernet<br>

- applications requiring network communications
- generate data
- request connections

- 가장 기계에 가까움<br>
- 물리적 프로토콜<br>
- 컴퓨터의 **물리적** 네트워크 연결<br>

## ✅ TCP/IP Process

1. Application Layer: sender application layer writes data on socket <br>
2. Transport Layer: data wrapped with segment, handed over to Network Layer <br>
3. sent to revieving node. Sender save data on sender buffer, reciever saves data on recieve buffer. <br>
4. When application is ready, starts reading data on buffer <br>
5. Flow control should not make **reciever buffer overloaded** <br>
6. Reciever promotes **RWND(Recieve WiNDoW)**: how much left on reciever buffer <br>

## ✅ TCP/IP Traffic control

> **Transmission Control Protocol** <br>
>
> > reliable, connection-oriented protocol in network communication <br>
> > network congestion avoidance algorithm <br>

<br>

> **Problems of reliable network** <br>
>
> > packet loss <br>
> > packet order miss <br>
> > congestion <br>
> > reviever overloaded <br>

## ☑️ Flow Control in TCP

- ⚠️ sender speed > reciever speed <br>
- configure data **speed** according to reciever <br>
- need to ensure reciever doesnt recieve too much packets <br>
- reciever sends feedback of state to sender <br>

### 💊 Solution

1. **Stop and Wait**

- only send next packet when recieved message

2. **Sliding window**
   <img width="604" alt="Screenshot 2024-07-27 at 00 59 08" src="https://github.com/user-attachments/assets/e52725fa-128c-4f43-80bb-41601033800b">

- only can packet size according to reciever
- packet on air = sliding window
  - sliding window= last sent byte - last checked byte

## ☑️ Congestion Control in TCP

- configure host, router to prevent congestion

### 💊 Solution

1. **AIMD**(Additive Increase/Multiplicative Decrease)

- send `n` packet, if arrives successfully, send `n+1`
- if fail, packet send speed `/2`

2. **Slow Start**

- send `n` packet, if arrives successfully, send `n+1`
- if fail, `window size =1`(여기서 말하는 윈도우는 슬라이딩 윈도우)

3. **Fast Retransmit**

- if reciever recieves the wrong packet, send ACK
- but in this ACK, send the number of packet that reciever missed to recieve
- sender will acknowledge he didnt sent this packet, and send.
- if repeated w same number packet more than three times, reduce `window size`

4. **Fast Recovery**

- if congestion, increase `window size`

## 💡 Reference

<https://gyoogle.dev/blog/computer-science/network/%ED%9D%90%EB%A6%84%EC%A0%9C%EC%96%B4%20&%20%ED%98%BC%EC%9E%A1%EC%A0%9C%EC%96%B4.html>
