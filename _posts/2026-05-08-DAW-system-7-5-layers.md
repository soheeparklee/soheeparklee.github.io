---
title: 7.5 Transport Layer 7.6 Network Layer 7.7 Link Layer
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

CC by Aru

## 💡 Layer 3: Transport Layer

- Service in charge of breaking information into pieces.
- Pieces must be less than or equal to 64 KB.
- Pieces can travel using:

  - TCP
  - UDP

- The protocol used depends on the application/service.

---

## ✅ TCP (Transfer Control Protocol)

- Reliable communication protocol.
- Every piece requires confirmation.
- Confirmations themselves are also confirmed.

### ☑️ TCP Communication Phases

#### ✔️ 1. Establishment of Connection (SYNC)

- Machines establish communication first.
- Uses 3-way handshaking.

### ☑️ Process

#### ✔️ Step 1

- Machine 1 requests communication with Machine 2.

#### ✔️ Step 2

- Machine 2 confirms request.

#### ✔️ Step 3

- Machine 2 also requests communication.

#### ✔️ Step 4

- Machine 1 confirms.

### ☑️ Notes

- Made of 4 messages functioning as 3.

---

#### ✔️ 2. Flow

- Data pieces begin transmission.
- Every sent piece requires:

  - ACK
  - ACK of the ACK

---

#### ✔️ 3. Termination (FIN)

- Communication is closed properly.
- Both sides:

  - announce termination
  - confirm termination

### ☑️ Notes

- Composed of 3 messages.

---

## ✅ Protocols that Use TCP

- FTP
- SMTP
- POP3
- IMAP

### ☑️ Reason

- They require ACK confirmations.

---

## ✅ UDP (User Data Protocol)

- Fast but unreliable protocol.

### ☑️ Characteristics

- No SYNC.
- No ACK.
- No FIN.
- Data is simply sent.

### ☑️ Important Note

- Nobody checks if pieces arrive correctly.

---

## ✅ Protocols that Use UDP

- TFTP

### ☑️ Reason

- TFTP does not use ACK confirmations.

---

## ✅ Ports to Remember

### ☑️ Socket

- Combination of:

  - IP address
  - port

- Represents:

  - machine + service

### ☑️ Example

#### ✔️ `192.10.8.6:25`

- Sending an email.
- Port 25 = SMTP/email service.

---

## 💡 Layer 2: Network Layer

- Layer responsible for mixing communication portions in channels and sending them.
- Usually handled by routers.

---

## ✅ IP (Internet Protocol)

- Checks whether IP addresses are correct.

---

## ✅ ICMP (Internet Control Message Protocol)

- Warns about communication problems.
- Detects dangerous events.

### ☑️ Examples

- Destination not reachable.
- Communication delay.

### ☑️ Ping Command

- Uses ICMP.
- Checks whether destination is safely reachable.

---

## ✅ ARP (Address Resolution Protocol)

- Identifies which IP belongs to which MAC address.

### ☑️ Characteristics

- Requires huge database containing:

  - machines
  - IPs
  - MAC addresses

### ☑️ Important Note

- Modifying database can detach IP from MAC.

---

## 💡 Layer 1: Link Layer

- Checks for transmission errors in bits.

### ☑️ FCS (Frame Checking Sequence)

- Redundancy information added to portions.
- Guarantees correction and error detection.

---

## ✅ Layer 1 Techniques

### ☑️ ECC

- Error Correction Code.
- Technique for correcting errors.

### ☑️ CRC

- Cyclic Redundancy Check.
- Technique for detecting transmission errors.

### ☑️ Important Note

- Layer 1 does not really use protocols/rules.
- Mainly based on correction and checking techniques.
