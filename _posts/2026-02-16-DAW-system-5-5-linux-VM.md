---
title: 5.5 Install linux in VM
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

## ✅ Installation

- every release have same hardware requirements
- 🆚 flavors require different hardware requirements
- If you do not have the hardware requirements, change the flavor⭕️, not the release ❌

[![Screenshot-2026-02-16-at-16-36-29.png](https://i.postimg.cc/Hx64WXK6/Screenshot-2026-02-16-at-16-36-29.png)](https://postimg.cc/dkTT4kJC)

- (1) two cores
- (2) If you want to install Ubuntu in RM ➡️ minimum 4GB
- (3) If you want to install Ubuntu in VM ➡️ minimum 2GB, recommended 4GB

- (4) 25GB of harddrive
- (4) 8.6GB of harddive is minimum for flavor `"L"ubuntu`
- (5) 3D accerleration is mandatory
- (5) 256MB of Video RAM is necessary if you want to use linux in graphic mode

  - 💊 use linux in command mode
  - for ubuntu experts, use in command mode
  - for standard users, use `"L"ubuntu or "X"ubuntu` if you have problems with grpahic

- (6) High resolution, must have `SVGA`
- if possible, `VM SVGA`

- 1️⃣ But when I choose `VM SVGA` the VM does not work, and the `iso` might not boot
- bc the `SVGA` is asking for too much resources from my RM
- the RM is boycotting the VM
- if my RM has less than `512MB`(in order to give half `256MB` to the VM)
- I will have this problem
- 💊 still, you need to give `SVGA` in order to use Ubuntu
- 💊 so give `Vbox SVGA`, instead of `VM SVGA`

- 2️⃣ if `Vbox SVGA` still does not work
- give `Vbox VGA`
- but you will not see the graphics of ubuntu
- 💊 but, still you can control linux with command mode
- 👉🏻 that is why many ubuntu consoles do not offer graphic mode at all
- 💊 use commands!

- (8) give internet
- use `Bridge` or `NATed`
- `NAT`: one IP address for both
- `Bridge`: each RM, VM has their own IP address

```
❓ What happends if you are in bridge
and you are in Clara Del Rey and you have problem with internet
you lack IP address
and you try to install ubuntu
you machine is not connected to internet

- then change to NAT
- then you can share the NAT
```

- (9) If you are in systems that are limited in resources
- create VM in internal disk ⭕️
- do not created VM in external disk ❌
- you can create it internally, then deploy it on external

## 📌 Create VM for Linux

#### ✔️ RAM

- When while creating the VM
- When we install OS that require SWAP
- give miminum RAM
- so that SWAP can also be minimum
- later, after running and you see that you need more RAM, SWAP
- then allocate more RAM

[![image.png](https://i.postimg.cc/tJx3dT2g/image.png)](https://postimg.cc/p5P5R2NN)

#### ✔️ **EFI**

- for Linux EFI is not mandatory
- but if we decide to tick EFI
- linux will create its own `/boot/efi` partition
- if possible, tick EFI
- 👍🏻 EFI will enable stronger booting

[![image.png](https://i.postimg.cc/DzpLtsNL/image.png)](https://postimg.cc/KKL1TKx8)

#### ✔️ **Harddisk**

- if you give `dynamic`, the `dvi` will be only `2MB`
- so when installing OS, tick on `Reservar complementamente`
- always give full size of harddisk

- ⚠️ why you have `Disk Full error`
- 1️⃣ when you do not have `30GB` on your RM
- 💊 delete some files and apps and make some space on your harddisk
- 2️⃣ if the format of my harddisk is FAT32, as maximum is `4GB`
- 💊 harddisk should be formatted to exFAT, with backup

#### ✔️ **Boot order**

- If you tick EFI
- boot order cannot be modified in VirtualBox
- you can modify in the EFI

- 💊 If you want to change this
- uncheck `EFI` one second
- then change boot order
- then again tick `EFI`

[![image.png](https://i.postimg.cc/zv9GWwfJ/image.png)](https://postimg.cc/q6xrH3nY)

#### ✔️ I/O APIC

- we should tick bc
- we have two cores
- and we are 64 bits

#### ✔️ Secure boot

- never use Secure boot for linux
- it will not boot linux

#### ✔️ Memoria de video

- give half, if you cannot give 256GB

#### ✔️ VideoRAM

- In systems that need 3D acceleration as requirement like Ubuntu,
- when you enable 3D acceleration
- the system adds more video RAM
- it takes the video RAM from the SWAP
- the system dedicates part of the harddisk to the RAM, for the video RAM ➡️ creates `video SWAP`
- thanks to the SWAP ➡️ creates `video SWAP`
- we can give more to the VM

- 👉🏻 3D on
- 👉🏻 when videoRAM increases double with video SWAP from `128MB` to `256MB`
- 👉🏻 allocate half of videoRAM

[![Screenshot-2026-02-16-at-20-03-24.png](https://i.postimg.cc/GpYJszhB/Screenshot-2026-02-16-at-20-03-24.png)](https://postimg.cc/bGy27xn8)

[![Screenshot-2026-02-16-at-20-03-40.png](https://i.postimg.cc/MHZyNS0j/Screenshot-2026-02-16-at-20-03-40.png)](https://postimg.cc/47M7HjSJ)

- always play along with graphics
- to avoid invalid settings
- try to satisfy as many requirements as possible

[![Screenshot-2026-02-16-at-20-04-04.png](https://i.postimg.cc/hPjL0KPY/Screenshot-2026-02-16-at-20-04-04.png)](https://postimg.cc/Yj5LrKFN)

#### ✔️ Shared folders

- linux has a good system for shared folders
- activate shared folders with USB
- so for linux, create shared folders

#### ✔️ Attach a details screen

- After setting a virtual machine
- always ITIL to attach a details screen

## ✅ Final summary of the VM

[![Screenshot-2026-02-16-at-20-13-33.png](https://i.postimg.cc/gj4fbmCk/Screenshot-2026-02-16-at-20-13-33.png)](https://postimg.cc/K3k9nScd)
