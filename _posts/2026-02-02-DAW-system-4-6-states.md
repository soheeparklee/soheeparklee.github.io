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
