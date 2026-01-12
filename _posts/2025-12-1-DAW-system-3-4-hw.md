---
title: 3.4 HW specs for installing the OOSS
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

## ✅ What to check when installing OS

[![Screenshot-2025-12-01-at-16-20-08.png](https://i.postimg.cc/5NjbwT56/Screenshot-2025-12-01-at-16-20-08.png)](https://postimg.cc/KRX6b9H2)

⭐️ Important thing to check before installing OS

- type of BIOS
  - BIOS legacy
  - UEFI

#### 1️⃣ Architecture system

#### 2️⃣ Harddisk free capacity

- (you need to have the comply with the **minimum** capacity, but also the **recommended** capacity)

  - if Ubuntu 24 says that minimum is 20GB, but recommends 25GB
  - the extra recommended space is for **updates**
  - so always put recommended space
  - ✔️ in windows the updates are called `service pack`
  - ✔️ in linux, the updates are called `packages`

- 💡 recommended capacity is always **5GB** more than the minimum capacity
- 👀 windows say minimum 40GB
- so always install with 45GB!

#### 3️⃣ RAM

- need **minimum** RAM and **recommended** RAM
- Lubuntu(`light version of ubuntu`) has a minimum of 2GB of RAM, but recommends 4GB of RAM
- recommend to give the recommended RAM
- if you give more than the minimum RAM, you are more multitasking

- 💡 the recommended RAM is always **double** than the minimum RAM

```
❓ Recommended HD is for...
- updates

❓ Recommended RAM is for...
- multitasking

❓ You have a recommended HD for updates. You have a recommded RAM for multitaksing.
👉🏻 HD is +5GB, and RAM is double
```

#### 4️⃣ Clock speed, the clock frequency

- clock speed
- how many GHz your OS needs
- some OS needs a very fast clock speed

#### 5️⃣ GPU

- ⚠️ the GPU is not a graphics card(external)!
- GPU: the **internal** graphics processor of the CPU
- located inside the CPU
- many AI need GPU inside the CPU for the speed

#### 6️⃣ Installation media

- Specific ways of installation

- some OS needs specific ways of installation
- 👀 some OS cannot be installed with USB, some need to be installed through a network
- If a OS is installed through network, it is called `unattended installation`

#### ⭐️ BIOS

- important to check the BIOS

## ✅ Hardware specs/limits for OS

- Hardware specs to satisfy are called `Scaffold`
- so all features we saw above, , OS bits, harddisk, RAM, clock frequency, GPU, install media are all together called **scaffold**

## ✅ Apart from the scafold, there are things that make no sense

- multitasking of OS in monocore and monothreading CPU? NO.
- multitasking OS, do not buy them if you have a monothreading server. It will not work

- Apart from satisfying the scaffold, there are some things that do not make no sense...let's see them in 3.6
