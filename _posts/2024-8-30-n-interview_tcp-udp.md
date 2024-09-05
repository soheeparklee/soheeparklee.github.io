---
title: Interview_TCP/UDP
categories: [Computer Science, Network]
tags: [interview] # TAG names should always be lowercase
---

## 📌 UDP

<details>
<summary>✅ What is UDP? </summary>
- User Datagram Protocol <br>
- conectionless <br>
- unreliable <br>
- check just data error with checksum <br>

</details>

<br>

<details>
<summary>✅ What are the benefits of UDP? and the disadvantages? </summary>
👍🏻 fast <br>
👍🏻 less overhead <br>
👍🏻 1:1, 1:N, N:N connection possible <br>

👎🏻 packet loss, corruption<br>
👎🏻 data can be recieved in different order <br>

</details>

<br>

<details>
<summary>✅ What is UDP checksum? </summary>
- to check data error <br>
- send data with checksum header <br>
 <br>
- divide segment into 16bits <br>
- add all, add 1, create checksum <br>
- send data with checksum <br>
 <br>
- reciever also creates checksum for recieved data <br>
- if it matches, no error <br>
- if doesnt match, error in segment! <br>
</details>

<br>

<details>
<summary>✅ Where is UDP used?</summary>
- DNS <br>
- SNMP <br>
- RPC, NetBios, syslog, Kerberos, TFTP <br>
- streaming, internet calls<br>
<br>

- allow little data loss <br>
- need to send fast <br>
</details>

<br>

<details>
<summary>✅ How is UDP connection? </summary>
- server, client can be connected 1:1, 1:N, N:N <br>
</details>

<br>

<details>
<summary>✅ What is overhead?</summary>
- excess usage of computing resource <br>
- such as processing, memory, bandwidth <br>
<br>
- extra memory required for supplemental information <br>
- (ex) src to destination <br>
- space eaten up by protocols to acheive certain goal <br>
</details>

<br>

<details>
<summary>✅ What is payload? </summary>
- actual data to be transmitted <br>
</details>

<br>

## 📌 신뢰적 데이터 전송

<details>
<summary>💊 How can we prevent data loss during transmission? </summary>
- ARQ <br>
- countdown timer <br>
- sliding window <br>
</details>

<br>

<details>
<summary>✅ How long should be countdown timer? </summary>
- more than travel time <br>
- more than time reciever needs to manage segment <br>
</details>

<br>

<details>
<summary>✅ What is ARQ? </summary>
- Automatic Repeat Request/Query <br>
<br>
- error checking<br>
- reciever feedback<br>
- sender retransmit<br>
<br>
- ⭐️ sequence number <br>
- ⭐️ countdown timer <br>
- ⭐️ sliding window <br>
</details>

<br>

<details>
<summary>⭐️  What is stop and wait? </summary>
- Send and wait until ACK response from reciever <br>
- 👍🏻 reliable, 👎🏻 but slow <br>
</details>

<br>

<details>
<summary>✅ What is pipeline protocol? </summary>
- Send packets without waiting for ACK response <br>
- 👎🏻 cannot solve data packet loss <br>
- 👎🏻 recieved order might be different <br>
- from HTTP 1.1 <br>
</details>

<br>

<details>
<summary>⭐️ What is GBN ARQ? </summary>
- Go-back-N <br>
- send n(window size) packets if not recieved <br>
- sliding window protocol  <br>
- cumulative acknowledgement 내가 여기까진 받았다 <br>
</details>

<br>

<details>
<summary>✅ What are the benefits, disadvantages of GBN? </summary>
- 👍🏻 pipelining <br>
- 👎🏻 send packet multiple times(lost packet + following frames) <br>
</details>

<br>

<details>
<summary>⭐️ What is SR? </summary>
- selective repeate <br>
- only retransmit lost packet <br>
</details>

<br>

<details>
<summary>✅ What is the benefit of SR? </summary>
- 👍🏻 pipelining <br>
- 👍🏻 send only lost packet <br>
</details>

<br>

## 📌 TCP

<details>
<summary>✅ What is TCP? </summary>
- Transmission control protocol <br>
- Transport layer <br>
- conection oriented <br>
- reliable <br>
</details>

<br>

<details>
<summary>✅ Where is TCP used? </summary>
- HTTP <br>
- SMTP <br>
- FTP <br>
- SSH <br>
</details>

<br>

<details>
<summary>✅ What is full duplex and point-to-point? </summary>
- full duplex: 양방향 <br>
- point-to-point: 2개의 종단점으로 연결
</details>

