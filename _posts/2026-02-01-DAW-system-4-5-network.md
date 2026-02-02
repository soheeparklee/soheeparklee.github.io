---
title: 4.5 Connect VM to the network
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

## ✅ Bridge Networking

> Each VM has its own IP address <br>
> and the VM's IP address is different from the host

- 👍🏻 each machine has its own traffic

- `RJ45 + ethernet wire(if wired)` or `wireless connection` belong to the RM
- the bandwidth is shared by the RM and the VM

```
⭐️ bandwidth: how many bits travel per second of that connection
mega bits per second
```

[![Screenshot-2026-02-02-at-17-17-36.png](https://i.postimg.cc/DzfLbxKN/Screenshot-2026-02-02-at-17-17-36.png)](https://postimg.cc/9DSr6t0P)

- 4 IPs, 4 traffic
- but only one wire,
- so all traffic share the bandwidth
- distributed by `percentage %`

- ❓ What if one machine goes very slow?
- 💊 you can resize the bandwidth distribution

## ✅ NAT mode

> Network Access Translation

[![image.png](https://i.postimg.cc/8zZsxD2V/image.png)](https://postimg.cc/RWnMHrCP)

- Only 1 IP for all RM and VM
- for the VM to access internet, has to go through RM
- the traffic is signed by the host
- so the RM will check the VM access to the internet
- the RM will control the connectivity

- 👍🏻 security
- 👍🏻 No connectivity problems, and RM will control all
- 👎🏻 If I want to do hacking with VM, I cannot as RM will know my IP

- ⭐️ **NATed**: there is only one IP, and it is used by all virtual machines

## ✅ Internal Network

[![image.png](https://i.postimg.cc/kGgp1Q8p/image.png)](https://postimg.cc/HcFzj76w)

- **RM**: connected to Internet, with its own IP
- can connect to Internet
- Anfitrion: RM

- **VM**: some VMs create an internal, isolated network
- Invitado: one virtual machine, acting as a boss for the internal VMs
- all VMs are connected to the boss VM, invitado

- It is similar to creating a VPN(Virtual Private Network) with VMs
- 🛠️ Used for company intranet

## ✅ Host Mode

[![Screenshot-2026-02-02-at-17-28-43.png](https://i.postimg.cc/HLSZJJFM/Screenshot-2026-02-02-at-17-28-43.png)](https://postimg.cc/t1xtwgqR)

- VM is connected to the RM
- but connection to internet is lost
- nobody has connection to the internet
- only connection between VM and RM
- 🛠️ Designing a secret project
- so that spies cannot look at me!

## ✅ No connectivity

[![Screenshot-2026-02-02-at-17-30-49.png](https://i.postimg.cc/c1fR2gX0/Screenshot-2026-02-02-at-17-30-49.png)](https://postimg.cc/ThY5WPz4)

- nobody has connection to the internet
- no connectivity between VM and RM
- 🛠️ Used for VMs that spy on your computer, without being noticed by the RM
- 🛠️ Virtual malware
