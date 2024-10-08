---
title: CISCO_PART5_IP주소
categories: [Computer Science, Network]
tags: [cs]
---

## 1️⃣ IP 주소 이야기 1, 2, 3

### IP주소란?

TCP/IP프로토콜을 쓰는 장비들을 구분해주기 위해 만들어낸 주소 ➡️ 장비마다 IP주소는 모두 **다르다.** <br>

## ✅ IPv4, IPv6

#### ✔️ IPv4

IP주소는 **이진수 32자리**로 되어 있다.(IPv4) <br>
그래서 IP주소의 개수는? 2의 32제곱 <br>
이진수 8자리 **(옥텟, Octet)** 마다 점을 찍는다. <br>
근데 이진수 32자리수로 하면 사람이 알아보기 너무 힘드니까 이진수를 십진수로 바꿔서 쓴다. <br>

- 32비트 2진수
- 2진수 32자리
- 예시: `11000001 00100000 11011000 00001001`
- 십진수로 나타내면 예시: `193.32.216.9`

#### ✔️ IPv6

- 128비트 2진수
- 16비트 단위로 끊어서 쓴다.
- 예시: `2004:2ba8:13aa:0011:0000:0000:0000:abaa`

## 📌 MTU

> Maximum Transmission Unit
> maximum data link-level frame can transmit

- different link types, different MTUs
- large IP datagram ➡️ fragmented `datagrams`
- reassembled at final destination
- `IP header bits` used to identify, orfer related fragments

```
If 4000bite(IP header(20 bites) + Payload(3980 bites))
and MTU 1500
need to make three fragments
  - fragments are called `datagram`
for `fragmentation` and `reassembly`, in `IP header`...
  - ID: same ID for fragmented datagrams
  - Flag: to identify until where is fragmented datagram, last datagram flag is 0
  - Offset: to reassemble in order

Conclusion:
- original datagram: IP header(20 bites) + Payload(3980 bites)
- MTU: 1500
- 3980= 1480 + 1480 + 1020

- First datagram: 20(header) + 1480(payload)
  ID: x, fragflag: 1, offset: 0(byte)
- Second datagram: 20(header) + 1480(payload)
  ID: x, fragflag: 1, offset: 185(1480/8)(byte)
- Third datagram: 20(header) + 1020(payload)
  ID: x, fragflag: 0, offset: 370(1480+1480/8)(byte)
```

## ✅ IP주소의 구성 `네트워크 부분` + `호스트 부분`

#### 네트워크 부분 Network Part

같은 네트워크 상에 있다 <br>
🟰 브로드캐스트 영역 Broadcast Domain <br>
🟰 한 PC가 데이터를 뿌렸을 때 라우터를 거치지 않고 통신이 가능한 영역 <br>

#### 호스트 부분 Host Part(노드 부분)

각각의 PC 또는 장비 <br>
마지막 옥텟(맨 마지막 자리)가 호스트 부분 <br>

#### 네트워크 부분은 🟰 호스트 부분은 항상 🟰❌

IP주소에서 네트워크 부분은 모두 같아야 하고 호스트 부분은 모두 달라야 한다. <br>
서로 같은 네트워크 상에서는 네트워크 부분은 모두 같고, 호스트 부분은 달라야 함. (같으면 충동 생김) <br>

```
  203.240.100.1
------------- ---
네크워크 부분     호스트 부분(노드부분)

```

#### ⭐️ 네트워크 내부 ❓ 허브 또는 스위치 : 라우터

네트워크 내부에서 통신한다면? 허브 또는 스위치가 호스트 부분(노드 어드레스)보고 통신 <br>
네트워크 외부로 나가야 한다면? 라우터가 필요하다. <br>
<br>
라우터가 라우팅(경로 배정)을 할 떄는 네트워크 부분만 보고, <br>
스위치나 허브가 노드 어드레스 보고 통신한다. <br>
따라서 같은 네트워크 상에서 통신한다면, 라우터가 필요가 없다! <br>
라우터 없이 내부 통신 가능 ⭕️ <br>
<br>

## ✅ IP주소의 클래스

네트워크 부분, 호스트 부분 구분하기 <br>
어디까지가 네트워크 부분이고, 어디까지가 호스트 부분인가? <br>
❓ 클래스를 나누는 이유; IP주소를 적정하고 효율적으로 배분하기 위해 <br>

#### ☑️ 클래스 A

