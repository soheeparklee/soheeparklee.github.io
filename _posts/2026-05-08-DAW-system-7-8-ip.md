---
title: 7.8 IP address
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

CC by Aru

## ✅ IP Addresses (IPv4)

- The IPs discussed here are IPv4.
- IPv6 exists but is less widespread.
- IPv6 addresses are longer.

---

## ✅ What is an IP Address?

- An IP address identifies connections/devices in a network.

### ☑️ Structure of IPv4

- 4 pieces of 8 bits.
- 4 octets.
- Total = 32 bits.
- Followed by `/number` (prefix index).

### ☑️ Binary to Decimal Conversion

- Uses powers/weights of 2.

#### ✔️ Example

- `11000000.10101000.00001010.00000100 /24`

### ☑️ Conversion

- `128 + 64`
- `128 + 32 + 8`
- `8 + 2`
- `4`

### ☑️ Decimal Result

- `192.168.10.4 /24`

---

## ✅ IPs in Communication

- IP bits travel in:

  - packets
  - headers

- Every communication on the internet includes IP information.

---

## ✅ Devices with IP Addresses

- Computers
- Routers
- Switches
- Modems
- Any network-connected device

### ☑️ Switch

- Creates/manages connections.
- Usually represented as a cube with arrows.

### ☑️ Router

- Finds best path for packets.
- Uses routing table.

---

## ✅ Identifying Networks and Hosts

- IP identifies:

  - physical location
  - logical location

### ☑️ Prefix Index / Subnet Mask

- Number after `/`.
- Indicates how many bits identify the network.

### ☑️ Remaining Bits

- Identify the host/device inside the network.

---

## ✅ Example of Net and Host

#### ✔️ Binary IP

- `00001010.11001010.00111010.01011010 /16`

### ☑️ Decimal Conversion

- `10.217.58.90 /16`

### ☑️ Net Portion

- `10.217.0.0`

### ☑️ Host Portion

- `0.0.58.90`

---

## ✅ Subnet Mask

- Alternative representation of prefix index.

### ☑️ Process

- Write:

  - as many `1s` as prefix bits
  - remaining bits as `0s`

- Convert to decimal.

#### ✔️ Example

- `11111111.11111111.00000000.00000000`

### ☑️ Decimal Form

- `255.255.0.0`

---

## ✅ IP Address Management Organizations

- 5 major organizations manage/sell IP addresses worldwide.

### ☑️ Examples

- ARIN → North America
- RIPE → Europe

### ☑️ ISP

- ISP = Internet Service Provider.
- ISPs buy IP ranges from these organizations.

---

## ✅ IPv4 Classes

- There are 5 IP classes.

---

## ✅ Class A

### ☑️ Characteristics

- `/8`
- 8 bits = network
- Remaining bits = hosts

### ☑️ First Octet Range

- `1 → 126`

### ☑️ Notes

- Very few networks possible.
- Huge number of hosts.
- Used by massive companies.
- Very expensive.

### ☑️ Subnet Mask

- `255.0.0.0`

### ☑️ Example

- `100.x.x.x`

---

## ✅ Class B

### ☑️ Characteristics

- `/16`
- 16 bits network
- 16 bits hosts

### ☑️ First Octet Range

- `128 → 191`

### ☑️ Subnet Mask

- `255.255.0.0`

### ☑️ Example

- `150.x.x.x`

---

## ✅ Class C

### ☑️ Characteristics

- `/24`
- 24 bits network
- 8 bits hosts

### ☑️ First Octet Range

- `192 → 223`

### ☑️ Notes

- Very common in companies.

### ☑️ Subnet Mask

- `255.255.255.0`

### ☑️ Example

- `200.x.x.x`

---

## ✅ Class D

### ☑️ Purpose

- Multicast communication.

### ☑️ First Octet Range

- `224 → 239`

### ☑️ Example

- `225.x.x.x`

---

## ✅ Class E

### ☑️ Purpose

- Educational/training use.

### ☑️ First Octet Range

- `240 → 254`

### ☑️ Example

- `250.x.x.x`

---

## ✅ Local Host (LH)

### ☑️ Characteristics

- Starts with `127`.

### ☑️ Purpose

- Testing connections.
- Testing services locally.

---

## ✅ Communication Types

### ☑️ Unicast

- One-to-one communication.

### ☑️ Broadcast

- One-to-all communication.

### ☑️ Multicast

- One-to-some communication.

---

## ✅ Special IP Classes

---

## ✅ Local Host

- Starts with `127`.

---

## ✅ APIPA

### ☑️ Characteristics

- Starts with `169`.

### ☑️ Meaning

- No valid IP assigned.
- Connection unreachable.

### ☑️ Causes

- No signal.
- DHCP failed.
- Weak connection.

### ☑️ Notes

- Used automatically in emergencies/weak channels.

---

## ✅ Private IPs

### ☑️ Private Ranges

- `10.x.x.x`
- `172.x.x.x`
- `192.x.x.x`

### ☑️ Characteristics

- Only visible inside LAN (Local Area Network).

### ☑️ External Communication

- Others usually see:

  - proxy IP
  - router IP

---

## ✅ Default Gateway

- Usually the router IP.
- First hop of communication.

### ☑️ Used When

- No proxy exists.
- Device has private IP.

---

## ✅ The Triplet

### ☑️ Components

- IP address
- Subnet mask
- Default gateway

### ☑️ Purpose

- Fully identifies:

  - network
  - host
  - fallback communication path

---

## ✅ Static vs Dynamic IPs

### ☑️ Static IP

- Never changes.
- Triplet visible in commands.

### ☑️ Dynamic IP

- Assigned by DHCP.
- Triplet not usually visible.
