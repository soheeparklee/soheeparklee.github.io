---
title: 7.3 TCPI / IP Model vs OSI Model
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

CC by Aru

## ✅ 7.3 TCP/IP Model vs OSI Model

## ☑️ Models and Protocols

### ✔️ What is a model?

- A **model** is a structure with layers used to explain how the internet works.

### ✔️ What is a protocol?

- A **protocol** is the set of rules followed by each layer.

### ✔️ Types of models

- **OSI Model (Open Systems Interconnection)**

  - Theoretical and more complex model.
  - Not used as much in real internet communication.
  - Structured in **7 layers**.

- **TCP/IP Model**

  - Most used model in internet connections.
  - Structured in **4 layers**.

---

## ✅ TCP/IP Model

## ☑️ Structure of the TCP/IP Model

### ✔️ 4th Layer — APPLICATION

- Set of rules explaining how applications work on the internet and how they are designed.
- Here we have the **data**.

### ✔️ 3rd Layer — TRANSPORT

- Set of rules guaranteeing communication between computers.
- Here we have the **segment**:

  - Source port
  - Destination port

### ✔️ 2nd Layer — INTERNET or NETWORK

- Set of rules ensuring data pieces find the best path.
- Here we have the **packet**:

  - Source IP
  - Destination IP

### ✔️ 1st Layer — ACCESS LAYER (LINK LAYER)

- Responsible for transforming information into binary and ensuring bits are sent.
- Here we have the **frame**:

  - Source MAC
  - Destination MAC
  - FCS (Final Checksum)

---

## ✅ Example with an Email Application

## ☑️ Data and Segments

- Suppose the application is an **email**.
- The information we want to send is called **data**.
- Data is broken into smaller pieces called **fragments**.
- When source and destination ports are added, fragments become **segments**.

### ✔️ Application Headers

- Each application is identified with a **header** attached to its data.
- Example:

  - Microsoft Office Online → application header.

---

## ✅ Ports and Services

## ☑️ Ports

- A host (computer connected to the internet) can run multiple applications.
- Different applications use different portions of the same connection called **ports**.

### ✔️ Examples of ports

- One port for:

  - Email
  - Web pages
  - Files

### ✔️ Closing ports

- Closing a port means forbidding one service.

### ✔️ Firewall

- The system that opens and closes ports is the **firewall**.

---

## ✅ Packets and IP Addresses

## ☑️ IP Addresses

- Many communication portions may use the same port number.
- To differentiate origin and destination, we use **IP addresses**.

### ✔️ Packet

- When source and destination IP addresses are added to a segment, it becomes a **packet**.

### ✔️ IP Characteristics

- IP is normally related to **location**, not device.

---

## ✅ MAC Address

## ☑️ MAC Address

- The **MAC address** uniquely identifies hardware devices.

### ✔️ NIC (Network Interface Card)

- The MAC address is found in the **NIC (network card)**.

---

## ✅ Headers

## ☑️ Purpose of Headers

- Headers are represented by the **baby blue sections in the diagram**.
- Every portion of communication must be identified with a header.

### ✔️ Types of Headers

- **Header 1:** Application header

  - Example: “Microsoft Office Online”

- **Header 2:** Service header

  - Indicates source and destination ports.
  - Example:

    - Email service
    - Webpage service

- **Header 3:** Network header

  - Contains:

    - Source IP
    - Destination IP

---

## ✅ Encapsulation

## ☑️ Definition

- **Encapsulation** is the process of adding headers to each portion of a message.

### ✔️ Why encapsulation is needed

- Internet portions do not always follow the same route.
- Portions need identification to reach the correct destination.

### ✔️ Routers

- The **router** finds the best route for message portions.

### ✔️ Weak Connections

- If a portion encounters a weak connection:

  - It may be delayed.
  - It may be lost forever.

---

## ✅ FCS (Final Checksum)

## ☑️ What is FCS?

- Each portion includes an extra tail called **FCS (Final Checksum)**.

### ✔️ Purpose

- Contains extra 0s and 1s for error detection.

### ✔️ Process

- Created by the transmitter.
- Checked by the receiver.

### ✔️ Controlled Communication

- FCS values must match.
- If they do not match:

  - The receiver tries to guess missing information.

---

## ✅ Frames

## ☑️ Frame Definition

- When source MAC, destination MAC, and FCS are added to a packet, it becomes a **frame**.

---

## ✅ Socket

## ☑️ Socket Definition

- A **socket** is a combination of:

  - IP address
  - Service

### ✔️ Important Note

- Intersecting a socket does not mean seeing the message.
- It means knowing:

  - The person
  - The use/service

---

## ✅ De-encapsulation

## ☑️ Definition

- **De-encapsulation** is the process of:

  - Removing headers
  - Removing FCS
  - Rejoining the data to recover the final message

### ✔️ Important Detail

- What travels through the wire contains:

  - Headers
  - Portions
  - FCS

---

## ✅ Multiplexing

## ☑️ Definition

- **Multiplexing** happens when:

  - Different portions
  - Of different services
  - From different people
  - And different applications
  - Travel together.

---

## ✅ Protocols

## ☑️ Protocol Rules

- The rules of each layer are divided into different **protocols**.
- Protocols act like different books of the same manual.

---

## ✅ OSI Model

## ☑️ General Information

- The OSI model is more complex than TCP/IP.
- It contains **7 layers**.

### ✔️ Main Difference

- In TCP/IP:

  - The Application layer is split into:

    - Application
    - Presentation
    - Session

- In TCP/IP:

  - The Link layer is split into:

    - Data Link
    - Physical

---

## ✅ OSI Model Layers

## ☑️ 7th Layer — APPLICATION

- Explains how the application works.

## ☑️ 6th Layer — PRESENTATION

- Controls the appearance/aspect of the application.

## ☑️ 5th Layer — SESSION

- Differentiates users inside the application.

## ☑️ 2nd Layer — DATA LINK

- Responsible for:

  - Adding MAC addresses
  - Adding FCS

## ☑️ 1st Layer — PHYSICAL

- Responsible for:
- Transforming bits into electricity or waves.
