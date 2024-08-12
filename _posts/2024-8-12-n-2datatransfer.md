---
title: How is data transferred over the network?
categories: [Computer Science, Network]
tags: [] # TAG names should always be lowercase
---

> **How is data transferred over the network?** <br>
>
> > break down the data into smaller units called packets <br>
> > the packets are sent from the source to desination <br>

<img width="567" alt="image" src="https://github.com/user-attachments/assets/996018d5-d479-486f-9521-97b921fff0ea">

## ✅ Packetization

Packets: <br>

- small segment of big original data
- `metadata(header)` ➕ portion of original data

## ✅ Routing

- route packet through the network
- router, switches

## ✅ Transmission Medium

- wires, cables
- Protocols: TCP/IP

💡 Protocol <https://soheeparklee.github.io/posts/n-3protocol/>

## ✅ Reassembly

- upon reaching destination, packets are reassembled in correct order
- in TCP, missing packets are retrasmitted

## ✅ Error Checking

- data integrity
- checksum
