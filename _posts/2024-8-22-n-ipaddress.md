---
title: IP address
categories: [Computer Science, Network]
tags: [] # TAG names should always be lowercase
---

<https://soheeparklee.github.io/posts/chapter5_IPadress/>

## ✅ IP address

> unique address for network interface <br>
> network address ➕ host address <br>

- network interface: network communication point
- host and router

## ✅ Working of IP address

1. Device request Internet Service Provider for acess to network
2. ISP assign device IP address from available range
3. Internet activity goes through ISP, route activity back to you with IP address

## ✅ Type of IP address

#### ✔️ IPv4

- **32 bit** binary number
  - `11000001 00100000 11011000 00001001`
  - in total `2^32`
- separated in 8 bits, 4 parts
- each number can be from `0-225`
- written in decimals(10진수) separated with `.`
  - `193.32.216.9`

#### ✔️ IPv6

- **128 bit** binary number
  - in total `2^128`
- separated in 16 bits, 8 parts
- writeen in hexadecimal(16진수), separated with `:`
  - `2004:2ba8:13aa:0011:0000:0000:0000:abaa`

## 📌 MTU

> MTU: Maximum Transmission Unit <br>
> maximum data that a link layer frame can transmit <br>
> larget possible link-level frame <br>

<img width="406" alt="Screenshot 2024-09-11 at 18 17 10" src="https://github.com/user-attachments/assets/7121d99a-5186-4131-a0ac-18772a01a726">

**1. Different link types, different protocols, different MTUs**

- datagram A: 4000bite(`IP header 20byte` ➕ `payload 3980 byte`)
- datagram A arrives at router
- datagram A has to be sent through link that has `MTU=1500 byte`

**2. Solution: Fragmentation**

> Fragmentation: Large IP datagram divided(fragmented) within net

- one datagram becomes several datagrams
- **reassembled** only at final destination
- IP header bits used to identify, order fragmented datagram

- datagram A is fragmented into three datagram fragments
  - fragment 1: `IP header 20byte` ➕ `payload 1480 byte`
    - ID: x, flag: 1, offset: 0 byte
  - fragment 2: `IP header 20byte` ➕ `payload 1480 byte`
    - ID: x, flag: 1, offset: 185 byte(1480/8)
  - fragment 3: `IP header 20byte` ➕ `payload 1020 byte`
    - ID: x, **flag: 0**, offset: 370 byte(1480+1480/8)

**3. Reassembly**

- when fragmented datagrams arrive at final destination,
- it is reassembled

💡 **IP header for fragmentation, reassembly**

- for fragmentation and reassembly IP header has the following features
- **ID**: all fragments from same datagram share a same ID
- **flag**: to check until where this fragmented datagram ends
  - last flag of fragmented datagram is 0
  - all other flags are 1
- **fragmentation offset**: order of fragmented datagram
  - to reassemble in order
  - byte

<img width="386" alt="Screenshot 2024-09-11 at 18 17 26" src="https://github.com/user-attachments/assets/7cd2937c-e7bb-48f0-935d-1439d0f7b36f">

## 📌 Subnet & Subnet Mask

> subnet: isolated part of whole network <br>
> for subnet, detatch each inferface from host or router, and create island of isolated network <br>

<img width="289" alt="Screenshot 2024-09-11 at 18 23 55" src="https://github.com/user-attachments/assets/4fb12fb6-bdcd-47ad-aef8-f0c27a64b704">

- three subnets(three blue parts)
- for each subnet, first `24bits` are identical `233.1.1`
- subnet mask: `24`
  - means out of `32 bit` address, first `24`bits are `subnet address`
  - 💡 first `24bits: network addresss`, last `8bits: host address`
- in each subnet, `2^8 - 2` number of IP address can exist

> **Why `2^8 - 2` number of IP address can exist?** <br>
>
> > host number `1111111` is used for broadcast address <br>
> >
> > - broadcast address: `255.255.255.255` <br>
> > - if host sends packet to broadcast address, all hosts in same subnet recieve packet <br>
> >   host number `00000000` is used for network address `233.1.1.0` <br>

<br>

**Subnetting**:

- divide large network(class A, B, C) into smaller subnets
- IP range `192.168.1.0/24` can be subnetted into `192.168.1.0/25`, `192.168.1.128/25`
  <br>

**Subnet Masking**:

- use subnet mask to distinguish `network part` and `host part` of IP address
- `255.255.255.0` (or `/24`) means that the first `24 bits` of the IP address represent the `network`, and the r`emaining 8 bits` represent the `host`

- Default subnet masks
  - class C: `255.255.255.0`
  - class B:`255.255.0.0`
  - class A: `255.0.0.0`

