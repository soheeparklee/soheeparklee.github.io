---
title: Interview 2_Network/Packetization/Protocol/OSI/TCPIP/Network Appliances
categories: [Computer Science, Network]
tags: [interview] # TAG names should always be lowercase
---

## 📌 Network

<details>
<summary>✅ What is computer network? </summary>
- connection of network devices to communicate data <br>
- use WWW <br>
- use HTTP <br>
</details>

<br>

<details>
<summary>✅ What are the types of network?</summary>
- WAN <br>
- LAN <br>
- MAN <br>
- PAN <br>
</details>

<br>

<details>
<summary>✅ How can we transfer data on network? </summary>
- 회선 교환 방식: Circuit-Switched  <br>
- 👎🏻 when circuit is occupied, other computers cannot transmit data <br>
 <br>
- Packet Switched: Divide data into small packets and transmit <br>
- 👍🏻 does not occupy circuit <br>
</details>

<br>

<details>
<summary>✅ What is packetization? </summary>
- Packet: small segment of big data <br>
- Packetization ➡️ Routing ➡️ Transmission medium ➡️ Reassembly ➡️ Error Checking <br>
</details>

<br>

<details>
<summary>✅ What is protocol?</summary>
- Set of rules to transmit data on network <br>
- for example, HTTP, SMTP, UDP <br>
</details>

<br>

---

## 📌 TCP/IP

<details>
<summary>✅ What is TCP/IP?</summary>
- Transmission Control Protocol, Internet Protocol <br>
 <br>
- Application Layer: show to user on application <br>
- Transport Layer: data transmission, TCP/UDP <br>
- Internet Layer: connect host, routing IP address <br>
- Network Link Layer: transmit data through physical device <br>
</details>

<br>

---

## 📌 OSI 7 Layer

<details>
<summary>✅ What is OSI 7 layer?</summary>
- Application Layer: show to user on application [[HTTP/HTTPS]] <br>
- Presentational Layer: change data format to transmitable format [[JPEG, ASCII]] <br>
- Session Layer: connection between application, message, [[SSL/TLS]] <br>
- Transport Layer: filter, manage traffic, segment, [[TCP/UDP]] <br>
- Network Layer: different network, packet, [[IP address, Router, Ping]] <br>
- Datalink Layer: same network, unit, MAC Address, [[Switch, Bridge]] <br>
- Physical Layer: change 0, 1 to analog data, send to physical device, [[Hub, cable, repeater]] <br>
</details>

<br>

<details>
<summary>✅ What are the benefits of dividing into layers?</summary>
- 👍🏻 can see how data is transfered <br>
- 👍🏻 easier for debugging <br>
- 👍🏻 compatible for any device <br>
- 👍🏻 independent layers, dependency on other layers ⬇️ <br>
</details>

<br>

<details>
<summary>✅ Why is it called "layer"?</summary>
- header is added to data as it goes up/down the layers <br>
- c(b(a)) <br>
</details>

<br>

<details>
<summary>✅ Why is header added as data goes up/down the layer?</summary>
- called encapsulation, decapsulation <br>
- only the current layer can decapsulate until that layer level <br>
- 👍🏻 reduce data latency(only open that layer header) <br>
- 👍🏻 encrpyt, secure other layers <br>
</details>

<br>

<details>
<summary>✅ Why is data trasmission always slower than excpected?</summary>
- bc header is added to data <br>
- and needs time for encapsulation, decapsulation <br>
</details>

<br>

<details>
<summary>✅ What is encapsulation and decapsulation? </summary>
- encapsulation: add header to data from higher layer ➡️ lower layer <br>
- decapsulation: remove header from data from lower layer ➡️ higher layer <br>
</details>

<br>

---

## 📌 Network appliances

<details>
<summary>✅ What is NIC?</summary>
- Network Interface card <br>
- OSI layer 1 <br>
- connect computer to network <br>
</details>

<br>

<details>
<summary>✅ What is repeater?</summary>
- amplify digital signal for long distance travel <br>
- OSI Layer 1(Physical Layer) <br>
</details>

<br>

<details>
<summary>✅ What is hub?</summary>
- multi-port repeater <br>
- one hub, one collision domain <br>
</details>

<br>

<details>
<summary>✅ What is bridge? </summary>
- OSI Layer 2(data link layer) <br>
- MAC address <br>
- send unit based on MAC address <br>
- has bridge table <br>
- divides collision domain  <br>
- on same network <br>
</details>

<br>

<details>
<summary>✅ What is L2 Switch?</summary>
- Like bridge, send unit to MAC address <br>
- but has multiple ports <br>
- OSI Layer 2(data link layer) <br>
- on same network <br>
</details>

<br>

<details>
<summary>✅ What is the difference between switch and bridge?</summary>
- switch has multiple ports compared to bridge <br>
</details>

<br>

<details>
<summary>✅ What are the functions of switches and bridges</summary>
- learning  <br>
- flooding  <br>
- forwarding  <br>
- filtering  <br>
- aging  <br>
- aging reflash  <br>
</details>

<br>

<details>
<summary>✅ How does switch, bridge forward frame?</summary>
- store and forward  <br>
- cut-through  <br>
- fragment free  <br>
</details>

<br>

<details>
<summary>✅ What is looping</summary>
- when there is more than one way of reaching switch, hub  <br>
- other PCs cant send data  <br>
- 💊 Spanning Tree algorithm  <br>
</details>

<br>

<details>
<summary>✅ What is spanning tree algorithm?</summary>
- To prevent looping  <br>
- If more than one way of reaching switch, bridge, block all ways except one  <br>
- If problem occurs with current way, unlock the blocked way  <br>
</details>

<br>

<details>
<summary>✅ What is router? </summary>
- OSI Layer 3(network layer) <br>
- IP address  <br>
- send packet based on IP address <br>
- different network <br>
- has routing table <br>
- divide broadcast domain <br>
</details>

<br>

<details>
<summary>✅ What is L3 Switch?</summary>
- switch ➕ router <br>
- MAC address ➕ Routing table 🟰 FPGA hardware <br>
- OSI Layer 3(Network Layer) <br>
</details>

<br>

<details>
<summary>✅ What is L7 Switch?</summary>
- switch with load balancing, firewall, deep packet inspection  <br>
- forward data based on application data  <br>
- OSI Layer 7(Application Layer)  <br>
</details>

<br>

<details>
<summary>✅ What is load balancing?</summary>
- share work load to more than two servers  <br>
</details>

<br>

<details>
<summary>✅ What is gateway? </summary>
- passage to conenct two networks <br>
</details>
