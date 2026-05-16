---
title: 7.10 Subnetting, Routing, PGP
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

CC by Aru

## 💡 Subnetting

- Subnetting = dividing a class network into smaller subnetworks.

### ☑️ Purpose

- Avoid wasting IP addresses.
- Organize companies into smaller groups/floors/departments.

---

## ✅ Examples of IP Capacity

---

## ✅ Class B (/16)

### ☑️ Number of Companies

- `2^16 = 65536`

### ☑️ Hosts per Company

- `2^16 - 2 = 65534`

### ☑️ Why Minus 2?

- One address = network identifier.
- One address = broadcast address.

---

## ✅ Class C (/24)

### ☑️ Number of Companies

- `2^24 = 16,777,216`

### ☑️ Hosts per Company

- `2^8 - 2 = 254`

---

## ✅ Why Subnetting Exists

- Large networks waste many IPs.
- Companies divide networks into smaller subnets.
- Subnets can be rented/shared.

---

## ✅ How to Subnet

### ☑️ Step 1: Decide Number of Subnets

#### ✔️ Example

- 8 floors → 8 subnets

---

### ☑️ Step 2: Find Number of Subnet Bits (a)

#### ✔️ Formula

- `2^a ≥ number of subnets`

### ☑️ Examples

#### ✔️ 8 Subnets

- `2^3 = 8`
- `a = 3`

#### ✔️ 9 Subnets

- `2^4 = 16`
- `a = 4`

---

## ✅ Step 3: Count Host Bits (X)

### ☑️ Example

- `/16`
- Host bits = `16 Xs`

---

## ✅ Step 4: Calculate Remaining Host Bits (b)

#### ✔️ Formula

- `b = x - a`

### ☑️ Example

- `b = 16 - 3`
- `b = 13`

### ☑️ Result

- Original `/16` network divided into:

  - 8 subnets
  - each subnet has `2^13 - 2` hosts

---

## ✅ Step 5: Transform Type Address

- Some `X` bits become `S` bits.
- `S` bits identify subnet.

---

## ✅ Example 2

### ☑️ Divide `192.168.34.0/24` into 2 subnets

---

## ✅ Step 1: Find a

#### ✔️ Formula

- `2^a ≥ 2`

### ☑️ Result

- `a = 1`
- 1 subnet bit (`S`)

---

## ✅ Step 2: Original Type Address

### ☑️ Original

- `192.168.34.xxxxxxxx`

### ☑️ Host Bits

- 8 host bits.

---

## ✅ Step 3: Calculate b

#### ✔️ Formula

- `b = 8 - 1`

### ☑️ Result

- `b = 7`

---

## ✅ Step 4: Transform Type Address

### ☑️ New Address

- `192.168.34.Sxxxxxxx`

### ☑️ New Prefix

- `/25`

---

# ✅ Subnet 0

### ☑️ Subnet Bit

- `S = 0`

### ☑️ Type Address

- `192.168.34.0xxxxxxx/25`

---

## ✅ Network Address

### ☑️ Result

- `192.168.34.0/25`

---

## ✅ First Host

### ☑️ Rule

- All `x = 0`
- Last `x = 1`

### ☑️ Result

- `192.168.34.1/25`

---

## ✅ Last Host

### ☑️ Rule

- All `x = 1`
- Last bit = `0`

### ☑️ Result

- `192.168.34.126/25`

---

## ✅ Broadcast Address

### ☑️ Rule

- All `x = 1`

### ☑️ Result

- `192.168.34.127/25`

---

## ✅ Important Warning

- In subnetting:

  - last host is not always `.254`
  - broadcast is not always `.255`

---

# ✅ Subnet 1

### ☑️ Subnet Bit

- `S = 1`

### ☑️ Type Address

- `192.168.34.1xxxxxxx`

---

## ✅ Network Address

### ☑️ Binary

- `10000000`

### ☑️ Decimal

- `192.168.34.128/25`

---

## ✅ First Host

### ☑️ Binary

- `10000001`

### ☑️ Decimal

- `192.168.34.129/25`

---

## ✅ Last Host

### ☑️ Binary

- `11111110`

### ☑️ Decimal

- `192.168.34.254/25`

---

## ✅ Broadcast Address

### ☑️ Binary

- `11111111`

### ☑️ Decimal

- `192.168.34.255/25`

---

## 💡 IPv4 Routing

### ☑️ Router

- Device with programmed routing table.
- Chooses best path for packets.

---

## ✅ Routing Table Columns

### ☑️ Destination

- Network you want to reach.

### ☑️ Mask

- Subnet mask of destination.

### ☑️ Gateway

- First hop taken by message.

---

## ✅ Gateway Rules

### ☑️ Gateway = `0.0.0.0`

- Direct wired connection exists.

### ☑️ Other Gateway

- Gateway = closest interface to next router.

---

## ✅ Router Connections

- One interface receives data.
- Another interface sends data to next hop.

### ☑️ Example

- Messages from LAN 1 to Router 2:

  - enter through ETH1.

---

## ✅ Routers Connected to the Internet

### ☑️ Characteristics

- Destination:

  - `0.0.0.0`

- Mask:

  - `0.0.0.0`

### ☑️ Meaning

- Represents outside world/internet.

---

## ✅ Internal Routers

- Can also contain `0.0.0.0`
- Gateway points to next router.

---

## ✅ Logical vs Physical Maps

### ☑️ Logical Map

- Includes:

  - devices
  - IP addresses

### ☑️ Physical Map

- Includes:

  - devices only
  - no IPs

### ☑️ Routing Tables

- Designed using logical maps.

---

## 💡 PGP

- PGP = Pretty Good Privacy.
- Uses:

  - public key
  - private key

- Used for encrypted emails.

---

## ✅ PGP Process

---

## ✅ Step 1: Create Keys

### ☑️ EducaMadrid

- `Configuración`
- `Claves PGP`
- `Crear`

### ☑️ Security Level

- `4096 bits` recommended.

### ☑️ Private Key

- Protected with strong password/hash.

---

## ✅ Step 2: View Keys

- Keys visible under:

  - `Claves PGP`

---

## ✅ Step 3: Send Public Key

### ☑️ Process

- `Redactar`
- Enable:

  - `Adjuntar mi clave pública`

- Send email.

---

## ✅ Step 4: Receive Other Person’s Public Key

- Destination sends back their public key.

### ☑️ Then

- Import their public key.

---

## ✅ Step 5: Verify Public Key

### ☑️ Check In

- `Claves PGP`

---

## ✅ Step 6: Send Encrypted Emails

### ☑️ Process

- `Redactar`
- Enable:

  - `Cifrar este mensaje`

- Send email.

---

## ✅ Receiving Encrypted Emails

### ☑️ Process

- Receiver gets encrypted message.
- Receiver uses own private key to decrypt.

---

## ✅ Public vs Private Keys

### ☑️ Public Key

- Shared with others.
- Used to establish secure connection.

### ☑️ Private Key

- Secret.
- Used to decrypt received messages.