```
                  옥텟 1       옥텟 2      옥텟 3      옥텟 4
                0xxx xxxx. xxxx xxxx. xxxx xxxx. xxxx xxxx
                - -------  ---------------------------------
              시작0   네트워크(7)       호스트 부분(24)
```

IP 주소 0으로 시작 <br>
네트워크 주소: 처음 **8**비트(1바이트) ➕ 호스트 주소: 나머지 **24**비트(3바이트) <br>
✔️ 네트워크 번호 시작: **1~126**(127은 예비 번호) <br>
✔️ 최대 네트워크 주소 개수: `2^7` <br>
✔️ 한 네트워크 안에 들어갈 수 있는 최대 호스트 수: `2^24 -2`개 <br>
(모두 0인 경우는 **네트워크 자체 주소**, 모두 1인 경우는 **브로드캐스트 주소**) <br>
하나의 네트워크가 가질 수 있는 호스트 수가 가장 많은 클래스 <br>

#### ☑️ 클래스 B

```
                  옥텟 1       옥텟 2      옥텟 3      옥텟 4
                10xx xxxx. xxxx xxxx. xxxx xxxx. xxxx xxxx
                - ------------------  ----------------------
              시작10   네트워크(14)           호스트 부분(16)
```

IP 주소 10으로 시작 <br>
✔️ 네트워크 번호 시작: **128.1 - 191** <br>
✔️ 최대 네트워크 주소 개수: `2^14` <br>
✔️ 한 네트워크 안에 들어갈 수 있는 호스트 수: `2^16 -2` <br>
(모두 0인 경우는 **네트워크 자체 주소**, 모두 1인 경우는 **브로드캐스트 주소**) <br>

#### ☑️ 클래스 C

```
                  옥텟 1       옥텟 2      옥텟 3      옥텟 4
                110x xxxx. xxxx xxxx. xxxx xxxx. xxxx xxxx
                - -----------------------------  ---------
              시작110          네트워크(21)           호스트 부분(8)
```

IP 주소 110으로 시작 <br>
✔️ 네트워크 번호 시작: **192 - 223** <br>
✔️ 최대 네트워크 주소 개수: `2^21` <br>
✔️ 한 네트워크 안에 들어갈 수 있는 호스트 수: `2^8 -2` <br>
(모두 0인 경우는 **네트워크 자체 주소**, 모두 1인 경우는 **브로드캐스트 주소**) <br>
공인 IP주소를 배정해 줄 때 클래스 A, B는 너무 많은 HOST주소를 가질 수 있기 때문에 일반적으로는 HOST C로 배정해준다. <br>

#### ☑️ 클래스 D, E

클래스 D는 멀티캐스트용, 클래스 E는 연구용 <br>
내가 필요한 그룹에만 한꺼번에 데이터를 전송할 때 쓰는 주소 <br>

## 2️⃣ 라우터에서 IP 주소 이해하기

우리가 라우터에 배정해야 하는 IP주소는 총 2개이다. <br>

- 이더넷 인퍼에이스용(내부) <br>
  - 우리가 부여받은 번호 중에 하나를 쓴다. <br>
- 시리얼 인터페이스용(외부) <br>
  - 우리가 접속하는 ISP업체에 따라 다르므로 인터넷 제공업체에 문의해서 사용 <br>
- 그리고 서브넷마스크는 서로 같아야 한다. <br>

## 3️⃣ Subnet Mask의 정의와 사용 이유

**서브넷 마스크**: 주어진 IP 주소를 네트워크 환경에 맞게 나누어 주기 위해서 씌워주는 이진수의 조합이다. <br>
서브(메인이 아님)적인 네트워크를 사용하기 위해 씌우는 마스크. <br>
서브넷 간의 통신은 **라우터**를 통해서만 가능하다. <br>

- 네트워크가 서로 다르다 🟰 브로드캐스트 도메인이 서로 다르다. <br>
- 네트워크 번호는 호스트 부분을 0으로 쓴다. <br>
- 라우터는 인터페이스별로 각각 IP주소를 배정하지만 <br>
- 스위치나 허브는 장비별로 IP주소를 배정한다. <br>

## ✅ 게이트웨이

