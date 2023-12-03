---
title: PART3_TCP/IP
categories: [Computer Science, CISCO networking]
tags: [tcp, ip, binary, dhcp, cbc, ,sbc]
---

## 1️⃣ TCP/IP를 모르면 인터넷을 아는게 아니다?

TCP/IP는 프로토콜의 한 종류 <br>
ARPANET에 의해 처음 개발되었다. <br>
각각의 네트워크에 접속되는 호스트들은 고유의 주소(IP주소)를 가지고 있어 자신이 속한 네트워크 & 다른 네트워크에 연결된 호스트까지 서로 데이터 주고받을 수 있음 <br>
<br>
<br>
TCP/IP라는 것은 사실 IP계층을 사용하면서, 그 위에 사용하는 프로토콜을 TCP와 UDP로 하겠다.<br>
<img width="707" alt="스크린샷 2023-12-02 오후 5 29 16" src="https://github.com/soheeparklee/sc_project_carrotMkt_improved/assets/97790983/a8d35e36-6e27-4c45-bb14-f79b5b6cddd7">

## 2️⃣ IP주소

IP주소가 유일해야 인터넷을 사용할 수 있음 <br>
인터넷을 사용하기 위해서는 유일한 IP주소를 가져야 한다. <br>
원래는 IP주소를 나타낼 때 이진수 32자리로 만들고 이진수 8자리마다 중간에 점을 하나씩 찍음 <br>
이 고유 주소는 Internet Network Information Center(InterNIC)라는 단체에서 관리 분배 <br>

IP주소= 네트워크 주소 + 서브넷 마스크 <br>
같은 네트워크상에 있는 PC들은 동일한 네트워크 부분과 동일한 서브넷 마스크를 가져야 한다. <br>

## 3️⃣ 이진수

원래 IP주소는 이진수로 나타내는데 사람이 알아보기 쉽게 십진수로 나타내기도 함.
우리가 현재 사용하는 IP주소는 버전 4인데, 이는 2의 32승만큼 IP주소를 나타낼 수 있음.
근데 이제 부족해서 IPv6(버전6)이 나왔음
IPv6(버전6)에서는 128개의 이진수로 이루어져 2의 128승만큼 IP주소를 나타낼 수 있게 됨!

## 4️⃣ AND 그리고

둘 다 모두 1이어야 1이 되고, 하나라도 아니면 0이 된다.

```
    1000 0101
AND 1111 1111
--------------
    1000 0101
```

## ✅ DHCP Dynamic Host Configuration Protocol

어떻게 사람이 매번 IP주소 다르게, 또 같은 네트워크 상에 있으면 네트워크, 서브넷 마스크는 같게 IP주소 배정하고 회수함? 너무 어렵고 골치 아픈 일😩

DHCP는 PC마다 IP주소를 미리 지정해 놓지 않고,
DHCP 서버가 그 네트워크에 필요한 IP주소를 모두 가지고 있다가
IP주소를 요구하는 클라이언트 PC가 있으면 그때그때 IP주소를 자동으로 배정
IP주소 다 쓰고나면 회수
DHCP 서버는 원도우 NT나 Novell Netware 또는 라우터에서 기능 실행

클라이언트 PC는 IP주소가 필요하면 브로드캐스트 뿌리고 DHCP 서버에 연결만 되면 자동으로 IP주소 배정받게 됨.

## ✅ 망 분리

네트워크를 분리한다. <br>
이유: 보안 <br>

- 물리적 망 분리: 진짜 망을 인터넷 망과 업무망으로 물리적으로 나눈다. <br>
- 논리적 망 분리 <br>
  - **CBC** Client Based Computing: PC기반의 가상화
    PC안에서 업무 영역과 인터넷 영역을 구분해서 사용
  - **SBC** Server Based Computing: 서버 기반의 가상화
    작업은 서버에서 진행하면서 화면만 PC로 뿌려준다.
