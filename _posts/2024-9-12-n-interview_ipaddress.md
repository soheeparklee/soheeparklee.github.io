---
title: Interview_IP address
categories: [Computer Science, Network]
tags: [interview] # TAG names should always be lowercase
---

## 📌 IP address

<br>

<details>
<summary> ✅ What is IP address? </summary>
- address for each device connected to network <br>
</details>

<br>

<details>
<summary> ✅ Two parts of IP address? </summary>
- network part ➕ host part <br>
- network part가 같다면 같은 네트워트 ➡️ switch, bridge, hub <br>
- network part가 같다면 다른 네트워트 ➡️ router<br>
- each device has unique host address <br>
</details>

<br>

<details>
<summary> ✅ If devices are on different network, how does it communicate? </summary>
- through router <br>
- router creates broadcast domain <br>
</details>

<br>

<details>
<summary> ✅ What is the difference between IPv4 and IPv6? </summary>
- IPv4: 32bit binary(total 2^32)/ 8 * 4parts/ in decimal, seperate with .<br>
- IPv6: 128bit binary(total 2^128)/16 * 8parts/ in hexadecimal, seperate with : <br>
</details>

<br>

<details>
<summary> ✅ How are the classes of IP address? </summary>
- class A: network 8 + host 24, start with 0 <br>
- class B: network 16 + host 16, start with 10 <br>
- class C: network 24 + host 8, start with 110 <br>
- class D, E
</details>

<br>

<details>
<summary> ✅ What is CIDR? </summary>
- Classless Interdomain Routing <br>
- devide network part, host part of IP address more flexibily than class  <br>
</details>

<br>

## 📌 MTU

<details>
<summary> ✅ What is MTU?</summary>
- Maximum Transmission Unit <br>
- Max data that can be sent <br>
- differs on protocol, link <br>

- ⭐️ fragmentation, reassembly <br>
</details>

<br>

<details>
<summary> ✅ What is in MTU header? </summary>
- ID <br>
- flag <br>
- offset <br>
</details>

<br>

## 📌 Subnet, Subnet Mask

<details>
<summary> ✅ What is Subnet? </summary>
- small isolated part of network <br>
</details>

<br>

<details>
<summary> ✅ Why do we have to make network into smaller subnets?</summary>
- If we use IP address as recieved, broadcast domain is too big <br>
- If broadcast domain is too big, more network load <br>
</details>

<br>

<details>
<summary> ✅ What is subnet mask? </summary>
- use subnet mask to distinguish  IP address into network part and host part <br>
- 1: network part, 0: host part <br>
- example: /20 means first 20 binary numbers are network part <br>
</details>

<br>

<details>
<summary> ✅ Why do we use subnet mask?</summary>
- 1. Make network into smaller subnets <br>
- 2. Save IP address <br>
</details>

<br>

<details>
<summary> ✅ What is broadcasting?</summary>
- one way to trasnmit data from node to node <br>
- one node to all nodes <br>
- exmaple: ARP, DHCP <br>
<br>

- 👎🏻 lot of network traffic, as message is sent to every node in network <br>
- 👎🏻 less secure <br>
  <br>

- 🆚 unicast: point to point <br>
- 🆚 multicast: multiple point to point <br>
</details>

<br>

<details>
<summary> ✅ If subnet mask is /24, how many hosts can be on network?</summary>
- 32-24 = 8 <br>
- 2^8-2 <br>
- 000000: for network address <br>
- 111111: for broadcast address <br>
- others can be used for device IP address, gateway <br>
</details>

<br>

## 📌 Routing

<details>
<summary> ✅ What is a router?</summary>
- route network traffic <br>
- create broadcast domain <br>
- OSI layer 3 <br>
- use IP address to route data <br>
- has routing table <br>
</details>

<br>

<details>
<summary> ✅ What is broadcast domain? </summary>
- when not knowing IP address, send to all device on broadcast domain "who"? <br>
</details>

<br>

<details>
<summary> ✅ What is routing? </summary>
- route network traffic among different network <br>
- look at IP address network part <br>
- If network part is differnet, has to go through router <br>
</details>

<br>

<details>
<summary> ✅ What is gateway? </summary>
- to access totally dissimilar network <br>
- access control <br>
</details>

<br>

## 📌 Routing Protocol