내부 네트워크에 내가 찾는 IP주소를 가진 곳이 없으면, 내가 속한 네트워크 밖으로 나가 외부 네트워크를 찾아야 한다. <br>
이 때 나가는 문이 **게이트웨이** <br>
<br>
게이트웨이: 내부 네트워크에서 없는 녀석을 찾을 때 밖으로 통해 있는 문 <br>
🟰 이 문은 바로 라우터의 이더넷 인터페이스 <br>

## 4️⃣ Subnet Mask의 시작

### 서브넷으로 나누는 이유

#### 1. 브로드케스트 영역 나누기

만약 IP 주소를 받은 그대로 사용한다면, 너무 큰 네크워크가 구성됨 <br>
➡️ 브로드캐스트 도메인이 너무 크다. <br>
➡️ 통신이 불가능 <br>
네크워크를 나누어 쓰기 위해 서브넷 마스크를 씌운다. <br>

#### 2. IP 주소 아끼기

## 4️⃣ 서브네팅과 서브넷 마스킹

### 서브네팅

하나의 주소에 서브넷 마스크를 씌워서 작은 네트워크로 만드는 것 <br>

### 서브넷 마스킹

기존 IP 주소의 호스트 부분의 일부를 네트워크 부분으로 바꾸는 작업 <br>

## 5️⃣ 서브넷 마스크의 구성

### subnet masking

<img width="436" alt="Screenshot 2024-08-12 at 20 41 11" src="https://github.com/user-attachments/assets/d2f1f0e4-e116-446d-9fdf-b2617b1dc5f8">

- three subnets in the picture
- each IP adress left 24bits are the same
- thus, subnet mask is 24
- in each subnet, there can be `2^8-2` host addresses
  - why minus 2?
  - one for broadcast address `11111111`
  - one for network address `00000000`

### 항상 IP 주소를 따라다니는 서브넷 마스크

#### 디볼트 서브넷 마스크

클래스C를 나누어 쓰지 않고 몽땅 쓰는 상황에서도 서브넷 마스크는 무조건 IP 주소를 따라다닌다. <br>

- 클래스 C의 경우 디폴트 서브넷 마스크: 255.255.255.0 <br>
- 클래스 B의 경우 디폴트 서브넷 마스크: 255.255.0.0 <br>
- 클래스 A의 경우 디폴트 서브넷 마스크: 255.0.0.0 <br>

### 서브넷 마스크는 IP 주소의 네트워크 부분, 호스트 부분을 나타내준다.

![IMG_FB3DD1A4252E-1](https://github.com/soheeparklee/sc_project_carrotMkt_improved/assets/97790983/78d4c0a7-6537-48cb-944b-f02f023571f6)

네트워크: 서브넷 마스크가 2진수로 **1**인 부분 <br>
호스트: 서브넷 마스크가 2진수로 **0**인 부분 <br>
논리연산자 AND를 사용해서 서브넷 계산 가능 <br>
논리연산자 AND는 양쪽이 모두 1인 경우에만 1이 된다. <br>

## ⭐️ 콜리전 도메인, 브로드캐스트 도메인 나누기

콜리전 도메인을 나누는 방법 ➡️ 스위치 <br>
콜리전 도메인을 나누더라도 브로드캐스트 도메인의 크기는 그대로이다. <br>
브로드캐스트 도메인을 나누는 방법 ➡️ 라우터(라우터의 이더넷 인터페이스) <br>

## 6️⃣ 서브넷 마스크 기본 성질

### 서브넷

서브넷 마스크로 나누어진, 하나의 독립된 네트워크 <br>

### 1. 서브넷은 라우터를 통해서만 통신

서브넷 마스크로 만들어진 네트워크, 즉 **서브넷**은 이제 하나의 네트워크이기 때문에 서로 나뉜 서브넷끼리는 라우터를 통해서만 통신이 가능하다. <br>

![이름 없는 노트북-8](https://github.com/soheeparklee/sc_project_carrotMkt_improved/assets/97790983/c0ff1adf-36e1-4d2b-9941-5b090fbf4785)

### 2. 서브넷 마스크는 2진수로 썼을 때 '1'이 연속적으로 나와야 한다.

(간소화) 1111.1111.1100.1111 ❌<br>
(간소화) 1111.1111.1111.1100 ⭕️<br>

## 7️⃣ 서브넷 마스크 응용 문제 풀기

![이름 없는 노트북-11](https://github.com/soheeparklee/sc_project_carrotMkt_improved/assets/97790983/f21c1a31-e0b8-4028-bc13-7c599d553464)ㄴ
