---
title: PART10_WAN
categories: [Computer Science, CISCO networking]
tags: [cs, wan, ppp, hdlc, isdn, frame, replay]
---

## 1️⃣ WAN: Wide Area Network

LAN처럼 내가 직접 선을 깔아 네트워크를 구축할 수 없을 때, 통신하는 방법 <br>

### ✅ WAN 구축 방식

#### ✔️ Leased Line 전용선

통신사업자가 이미 설치해 놓은 회선 중 하나를 대여해서 쓰는 방법 <br>
돈이 들지만, 그래도 나 혼자 쓸 수 있는 전용 라인이니까 leased line <br>

#### ✔️ Circuit Switched

통신을 하는 순간에만 나에게 필요한 회선을 열어주고 통신이 끝나면 회수하는 방식 <br>
통신할 때만 회선 쓰고, 통신 끝나면 회선 반납 <br>
ISDN, 모뎀 <br>

#### ✔️ Packet Switched

통신하는 순간에도 통신 회선 전체를 빌려주는 것이 아니라, 통신 회선을 다른 사람들과 나눠서 쓴다. <br>
**virtual circuit**: 사실은 나에게 배정된 회선이 업슨ㄴ데 마치 있는 것처럼 통신 <br>
프레임 릴레이, ATM, X25 <br>

### ✅ CPE, Dematcation, DTE

#### ✔️ CPE: Customer Premises Equipment

고객이 가진 장비<br>
라우터, DSU/CSU<br>

#### ✔️ Demarcation

경계: 어디까지가 고객이 책임지는 부분이고, 어디까지가 서비스 제공자가 책임지는 부분인지 나눌 때<br>

#### ✔️ DTE: Data Terminal Equipement

데이터가 WAN쪽으로 여행을 시작하는 터미널 같은 곳<br>
라우터

## 2️⃣ HDLC, PPP

WAN 구간을 세팅할 때 쓰는 기법들 <br>

### ✅ HDLC: High-level Data Link Control

표준 프로토콜이나, 시스코에서 사용하는 HDLC는 표준 프로토콜이 아니다.<br>
그래서 시스코 라우터와 다른 회사의 라우터를 서로 시리얼로 연결하는 경우에는 HDLC를 쓰면 안 된다.<br>

### ✅ PPP: Point to Point

👍🏻 encapsulation <br>
👍🏻 보안 기능 <br>
👍🏻 여러 가지 네트워크 계층 프로토콜을 한꺼번에 지원한다. <br>

#### 👬 PPP 보안 도우미

✔️ NCP: Network Control Protocol<br>
멀티프로토콜 지원<br>
✔️ LCP: Link Control Protocol<br>
링크 접속 보안, 에러 체크, 압축 기능 및 멀티링크PPP<br>

#### 🔖 PPP의 세션 구축 단계

➖ 데이터 링크 계층 세션 구축<br>
➖ 보안 인증<br>
➖ 네트워크 계층 세션 구축<br>

#### 🔐 PPP 보안인증 방법 PAP, CHAP

두 라우터 간에 서로를 확인하기 위한 보안 방법<br>
<br>

🔑 **PAP:** Password Authentication Protocol<br>
🤝🤝 2 way handshake: 인증을 위해 두 번의 통신이 이루어진다.<br>
<br>
예를 들어, 서울 라우터와 부산 라우터가 PPP로 접속하고 있고 보안 인증은 PAP방식<br>
부산 라우터 ➡️ 서울 라우터에게 접속 요청<br>
부산 라우터는 자신의 Host Name, Password를 서울 라우터에게 보냄<br>
서울 라우터는 자신이 가지고 있는 Host Name, Password와 비교<br>
일치하면 접속 허가<br>
<br>

👎🏻 Host Name, Password가 **clear text**로 이동한다.<br>
🟰 Host Name, Password가 **그대로 노출되어** 해킹될 수 있다.<br>

🔑 **CHAP:** Challenge Handshake Authentication Protocol<br>
🤝🤝🤝 2 way handshake: 인증을 위해 세 번의 통신이 이루어진다.<br>
<br>

예를 들어, 서울 라우터와 부산 라우터가 PPP로 접속하고 있고 보안 인증은 CHAP방식<br>
부산 라우터 ➡️ 서울 라우터에게 접속 요청<br>
서울 라우터는 부산 라우터에게 **Challenge**를 보낸다.<br>
Challenge: 이 코드값을 이용해 답을 보내라<br>
<br>

부산 라우터는 Challenge를 가지고 자신의 패스워드 암호화 **HASH** 해서 서울 라우터에게 보낸다. <br>
⭐️ **HASH**: 기존의 데이터를 어떤 코드 값을 이용해서 완전히 변형시켜 절대 원본 데이터로 돌아갈 수 없도록 만들기 <br>
<br>
서울 라우터는 자기도 똑같은 해싱 방법으로 결과를 만들어 부산 라우터에게서 받은 값과 비교
일치하면 접속 허가<br>
<br>

👍🏻 중간에 해킹해도 **HASH**되어 있으니 원래 비밀번호를 알 수가 없다.<br>

## 3️⃣ Frame Replay

WAN의 통신 방식 <br>
전통적으로 x.25방식을 사용했으나, <br>
Frame Replay는 에러 복구와 흐름 제어 등 데이터 처리 과정을 생략해 효율적인 데이터 전송 방법을 제거 <br>
그러니까 x.25보다 빠르고 효과적이나 에러 제어 기법은 거의 제공이 안 된다. <br>

#### ✔️ DLCI: Data Link Connection Identifier

프레임 릴레이 연결을 위한 주소<br>

#### ✔️ LMI: Local Management Interface

DLCI 정보와 함께 설정된 PVC 정보를 알려주어 인터페이스의 다양한 정보와 동작 상태 등을 제공<br>
라우터에서 LMI를 세팅할 때 LMI 타입을 맞춰주어야 한다.<br>

## 4️⃣ ISDN: Integrated Services Diigital Network

ISDN은 Circuit Switched Network의 한 종류<br>

#### ✔️ BRI: Basic Rate Interface

B 채널 2개, D 채널 1개

#### ✔️ PRI: Primary Rate Interface

B 채널 23개, D 채널 1개

### ✅ TE: Terminal Equipment

ISDN망에 접속한 장비

#### ✔️ TE1: ISDN용 전용 장비

#### ✔️ TE2: ISDN 전용 장비가 아닌 일반 장비(ISDN인터페이스가 없음)

TE2는 ISDN망에 접속하기 위해서는 TA(Terminal Adapter) 필요
