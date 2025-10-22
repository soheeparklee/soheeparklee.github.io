---
title: Structure of Operating System
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

## ✅ Three types of structure of OS

- There are three types
- All the OS since year 2011 more or less, are evolving towards **Hybrid**

## 1️⃣ Monolithic

[![Screenshot-2025-10-22-at-16-36-57.png](https://i.postimg.cc/t4TxpNCH/Screenshot-2025-10-22-at-16-36-57.png)](https://postimg.cc/dLb19dyW)

- An OS is monolitic if the software is a huge block
- huge block of SW, unique, only one software
- and does all the fuctions, it is in charge of everything
- kernel is active/works

- 💡 **Kernel**: this huge one, unique software that does everything is called `kernel`

- over this kernel, you can install other applications for customers
- However, the kernel is unmodifiable 🙅🏻‍♀️
- 👎🏻 NOT flexible
- 👎🏻 NOT adaptable to your needs

  - cannot even change the color of your OS

- 👀 Windows is not monolithic ❌
- 👀 Symbian OS was monolithic
- 👀 airport tower OS is monolithic, use modified symbian OS

- 👍🏻 more secure
- as nobody can not change anything, more difficult to corrupt
- very secure

## 2️⃣ Micro kernel OS with `IPC`

[![Screenshot-2025-10-22-at-16-37-29.png](https://i.postimg.cc/15W8CVcR/Screenshot-2025-10-22-at-16-37-29.png)](https://postimg.cc/RNHCqFD2)

- the `kernel(SW)` is small
- you can add more/extra functionalities to the kernel

- 💡 **User servers:** These extra functionalities are called user servers
- installed to give extra services to the users
- you add more service to the kernels
- 👀 `Service pack` for windows
- when you add a service pack to windows, you are adding a user server, new functionality to kernel

- 👍🏻 more adaptative to user needs
- 👎🏻 less secure, kernel is not so protected
- 👀 Windows

- In `Micro kernel OS`, the kernel only gets orders/only gets disturbed only when there is high relevence
- so only when there is an emergency
- 💡 **IPC**` Inter Process Communications`: emergencies thrown to the kernel
- if there is one `IPC`, not very urgent
- but if there are hundreads of `IPCs`⬆️⬆️⬆️, big big emergency!
- the number of `IPC` that you see in a a terminal is an indicator of an **importance** of an error in the system
- as system experts, you need to check the **frequency** of `IPC`
- If the frequency is high⬆️, need to **mirror** the servers before the breakdown

- 👀 Whatsapp everyday at 2am, checks the `IPCs`
- to prevent failure, and became a more stable service

## 3️⃣ Hybrid

- mix of `Monolithic` and `Microkernel`
- the kernel is half size
- so the kernel works/active, has important functions
- and has user servers to help the kernel
- **security layer** between the server and the kernel
- In hybrid, there is NO `IPCs` ❌ , bc we have security layer

- 👍🏻 adaptative, as it has user servers
- 👍🏻 safe, as it has a security layer
- 👍🏻 even without installing so many user service, it is still active as kernel works

  - as kernel is working, you can run it wo so many user service

- 👀 Linux is hybrid structure

## ⭐️ Exam Questions

[![image.png](https://i.postimg.cc/65dfP0bB/image.png)](https://postimg.cc/562zYwMr)

```
❓ Look at the picture and answer some questions

❓ Are there user servers?
- only Microkernel and Hybrid

❓ Are there IPCs? Which one has IPCs?
- Only Microkernel has IPCs, so last picture
```

## ✅

## ✅
