---
title: Load Balancing
categories: [Computer Science, Network]
tags: [] # TAG names should always be lowercase
---

## ✅ Load Balancing

> sharing the work(load) to more than two servers

network connection ⬆️

- scale-up: increase capability of hardware
- scale-out: divide work among several servers ➡️ **Load balancing**

✔️ **Load Balancing**

- locate load balancer between client and server
- if one server is full, load the work to another server
- solve the problem of overlaoding
  <br>

> How does a load balancer choose a server?
>
> > - Round Robin: CPU scheduling round robin method
> > - Least connections: choose the server with least connection
> > - Source: Hash user IP and distribute(same user will always have same server)
