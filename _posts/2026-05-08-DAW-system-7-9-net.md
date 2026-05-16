---
title: 7.9 Net Range

categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

CC by Aru

## ✅ Net Range

- From an IP + subnet mask, we can calculate all characteristics of the LAN.
- Net range = all important addresses inside a network.

---

## ✅ Example

- Host IP:

  - `192.168.10.10/24`

### ☑️ Identifying the Class

- `/24` + beginning with `192`
- Therefore:

  - Class C

---

## ✅ Type Address (Dirección Tipo)

### ☑️ Rule

- Replace all host bits with `X`.

### ☑️ Example

- `/24`
- 24 bits = network
- 8 bits = host

#### ✔️ Result

- `192.168.10.XXXXXXXX`

---

## ✅ Network Address

### ☑️ Rule

- Replace all `X` with `0`.

#### ✔️ Result

- `192.168.10.0/24`

### ☑️ Notes

- Identifies the network itself.
- No data should be sent here.

---

## ✅ First Host Address

### ☑️ Rule

- All host bits = `0`
- Last bit = `1`

#### ✔️ Binary

- `XXXXXXXX → 00000001`

#### ✔️ Result

- `192.168.10.1`

---

## ✅ Last Host Address

### ☑️ Rule

- All host bits = `1`
- Last bit = `0`

#### ✔️ Binary

- `11111110`

#### ✔️ Result

- `192.168.10.254/24`

---

## ✅ Broadcast Address

### ☑️ Rule

- Replace all `X` with `1`.

#### ✔️ Result

- `192.168.10.255/24`

### ☑️ Purpose

- Sending to broadcast IP sends message to all devices in network.

---

## ✅ Multicast Reminder

- Multicast requires:

  - Class D IPs
  - receiving hosts configured for multicast

---

## ✅ Example: Host 72

### ☑️ Binary Conversion

- `64 + 8 = 72`
- Binary:

  - `01001000`

#### ✔️ Result

- `192.168.10.72`

---

## ✅ Full Example of Address Range

### ☑️ Given IP

- `172.23.84.138/16`

---

## ✅ IP Address

### ☑️ Binary

- `10101100`
- `00010111`
- `01010100`
- `10001010`

### ☑️ Decimal

- `172.23.84.138/16`

---

## ✅ Subnet Mask

### ☑️ Binary

- `11111111`
- `11111111`
- `00000000`
- `00000000`

### ☑️ Decimal

- `255.255.0.0/16`

---

## ✅ Type Address

### ☑️ Binary

- `10101100`
- `00010111`
- `xxxxxxxx`
- `xxxxxxxx`

### ☑️ Decimal

- `172.23.xxxxxxxx.xxxxxxxx/16`

---

## ✅ Network Address

### ☑️ Binary

- `10101100`
- `00010111`
- `00000000`
- `00000000`

### ☑️ Decimal

- `172.23.0.0/16`

---

## ✅ First Host Address

### ☑️ Binary

- `10101100`
- `00010111`
- `00000000`
- `00000001`

### ☑️ Decimal

- `172.23.0.1/16`

---

## ✅ Last Host Address

### ☑️ Binary

- `10101100`
- `00010111`
- `11111111`
- `11111110`

### ☑️ Decimal

- `172.23.255.254/16`

---

## ✅ This Host Address

### ☑️ Decimal

- `172.23.84.138/16`

---

## ✅ Broadcast Address

### ☑️ Binary

- `10101100`
- `00010111`
- `11111111`
- `11111111`

### ☑️ Decimal

- `172.23.255.255/16`

---

## ✅ Standard vs Non-Standard Prefixes

### ☑️ Standard Prefixes

- `/8`
- `/16`
- `/24`

### ☑️ Non-Standard Prefixes

- More complicated.
- Use subnetting.

### ☑️ Subnetting

- Dividing a network into smaller groups/subnets.

---

## ✅ How to See Your IP?

### ☑️ Subnetting Identification

- Weird/non-standard masks usually indicate subnetting.

---

## ✅ Checking Private IP in Windows 10

### ☑️ Method 1

#### ✔️ Steps

- Control Panel
- Network and Internet
- Network and Sharing Center
- Active Network
- Details

---

### ☑️ Method 2

#### ✔️ Steps

- `Windows + R`
- `cmd`
- `ipconfig`

---

## ✅ Important Class Example

- If classroom internet fails:

  - nearby classroom may fail too

- Reason:

  - both may belong to same subnet.

---

## ✅ Checking Private IP in Linux

### ☑️ Commands

#### ✔️ Install Tools

- `sudo apt-get install net-tools`

#### ✔️ Show IP

- `ifconfig`

---

## ✅ Public IP

### ☑️ Meaning

- IP seen by other people/devices on the internet.

### ☑️ Usually Given By

- Proxy
- Router (if no proxy)

### ☑️ Location

- Usually points to ISP technical office location.

---

## ✅ Public IP Websites

- `https://vermiip.es/`
- `https://whatismyipaddress.com/es/mi-ip`

---

## ✅ Checking if an IP is Accessible

### ☑️ Command

- `ping`

### ☑️ Example

- `ping 8.8.8.8`

### ☑️ Notes

- `8.8.8.8` = Google DNS server.
- Big companies usually have fixed DNS servers.

---

## ✅ Ping and ICMP

### ☑️ Ping Uses

- ICMP protocol.

### ☑️ Purpose

- Check if destination is reachable.

---

## ✅ Connection Quality

### ☑️ Measured Using

- Response time.
- TTL (Time To Live).

### ☑️ Better Connection

- Lower response time compared to TTL.

### ☑️ Packet Loss

- Ideal:

  - `0%`

- Acceptable:

  - `20–30%`