<br>

<details>
<summary>✅ How is TCP reliable? </summary>
- checksum <br>
- ARQ <br>
- timer <br>
- sequence number <br>
</details>

<br>

<details>
<summary>✅ What does it mean to be "reliable"? </summary>
- data integrity <br>
- data is in the right order <br>
</details>

<br>

<details>
<summary>✅ How is TCP connection-orinted? </summary>
- pre-connection process <br>
- 3 way handshake <br>
</details>

<br>

<details>
<summary>✅ Explain ACK lost scenario in TCP </summary>
- Segment send to reciever, but ACK from reciever to sender was lost <br>
- Sender sends again same packet <br>
- Reciever already recieved, throw away <br>
</details>

<br>

<details>
<summary>✅ Explain premature timeout scenario in TCP</summary>
- Reciever recieves, sends ACK  <br>
- However, ACK arrvies later than timeout <br>
- Sender thinks packets didnt arrive, so sends again<br>
</details>

<br>

<details>
<summary>✅ Explain cumulative scenario in TCP</summary>
- Sender sent segment 1, 2 <br>
- Reciever recieved, sent ACK 1, 2<br>
- ACK 1 was lost, ACK 2 arrived<br>
- Sender thinks as ACK 2 arrived, ACK 1 has arrived successfully<br>
- Retransmission of data does not occur <br>

</details>

<br>

<details>
<summary>✅ How can TCP know which segment to send? </summary>
- sequence number <br>
</details>

<br>

<details>
<summary>✅ What are the problems that can occur in TCP? </summary>
- packet loss <br>
- packet corruption <br>
- reciever overloaded <br>
</details>

<br>

<details>
<summary>✅ How can re realize that a packet is lost? </summary>
- timeout <br>
- 3 duplicate ACK <br>
</details>

<br>

<details>
<summary>✅ What is 3-way-handshake? </summary>
- pre-connection-process <br>

- **SYN** <br>

* client: SYN-SENT

- **ACK** <br>

* sever: SYN_RCVD

- **SYN**

* client: ESTABLISHED, sever: ESTABLISHED
</details>

<br>

<details>
<summary>✅ Why not 2-way-handshake? </summary>
- server needs to check state of client <br>
<br>

- 이럴 때는 연결되면 안된다. <br>
- client request is retransmission of timeout <br>
- TCP connection is over <br>
</details>

<br>

<details>
<summary>✅ How can we confirm message was recieved by server?</summary>
- with ACK(acknowledgement) message <br>
- server replies with ACK message to confirm that server recieved the message<br>
- ACK message is control signal to (1) confirm it recieved message (2) is ready to recieve message<br>
</details>

<br>

<details>
<summary>✅ What is 4-way-handshake? </summary>
- To finish connection <br>
<br>
- FIN <br>
* client: FIN_WAIT   <br>
- ACK <br>
* server: CLOSE_WAIT  <br>
- FIN <br>
* client: TIMED_WAIT  <br>
* server: LAST_ACK  <br>
- ACK <br>
* client: CLOSED  <br>
* server:CLOSED  <br>
</details>

<br>

<details>
<summary>✅ What is fast retransmission in TCP? </summary>
- Sender does not wait until timeout <br>
- When Sender recieves identical ACKs for three times, retransmits <br>
- 3 duplicate ACK <br>
<br>
- fast bc sender does not wait for timeout <br>
</details>

<br>

<details>
<summary>✅ What is flow control? </summary>
- prevent reciever recieving too many segments before it could handle <br>
- 💊 control speed  <br>
<br>

💊 configure sliding window size <br>
💊 stop and wait <br>

</details>

<br>

<details>
<summary>✅ What is congestion control? </summary>
- prevent too many packets on network <br>

💊 AMID(Additive Increase Multiplicative Decrease) <br>
💊 slow start <br>
💊 TCP Tahoe <br>
💊 TCP RENO <br>

</details>

<br>

<details>
<summary>✅ What happens when network is congested? </summary>
- latency <br>
- packet loss <br>

</details>

<br>

<details>
<summary> TCP 🆚 GBN </summary>
- 공통점: sliding window, sendbase, sequence number <br>
- GBN: send n(sliding window size) number of segment <br>
- TCP: send only the missing segment <br>
</details>

<br>

<details>
<summary> TCP 🆚 SR </summary>
- 공통점: retransmit only lost segment <br>
- SR: each segment has timer <br>
- TCP: single timer <br>
</details>

<br>
