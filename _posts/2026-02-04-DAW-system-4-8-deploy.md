---
title: 4.8 Deployment of VM
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

## ✅ Deployment of VM

> deployment in VM = take a VM to a different computer

[![Screenshot-2026-02-04-at-15-16-46.png](https://i.postimg.cc/RZthpV7s/Screenshot-2026-02-04-at-15-16-46.png)](https://postimg.cc/9DWcr2NZ)

## 1️⃣ Create a `.ova` file

> ova: Open Virtualization Appliance

- open: standard, everybody can use it
- `.ova` file is open, standard
- `.ova` file is like taking `vbox` and `vdi` and making a **compressed** folder

#### 💡 step by step of using `.ova` file for deployment

- 1️⃣ Create the `.ova` file from host 1
- 2️⃣ Then send the compressed file to host 2
- ❓ How can I send the `ova` file?
- (1) using a USB, external disk
- (2) use cloud
- (3) use massive transfer platform: file sharing platform, then download
- 👀 like `dropbox`, `Drive`, `eTransfer`, `Mega`...
- 3️⃣ In host 2, import the `ova` file

#### 👎🏻 Problems of using `ova` file method for deployment

- the `ova` file contains the settings of the original computer
- so when use the `ova` in the new host,
- the settings have to be modified, need to be updated for the host 2
- adopt the `vbox`

#### 🛠️ When to use `ova` method

- when all computers are the same
- like in a company
- many companies can have `Windows + LTSC(longterm, no updates)`
- so that all company computers are identical

#### 💡 How to create `ova file` in host 2

- 1️⃣ turn machine off
- 2️⃣ `archivo > export`

[![Screenshot-2026-02-04-at-17-01-11.png](https://i.postimg.cc/sDwm1dwZ/Screenshot-2026-02-04-at-17-01-11.png)](https://postimg.cc/crtw5jqs)

- 3️⃣ select the machine you want to create the `ova` file
- 4️⃣ decide if you want to contain the `iso` inside the `ova` file

[![Screenshot-2026-02-04-at-15-36-31.png](https://i.postimg.cc/QCmsLy8j/Screenshot-2026-02-04-at-15-36-31.png)](https://postimg.cc/kR2LKwRH)

- ❓ when to contain the `iso` inside the `ova`
- when you did not install
- so if you are finished with installing, do not contain it
- 5️⃣ do not change the name of the `ova`
- 6️⃣ the `ova` file is always stored in the `documents folder` in the user `c:\usuarios\<username>/Documents`
- many ppl try to find the `ova` in the virtual box folder, `ova` is inside Documents folder
- 7️⃣ if the `ova` is for an official, comercial purpose(if I am trying to sell this `ova`), you add comments

[![image.png](https://i.postimg.cc/150VXmtN/image.png)](https://postimg.cc/QHtdnrcX)

- url: url that you will upload the `ova`
- 8️⃣ then click on terminal

#### 🟧 ova is orange

- vbox: 🟦 settings
- vdi: 🟥 harddisk
- extension pack: 🟩
- ova: 🟧 ova

#### 💡 in host 2, import

[![Screenshot-2026-02-04-at-17-02-00.png](https://i.postimg.cc/NFQ8fpXn/Screenshot-2026-02-04-at-17-02-00.png)](https://postimg.cc/cg5tF7X7)

[![Screenshot-2026-02-04-at-17-02-21.png](https://i.postimg.cc/DyyQ9pnq/Screenshot-2026-02-04-at-17-02-21.png)](https://postimg.cc/t7wVP51T)

- in host 2, you have to import the `ova` file
- so go to the VM, and navigate to `import`
- dont change any settings
- but make sure: MAC address
- **MAC address**: choose option **corresponding** to the number of the VM interconnected

[![Screenshot-2026-02-04-at-17-02-55.png](https://i.postimg.cc/Y9HYbbdt/Screenshot-2026-02-04-at-17-02-55.png)](https://postimg.cc/d75h0mMf)

#### ⭐️ Important note

- when you use `ova` method
- remeber you have to adapt the `vbox` settings to your computer
- according to host2

#### 👎🏻 Back and forth and Rewriting

- Back and forth:
- when you try to import the updated `ova` and you alredy have the VM installed
- it will say "This ova already exsits"
- 👉🏻 so you will have to **overwrite** the original VM
- 👎🏻 Overwrite is bad for secondary memory, harddisks
- haddisks will lose elasticity

#### 💡 OCI

- Oracle Clouding Interface
- so oracle offers their clouding service for their `ova`
- If you want to use OCI instead of `export > archivo` for creating a normal `ova`
- do `machine > exportar a OCI`

## 2️⃣ Send/Move host1 complete folder to the host2

#### 💡 How to send the folder

- 1️⃣ do `right click > mostar en explorador`
- 2️⃣ go one folder up, then you can take the whole folder
- 3️⃣ now send the whole folder to the host2
- 4️⃣ In host 2, you have two options
- (1) Fast deployment
- (2) Slow deployment

#### ⭐️ Fast deployment

- double click on `vbox`
- 👎🏻 if the `vbox` is **not compatible** between host1 and host2
- you will get an error, aborted
- does not give you the opportunity to adopt the settings

#### ⭐️ Slow deployment

- in host 2 VirtualBox, `maquina > anadir`
- then you can navigate to the concete `vbox`
- the scaffold will appear
- then you can modify the settings, modify the `vbox`

#### 👎🏻 Back and forth and Rewriting

- same problem with the `ova`

## 3️⃣ Synchronized

#### 👍🏻 Synchronized

- do not have the problem of back and forth and rewriting
- whatever I do to the VM host2 will be applied, kept for host1

#### 💡 How to use synchronized method

- you take the VM to an external disk, USB
- create in host2 **a link/an access** to that VM, inside the host2
- so that USB is the VM
- 👍🏻 each computer will be a perfect access to the VM
- the VM will always be the same
- 👍🏻 and you always carry the VM in your USB

- But to create a VM inside the external disk is slow
- So you can create the VM in the internal disk
- and copy it to the external disk
- then create the access in host2

#### 💡 How to create a new access to my machine in USB

- 1️⃣ `maquina > new`
- 2️⃣ Name: should be the same as the original machine
- 3️⃣ Folder: always `C:`
- remember, you are just creating an access, not a new machine.
- the access is in your host2
- folder should be `C:`
- 4️⃣ `iso`: add it, VirtualBox makes adding `iso` mandatory, obliged
- but we are not going to use the iso, so just add any iso
- purpose: to continue with Virtual Box, to omit unattended iso
- Virtual Box does not let you omit unattended installation unless u add an iso
- 5️⃣ Hardware: allocate how much resource of host2 you will give to the VM
- allocate half of RAM, cores
- 6️⃣ Harddisk: do not create a new `vdi`
- remember, you are just creating an access, not a new machine.
- you navigate, and use the existing `vdi`