> **Why do we use subnet masks?** <br>
>
> > 1. to make smaller parts of network <br>
> >    if we use the IP address as recieved, broadcast domain is too big <br>
> >    communication between subnets are possible through router <br>
> > 2. save IP address <br>

<br>

> **How can we communicate among different subnets?** <br>
>
> > with router <br>

## ✅ IP address parts

> IP address = network address ➕ host address

✔️ **Network part**

- on same subnet
- broadcast domain
- can communicate without going through router

- ⭐️ same for every device on same subnet

✔️ **Host part**

- each PC/device
- last octet
- ⭐️ always different for each device

❓ **Hub, switch, router?**

- on same network: hub, switch
  - look at `host part of IP address`
  - do not need router to communicate

<br>

- on different subnet: router
  - look at different `network part of IP address`

> **What does it mean to have different network address?** <br>
>
> > - to have different broadcast domain <br>

## ✅ IP address class

> **Why do we divde address class?** <br>
>
> > to distribute IP address more efficiently <br>

<img width="710" alt="Screenshot 2024-09-11 at 18 46 49" src="https://github.com/user-attachments/assets/cae47c94-516a-4943-ac4e-716145dd7a6a">

#### ✔️ Class A

> network part `8bits(1byte)` ➕ host part `24bits(3bytes)`

- start with `0`
  - `0xxx xxxx. xxxx xxxx. xxxx xxxx. xxxx xxxx`
- maximum network address number: `0~2^7` (8-1)
- maximum host address number: `2^24 - 2`

#### ✔️ Class B

> network part `16bits(2bytes)` ➕ host part `16bits(2bytes)`

- start with `10`
  - `10xx xxxx. xxxx xxxx. xxxx xxxx. xxxx xxxx`
- maximum network address number: `0~2^14` (16-2)
- maximum host address number: `2^16 - 2`

#### ✔️ Class C

> network part `24bits(3bytes)` ➕ host part `8bits(1byte)`

- start with `110`
  - `110x xxxx. xxxx xxxx. xxxx xxxx. xxxx xxxx`
- maximum network address number: `0~2^21` (24-3)
- maximum host address number: `2^8 - 2`

- 🛠️ normally used for public IP ddress

<br>

> **Why is class C used for public IP address?** <br>
>
> > as class A, B can have too many hosts <br>

#### ✔️ Class D

- for multicast

#### ✔️ Class E

- for future uses

## 📌 CIDR

> Classless Interdomain Routing

- routing strategy
- more flexible than classes
- subnet portion of address of arbitary length
- format: `a.b.c.d/x`
- `x`: first number of bits, `subnet(network)` part of address

<img width="513" alt="image" src="https://github.com/user-attachments/assets/db286476-bd98-4a86-82e9-97e7a06744eb">

- 👍🏻 more flexible divide IP address
- 👍🏻 more efficiently use IPv$

## 📌 DHCP

> Dynamic Host Configuration Protocol <br>
> protocol for host to get IP address <br>
> automated process of assigning IP address <br>

<img width="711" alt="Screenshot 2024-09-11 at 19 14 54" src="https://github.com/user-attachments/assets/8717d3fa-83f1-4dee-a594-c75a0fa20257">

#### ✔️ Two ways of getting IP address

- device configure IP address manually
- DHCP

- server-client protocol
- UDP
- port 67, 68
- If a new device connects to network, DHCP assigns IP address to the device
- maintain unique IP address for each hsot

**1. DHCP Discover message**

- new host connects to network
- at this momemnt
  - the host does not know the IP address it will be connected to
  - thus, source IP address is `0.0.0.0`(PC has had no IP address until now)
  - the host does not know DHCP adress
  - thus, destination IP address is `255.255.255.255`(for broadcasting)
  - thus, sends **broadcsting** to send message to DHCP
- sends **DHCP discover message**

**2. DHCP offers a message**

- upon recieving message from host, DHCP sends message to host
- server IP is specified in message packet to identify the server
- source IP address is `DHCP server IP address`
- destination IP address is `255.255.255.255`(broadcast IP address)

**3. DHCP request message**

- host recieves DHCP offer message
- host produces ARP to check if there are any other host with same IP address
- host sends` DHCP request`
- source IP address is `0.0.0.0`(PC still has no IP address)
- destination IP address is `255.255.255.255`(for broadcasting)

**4. DHCP ACK message**

- upon ` DHCP request`, DHCP server sends DHCP ACK to check requested parameters
- now, host has IP address provided by DHCP server

## 📌 Private IP

✔️ **Two types of IP address**

- public IP
- private IP

✔️ **Private IP**

> internal address of device that is not routed to internet

