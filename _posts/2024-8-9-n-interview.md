---
title: Interview_OSI/TCP/IP/handshake/IOCP
categories: [Computer Science, Network]
tags: [] # TAG names should always be lowercase
---

## ✅ OSI 7 Layer

- Application: 사용자가 네트워크에 접속할 수 있도록 서비스 제공
- Presentation: 세션 계층 간 주고받는 인터페이스를 일관성있게 제공
- Session: 통신 시스템 사용자간의 연결 위한 유지
- Transport: 두 호스트 사이 데이터 흐름 제공
- Network: 패킷을 네트워크 간의 IP를 통해 전달(라우팅)
- Datalink: 송/수신. MAC주소 가지고 통신(스위치, 브릿지)
- Physical: 전송하는데 필요한 기능 제공(케이블, 허브)

💡 <https://soheeparklee.github.io/posts/n-1osi/> <br>

## ✅ TCP/IP

- Application: 데이터 송수신에 대한 약속
- Transport: 데이터의 실제 송수신
- Internet: 경로 검색 라우팅
- Network Interface: 네트워크 표준과 관련된 프로토콜 정의 LAN, WAN

## ✅ TCP

> 3 way handshake: secure data exchange <br>
> flow control, congestion control <br>

**Server**

- `socket()` create socket
- `bind()` allocate socket address
- `listen()`
- `accept()` allow connection
- `read/write()` data exchange
- `close()`

**Client**

- `socket()` create socket
- `connect()`
- `read/write()` data exchange
- `close()`

💡 <https://soheeparklee.github.io/posts/n-3protocol/> <br>

## ✅ 3 way handshake

- to start communication
- client ➡️ server: `SYN` asking for connection
- server: recives `SYN`
- server ➡️ client: `ACK(M+1), SYN(N)` packet
- client: revieve `ACK(M+1), SYN(N)`, send `ACK(N+1)`, connection success

- client ➡️ server: `FIN`
- server: recieve `FIN`, send `ACK`
- TIME_OUT until all data is sent
- when all data is send, server ➡️ client `FIN`
- client ➡️ server: `ACK`
- server: close socket conenction
- client: in case there are missing data, `TIME_WAIT`

💡 <https://soheeparklee.github.io/posts/n-2tcp/> <br>

## ✅ UDP

- TCP와 달리 메세지를 패킷으로 나누고, 재조립하는 서비스를 제공하지 않음
- 다른 컴퓨터를 거치지 않고 데이터 주고받을 컴퓨터끼리 연결

## HTTP 🆚 HTTPS

HTTP: TCP ➡️ HTTP <br>
HTTPS: TCP ➡️ SSL ➡️ HTTP <br>
<br>
SSL: 정보 암호화, 공개키, 개인키 <br>
HTTPS: 인터넷 상에서 주고받는 데이터를 암호화하기 위해 SSL를 쓴다. <br>

## ✅ IOCP

> Input/output Completion Port <br>
> 입력, 출력할 포트를 지정해서 처리하겠다. <br>
> 프로그램 대기 시간을 줄이기 위해 비동기 작업을 하면서 블록을 맏는다. <br>

- multithreading
- thread pooling

## ✅ Thread Pooling

- create several threads, wait
- when needed, use one thread and when finished, return to pool

## Router 🆚 Switch

- Router: Network Layer, check recieved packet data and send the packet to right path
- Switch: DataLink Layer, send frame by looking at MAC address table
