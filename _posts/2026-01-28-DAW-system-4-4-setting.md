---
title: 4.4 Virtual Machine Setting
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

## ✅ Enable hardware watch(clock)

- Enable hardware watch(clock)
- you are getting the real machine data and time
- and you are giving that to the VM
- purpose: both VM and RM are syncrhonized
- when would you not want to synchornize the VM with the RM
- when you want to make a worm and play around

## ✅ Settings

- interruptions advanced
- USB
- synchronized

## 📌 System

### ✅ I/O APIC

[![Screenshot-2026-01-28-at-15-58-17.png](https://i.postimg.cc/dQWCksg3/Screenshot-2026-01-28-at-15-58-17.png)](https://postimg.cc/hhdvNBDR)

- If you have more than 1 core
- ✔️ must tick on `I/O APIC`
- bc you have two bosses(cores) interrupting
- after you start the OS, you will not be able to tick/untick the `I/O APIC`
- so becareful

### ✅ Execution Cap, Limite de ejecucion

- 1️⃣ If the execution is **100%**, there is no limit on the VM
- obviously, there will always be RAM, cores limit
- but other than those, there is no other limit

- 2️⃣ If the execution is **lower than 100%**, weakens the VM
- you do it to weaken the VM
- and give the power to the RM
- do it when the VM is so demanding, it is being too strong
- the VM is eating too much of your RM
- and the RM will run better

- 3️⃣ If the execution is **0%**
- you are making the VM stop/freeze
- which means 🟰 stopping
- it does not mean shutting down the VM ❌
- 🛠️ to protect your VM from VM malware
- 💡 VM malware: a VM that enters your computer without your permission, and starts running
- if you have a VM malware, you set the limitation cap of all the VMs to 0%
- then, go one by one and for only the VMs you know and are official, set it back to 100%

### ✅ PAE/NX

[Screenshot-2026-01-28-at-15-53-26.png](https://postimg.cc/vD32Rp32)

#### ☑️ PAE

- P: Physial
- A: Address ➡️ RAM
- E: extension
- ➡️ RAM Extension
- ➡️ SWAP
- use harddisk help

```
if RAM of the VM < 4GB then SWAP = RAM*2
if RAM of the VM = 4GB then SWAP = RAM
if RAM of the VM > 4GB then SWAP = RAM/2
```

- 💡 Note: Tick PAE, if RAM <= 4 GB
- Do not tick PAE only if RAM > 4GB
- Also try to save some SWAP, save some harddisk, if you do not need

- ❓ Why not tick PAE in every condition?
- bc PAE is taking space from your SWAP, your HD

#### ☑️ NX

> Non execute

- Flag that you exable for suspicious processes
- 👀 suspicious processes: process that tries to enter the OS in RAM
- then you enable NX flag for that processes
- if the antivirus sees a process with the NX flag,
- antivirus will capture it and **swap out three generations** from the process from the RAM
- in order to see the generations of the process,
- we need to do a query of the **processes table** in **OS in RAM**

#### ☑️ Why is PAE joined to NX?

- bc I need to capture the suspicious process and make queries
- and these queries are overusing the RAM
- and you are increasing the waiting time for the good processes
- so you use the help of SWAP
- so that standard processes do not have to wait so much

- 💡 Note: not all process needs protection in a computer
- 👀 pings can fail, but as it is repeated, it can fail as long as it is repeated

### ✅ Aceleration

[![Screenshot-2026-01-28-at-15-54-54.png](https://i.postimg.cc/TPy7SNmJ/Screenshot-2026-01-28-at-15-54-54.png)](https://postimg.cc/hJB1Qr2X)

- the RAM always gives more priority to the RM processes
- VM processes have worse priority
- if you activate accerleration,
- you balance all processes of both RM and VM

- tick means: balancing

## 📌 Pantalla

[![Screenshot-2026-01-28-at-16-02-31.png](https://i.postimg.cc/43LKKwF6/Screenshot-2026-01-28-at-16-02-31.png)](https://postimg.cc/NyXGS8tF)

### ✅ Pantalla-Memoria de video

- RAM of your graphics card
- modern graphics card have their own RAM for speed purposes
- memoria de video(Grpahic card) does DMA, they have their own RAM ⭕️
- it does not do PIO anymore ❌

```
PIO: doing the 8 in the RAM
DMA: Direct Memory Access, having your own RAM
```

- If I have a graphics card in my RM that has a RAM,
- how much of the total RAM of grphics card should I give to the RAM?
- **maximum half** of the RAM of grphics card to the VM

### ✅ Pantalla-numero de monitores

- several screens in your VM

### ✅ Factor de escalado

- how to split VM to several monitos
- scale: give 40% of VM to screen 1, give 60% of VM to screen 2...

### ✅ Pantalla-Graphic controller

- controlador grafico
- **resolution** you are giving to the screen of the VM

✔️ **Two types of resolution**

- `VGA` : low resolution, width and height lower than 800px
- `Super VGA`: high resolution, width and height more than 1000px
- we need `SVGA` for VM when the VM needs high resolution

- 🛠️ high resolution: when `GUI` is important
- we always need to check the specs of the `iso`
- if we have a VM buttons that disappears,
- it is bc you should have given `SVGA`, but you did NOT! 😱

- do not give a `SVGA` to an application that wants `VGA`
- it can make an `.iso` not to work, bc you are demanding too much resolution

✔️ **Two types of SVGA**

[![Screenshot-2026-01-28-at-16-16-15.png](https://i.postimg.cc/wTw34w99/Screenshot-2026-01-28-at-16-16-15.png)](https://postimg.cc/KRgZRrKW)

- `VMSVGA`: the perfect controller for that specific `.iso`
- `VBoxSVGA`: standard controller offered by virtual box, with minimum requirements

- if the `.iso` needs `VMSVGA`, do not give `VBoxSVGA`
- some `.iso` do not have `VMSVGA`, so you need to choose `VBoxSVGA`

### ✅ Acceleration 3D

- tick only if the specifications of the `.iso` demands on its specs
- 🛠️ for videos, movements
- do not tick by default

## ✅

## ✅

#### 1️⃣

#### 2️⃣

#### 3️⃣

#### 4️⃣

- 1️⃣
- 2️⃣
- 3️⃣
- 4️⃣
  👍🏻
  👎🏻

```
⭐️⭐️⭐️ EXAM ⭐️⭐️⭐️
❓
👉🏻
```

## 😱 VirtualBox installation errors

#### 1️⃣ c++ Redistinbutable Package Missing

- means an API is missing
- 💊 Go to microsoft webpage
- search and download the API
- then execture, double click
- and install the API

#### 2️⃣ Traces of previous verions found

- problems bc of traes/remains leftovers of the old version

- If you have a previous version of VM in the computer
- and somebody deleted the old version
- traes/remains of the previous version of Virtual Box

- ✔️ **Traces could be in two places**
- (1) in `C\Users\<user>\.VirtualBox`
- enter that folder
- empty the folder, delete all the content
- we only empty the folder when the error appears
- if there is no error, do not empty the folder

- bc if you delete that folder with no reason,
- you will delete all the access to that VM
- you will have to rebuild the accesses

- If the `.VirtualBox` does not exist, it means previous versions of VM does not exist

- (2) in `C\Windows\system32\drivers`
- and serach files
- starting by `VBox` with extension `.sys`
- `VBox*.sys`
- `*` is a wildcard
- then delete

- again, also only delete when you are having problem
- if you do not have any problem, but delete,
- you will lose access to the VM
- and before deleting, communicate with your team that you are deleting them

- Note: All applications can have trace problems
- 💊 look for traces inside the `C\Users\<user>\.<nameOfApplications>`

- Note: after deleting traces
- good practice to uninstall Virtual Box then install again

#### 3️⃣

#### 4️⃣

- 1️⃣
- 2️⃣
- 3️⃣
- 4️⃣
  👍🏻
  👎🏻

```
⭐️⭐️⭐️ EXAM ⭐️⭐️⭐️
❓
👉🏻
```