<details>
<summary> ✅ What is routing protocol? </summary>
- protocol to decide how to route data packet from src to dest <br>
- find best route <br>
- update routing table <br>
 <br>

✅ Distance Vector Routing Protocol <br>

- select path on hop counts <br>
- RIP <br>
- hop count: how many router between src and dest? <br>
  <br>

✅ Link State Vector Protocol <br>

- every node constructs a map of the connectivity of network in form of graph <br>
- which node is connected to which <br>
- more about internetwork <br>
- OSPF <br>
  <br>

✅ Advanced Distance Vector Routing Protocol <br>

- hybrid routing protocol <br>
- EIGRP <br>
  <br>

⭐️ RIP <br>

- Routing Information Protocol <br>
- maximum hop: 15, not suitable for big networks <br>
  <br>

⭐️ OSPF <br>

- Open Shortest Path First <br>
- caculate shortest path spanning tree <br>
  <br>

⭐️ IGRP

- Interior Gateway Protocol <br>
- more than 15 hops, maximum hop: 255
- suitable for larger networks
  <br>

⭐️ EGP <br>

- Exterior Gateway Protocol <br>
  <br>

⭐️ EIGRP <br>

- Enhanced Interior Gateway Routing Protocol<br>

⭐️ BGP <br>

- Border Gateway Protocol <br>
- replaced EGP <br>
</details>

<br>

<details>
<summary> ✅ What is DHCP?</summary>
- Dynamic Host Configuration Protocol <br>
- DHCP server automatically assigns IP address when new host joins a network <br>
- client-server based <br>
- message ➡️ request ➡️ response with IP address <br>

- when host sends DHCP message, use broadcasting <br>
</details>

<br>

<details>
<summary> ✅ How is IP address assigned? </summary>
- Static Assignment: manually assign static IP <br>
👍🏻 can predict network <br>
👍🏻 address is static, doesnt change <br>
👎🏻 difficult to manage, address collision  <br>
🛠️ printer, server, important network devies <br>

- Dynamic Assignment: automatically assign dynamic IP addressby DHCP <br>
- only valid for limited time, need revalidation <br>
  👍🏻 automatic
  👍🏻 easy to manage, prevent address collision
  👎🏻 IP address can change dynamically
  🛠️

</details>

<br>

## 📌 NAT, Private IP, Public IP

<details>
<summary> ✅ What is private IP and public IP?</summary>
- Private IP: IP used in private network <br>
- cannot be accessed from outside <br>
- cannot access Internet <br>

- Public IP: IP to access Internet<br>
</details>

<br>

<details>
<summary> ✅ What is NAT? </summary>
- Network Address Translation <br>
- private IP ➡️ NAT ➡️ public IP <br>

- host in private network request with private IP, port <br>
- NAT translate into public IP, assign port <br>
- update NAT translation table <br>
- web server reply arrive to public IP address <br>
- NAT translate again to private IP, send to host <br>
</details>

<br>

<details>
<summary> ✅ What are the benefits of using NAT? </summary>
- 👍🏻 security, private IP access impossible <br>
- 👍🏻 save IP address(several private devices use one public IP address) <br>
- 👍🏻 devices in private network can access Internet <br>
</details>

<br>

## 🆚 Mac address

<details>
<summary> IP address 🆚 Mac address? </summary>
✔️ Mac address <br>
- physical unique identifier on NIC card <br>
- hardware address that is physically embedded into NIC <br>
- OSI layer 2, switch, bridge, collision domain <br>
- 48bit number <br>
<br>

✔️ IP address <br>

- logical identifier assigned to device when joining network <br>
- OSI layer 3, router <br>
- IPv4, IPv6 <br>
  <br>

✔️ ARP<br>

- IP address ➡️ map to Mac address<br>

</details>

<br>

## 📌 ICMP

<details>
<summary> ✅ What is ICMP? </summary>
- Internet Control Message Protocol <br>
- part of Internet Protocol <br>
- IP does not have error reporting function <br>
- ICMP provide error handling in network layer of OSI layer<br>

- 1. Error Handling: if data packet did not arrive, report <br>
- 2. Network assessment: ping <br>

- ping: echo request message
  - check packet loss or delay <br>
  - (check if there is a connection between two devies)<br>
  - (measure the time to reach dest) <br>
- traceroute: know the route between two devices <br>
</details>

<br>