- IP only for local network
- private IP is non-routable on internet(not open to outside)
- serach, access is impossible from outside
- private IP is only used within private network

- private IP can begin with

  - 192.168.xxx.xxx
  - 172.10.xxx.xxx
  - 10.xxx.xxx.xxx

- 👍🏻 more security within particular network
- 🛠️ used for internet wired/wireless connection

## 📌 NAT

> Network Address Translation <br>
> translate public IP to private IP <br>

- use private IP in private network
- use public IP to access Internet
- NAT: allow multiple device to access Internet through single public address

<img width="562" alt="Screenshot 2024-09-11 at 23 41 55" src="https://github.com/user-attachments/assets/ac7862c3-8c62-4dad-9244-e7cdae714bbd">

**0. Environment**

- router IP: `138.76.29.7`
- PC private IP: `10.0.0.1`

**1. host send from private IP**

- host with private IP `10.0.0.1` requests web page to
- web server with public IP `128.119.40.186(port 80)`

- host sends its private IP with port `3345`

**2. NAT recieves, translates**

- NAT translates private IP into public IP
- create port `5001`
- translate to public IP `138.76.29.7`

**3. Web server replies**

- web server will reply to public IP `138.76.29.7`
- and port `5001`

**4. NAT translate**

- translate public IP to private IP `10.0.0.1`

## 💡 Get network address, broadcast address

> ❓ My computer IP is `165.132.120.10` <br>
> subnet mask is `255.255.252.0` <br>
> What is my network address? and broadcast address? <br>

- `255.255.252.0` ➡️ `1111 1111.1111 1111.1111 1100.0` ➡️ 1이 22개
- 따라서 `165.132.120.10/22`
- `165.132.120.10` ➡️ 이진수로 나타낸 다음 ➡️ 앞에서 부터 22개
- 8 + 8 + 6개니까
- 120 ➡️ `01111000` ➡️ `011110` ➡️ 120

- thus, network address is `165.132.120.0`
- broadcast address is `165.132.120.255`

> ❓ My computer IP address is `165.132.120.10` <br>
> subnet mask is default `255.255.0.0` <br>
> What is my network address? and broadcast address? <br>

- network address: `165.132.0.0`
- broadcast address: `165.132.255.255`

> ❓ My computer IP address is `165.132.120.10` <br>
> subnet mask is default `255.255.255.0` <br>
> What is my network address? and broadcast address? <br>

- network address: `165.132.120.0`
- broadcast address: `165.132.120.255`

> ❓ My computer IP address is `192.168.51.111/20` <br>
> Is my IP address private?

- yes

> ❓ My computer IP address is `192.168.51.111/20` <br>
> What is the network address? and broadcast address? <br>

- 51 ➡️ `00110011` ➡️ 20= 8 + 8 + 4니까 `0011`
- network address: `192.168.48.0`
- broadcast address: `192.168.48.255`

> ❓ My computer IP address is `192.168.51.111/20` <br>
> Is `192.168.60.211` on the same network?

- 60 ➡️ `00111100` ➡️ 앞에 4자리 `0011`
- yes

> ❓ Can I assign IP address to `192.168.63.255` <br>

- No. Cannot assign IP address to broadcasting address

> ❓ What is the network mask of `192.168.51.111/20`?

- first 20 digits of binary number in 1
- `1111 1111.1111 1111.1111 0000.0000 0000`
- thus, `255.255.240.0`

> ❓ Can `192.168.48.1` be the gateway of `192.168.51.111/20` network?

- Yes.
- all other addresses that are not broadcast or network can be gateway

## 🆚 Gateway

✔️ **router**

- route data packet in **similar** networks
- OSI layer 3, 4
- NAT, DHCP

✔️ **gateway**

- connect two network, different protocols as a translator
- connects two **dissimilar** networks
- OSI layer 5
- network access control, protocol conversion

## 🆚 Mac address

✔️ **Mac address**

1. Physical Identifier

- physical identifier: identifier for NIC card on local network
- identify physical device itself on local network

2. Layer 2

- datalink layer
- switch, bridge
- make sure data is sent to correct physical device on local network
- smame network

3. Format

- 48-bit number
- example: `00:1A:2B:3C:4D:5E or 00-1A-2B-3C-4D-5E`

✔️ **IP address**

1. Logical Identifier

- logical identifier: identifier of device connected to network(Internet)
- device location on network that uses Internet Protocol

2. Layer 3

- network layer
- router
- different network

3. Format

- 32-bit number(IPv4) or 128-bit number(IPv6)
- example: `192.168.1.1`, `2001:0db8:85a3:0000:0000:8a2e:0370:7334`

✔️ **Address Resolution Protocol**

- device use ARP to map IP address to MAC address
