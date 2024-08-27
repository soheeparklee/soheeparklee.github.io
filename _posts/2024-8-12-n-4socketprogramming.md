---
title: Socket Programming
categories: [Computer Science, Network]
tags: [] # TAG names should always be lowercase
---

## ✅ 소켓 프로그래밍

> `IP address + port 번호 + HTTP(프로토콜)` 생성 <br>
> 프로세스에세 HTTP 정보 통로를 열어둔다. <br>

- 소켓에 쓰면 반대편에서 읽을 수 있는데
- 그러기 위해서는 둘이 연결되어야 하고
- 그러기 위해서는 상대편 소켓의 주소를 알아야 한다.
- 이 주소 역할을 하는 것이 바로 `IP address(어떤 컴퓨터) + port 번호(컴퓨터 속 어떤 프로세스인지)`

- 사이트에 접속하기 위해서는 이 주소 `IP address + port 번호`를 알아야 해당 컴퓨터의 소켓과 연결될 수 있음
- 이를 대신해서 `Domain`을 사용한다.

- 주소창에 `Domain`을 치면
- DNS가 `Domain`을 `IP address`로 바꿔준다
- 그리고 port번호는 HTTP의 경우 80, HTTPS는 443

## ✅ Socket API

> TCP 기반 소켓 <br>
> UDP 기반 소켓 <br>
