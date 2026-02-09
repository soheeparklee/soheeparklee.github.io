---
title: 4.6 States of VM
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

## ✅ States of the VM

[![Screenshot-2026-02-02-at-17-42-44.png](https://i.postimg.cc/ZnJxVJkB/Screenshot-2026-02-02-at-17-42-44.png)](https://postimg.cc/Q9n7MGdh)

### ✔️ Powerd off(Apagada)

### ✔️ Running(En ejecucion)

- using RAM, Harddisk...all resources in use
- if you want to run, should click on `start` button

### ✔️ Saved(Guardada/Hibernate)

- saves exact RAM state
- if you have a machine that is saved
- and if you want to go to the beggining
- clock on button `discard`
- `discard`: for unsaving machnies that you saved

### ✔️ Paused(Pausada)

- execution stopped, but machine stays in RAM
- give a small rest to your VM
- without freeing any resources
- but temporarily free CPU without closing apps

### ✔️ Aborted(Abortada)

- critical error here
- `Aborted` happens in two cases
- 1️⃣ `Aborted` happens bc the `vdi` file is not reachable

- ❓ **Why my VM cannot reach the `vdi`?**
- 1️⃣ maybe you deleted the `vdi` by mistake
- 2️⃣ my external disk has changed its name(its letter from `D -> E`)
- this happens when we create a VM in the external disk
- and the external changes its letter automatically
- and the state will be aborted
- bc the letter of the external disk depends on (1) the distribution of the internal disk
- (2) and the order of insertion
- 💊 change the letter back to what it was `E -> D`
- use command: `diskmgmt.msc`

- 2️⃣ `Aborted` also happens when I try to boot my VM in another RM
- with the old `vbox` file
- and I did not adopt the `vbox` file to my RM

### ✔️ Snapshot(Estado de instantanea)

- I have taken a shapshot, a recovery point
- shapshot = recovery point
- button `restore` is used for launching that recovery point
- button `take` is used for creating new recovery points

- when I take my machine to the recovery point
- the machine will not be in the state of "now"
- but it goes "back" to the past recovery point that was good

💡 **How to create a Snapshot**

- 1️⃣ Machine needs to be off
- 2️⃣ Click on the three dots

[![Screenshot-2026-02-02-at-17-53-18.png](https://i.postimg.cc/h40kgjtk/Screenshot-2026-02-02-at-17-53-18.png)](https://postimg.cc/Z0C7xJ3H)

- 3️⃣ click on snapshot `instantaea`
- 4️⃣ and take snapshot `tomar`

- all the snapshots are saved in the folder indicated in `configuration > general.advanced`

💡 **How to go to a recovery point**

- in order to go to a recovery point,
- select the recovery point
- click on `resotre`
- Note: `real state` should be **bold**, same as the recovery point

💡 **How to go delete recovery point**

- click on delete

## Snapshot 🆚 Screenshot

- Snapshot: recovery point of the machine bc now this state is perfect
- Screenshot: picture of your screen

[![Screenshot-2026-02-02-at-17-51-25.png](https://i.postimg.cc/BnvsRF5B/Screenshot-2026-02-02-at-17-51-25.png)](https://postimg.cc/Vd23CdVJ)

## ✅

## ✅

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
