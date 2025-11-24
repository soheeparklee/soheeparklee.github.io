---
title: 2.10 Optimization management
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

> Which are the CPU cache that you use for instructions that are very frequently used? <br>
> L1, L2 is replicated, L3 is not. If I have 4 cores, how many cache do I have? 4+4+4+1=13 <br>
> How do you call when two processes share loaded on the RAM? sharing <br>
> virtual memory is a mixture of? RAM and secondary memory <br>
> calculate size of VM and SWAP <br>
> 1/2 RAM <= SWAP area <= 2 RAM <br>
> 3/2 RAM <= VM <= 3 RAM <br>

> sysdm cpl <br>
> how do you call the flag that turns to 1 when the process is creating problems? <br>
> location of types of memory <br>

## ✅ Optimize the computer

- File Management: FAT32
- RAM management: Segment, Paging
- Process management: FIFO, SJF
- IRQ/DRG: DMA, Polling, PIO
- 👉🏻 All this make the computer overloaded
- 👉🏻 We need to optimize the computer

## ✅ Priority of computer components

1. CPU
2. Main Memory RAM
3. Secondary Memory (HDD, SSD)
4. Peripherals

- 👉🏻 We should optimize the computer components following this order

## 1️⃣ Lets help the CPU

🤒 **Problem that CPU suffers**

- 1️⃣ speed problem, being slow ➡️ bottleneck problem
- 2️⃣ temperature problem 💊 better refrigeration problem, better ventilation

### 💊 **Solve the bottleneck problem**

- Use **CPU cache**
- `CPU cache` is inside CPU
- The `CPU cache` is divided into 4 potions

💡 `CPU cache` **is stable**

- in general, `CPU cache` is not deleted
- `CPU cache` is stable(not deleted after session finishes)
- unless we manually clean them

#### **4 types of CPU cache**

[![Screenshot-2025-11-19-at-16-46-31.png](https://i.postimg.cc/gj7hN44K/Screenshot-2025-11-19-at-16-46-31.png)](https://postimg.cc/vxWDmrJ1)

[![image.png](https://i.postimg.cc/wTsR9X04/image.png)](https://postimg.cc/QHhdbTLc)

- **L1D**: Level 1 Data cache
- For _data_ that CPU uses very very often
  - 👀 `power of 2`, as in computer everything is in binary, it is stored in cache for frequent access
  - 👀 `1`s and `0`s
- ☝🏻 one L1D per core
- it needs to be close to the CPU, as it is used very often to the nueman machine
- 🐁 size: comparatively small, we just want them for super frequent things

- **L1I**: Level 1 Instructions cache
- for _instructions_ that we use very very often
  - 👀 standard mathametical instructions, like `sum`, `minus`, `mul`, `div`, `move(move data to another space)`, `sqrt(square root)`
- ☝🏻 one L1I per core
- 🐁 size: comparatively small, we just want them for super frequent things

- **L2**: Level 2 Cache
- Both instructions and data mixed together that we use quite often
  - 👀 mathametical operations that are not so frequent: `log`, `cos function...`
- 🐇 size: bigger than level 1, need to save both instructions and data
- 🗺️ location: located further away from the neuman machine, compared to level 1
- ☝🏻 one L2 per core

- **shared L3**: Level 3 Cache
- Both instructions and data we use sometimes
  - 👀 `loops, like for, while`
- 🐳 size: bigger, very big
- 🗺️ location: far from neuman machine
- ✋🏻 Shared level 3: Not one per core, shared among all the cores
- Level 3 cache uses front side bus

```
❓ If I have 8 cores, how many CPU caches do I have?

- L1D: 8
- L1I: 8
- L2: 8
- L3 : one shared L3 per core

👉🏻 in total 25 CPU cache memory
```

## 💡 ISA

- Instructions Set Architecture
- set of instructions that the CPU needs to exectute
- the instructions that come by default when I buy my computer
- factory settings of my CPU
- the instructions that the neuman machines do by default

- `CPU cache` helps `ISA`, as some of `ISA` instructions are stored in the `CPU cache`

```
❓ If I reset my computer to factory settings, pure nueman machine, am I deleting the CPU cache memory?
👉🏻 yes, we are deleting

❓CPU cache helps which of the following?
1. IPC to the kernel
2. ISA
3. IRQ
4. DRQ
👉🏻 ISA
```

## 2️⃣ Lets help the RAM

🤒 **Problem that RAM suffers**

- 1️⃣ problem of space: even smaller bc of `process table, pages table, vectors table, service routines` and above all, processes!

[![Screenshot-2025-11-19-at-16-56-13.png](https://i.postimg.cc/J7FKTQs5/Screenshot-2025-11-19-at-16-56-13.png)](https://postimg.cc/qg88qyXN)

### 💊 Sharing

[![Screenshot-2025-11-19-at-16-57-33.png](https://i.postimg.cc/JzLFqQF6/Screenshot-2025-11-19-at-16-57-33.png)](https://postimg.cc/D8x5f1nL)

- there are some common portions that several proecesses share
- 👀 `menu bar in word, excel, ppt are more or less the same`
- If some processes have some elements in common,
- then put the same elements just one time on the RAM
- and **share** it among the processes

- 👎🏻 the shared elements would be less secure
- as it can be accessed by several processes
- sharing can be deactivated

### 💊 Virtual Memory

✔️ **Some processes are ok to be slow and is not used so frequently**

- can be slow
- is not used all the time
- we do not need the process to be there all the time in the RAM

✔️ **Page File and SWAP area**

[![image.png](https://i.postimg.cc/3Nnxrwzd/image.png)](https://postimg.cc/hQQBpKDB)

- we can leave the process in a specific part of the _Harddisk(secondary memory)_
- called in **Page File** `windows/mac/android` and **SWAP area** in `linux`
- 👉🏻 in `page file/SWAP area` we store the pages of the process that
- we don't use very often
- and we do not need so fast
- like having an extra storage
- 👍🏻 makes the RAM **feel bigger** than it seems
- 👍🏻 Feels like **virtually**, I have more RAM

- its called swap, bc when you need it,
- it seems the process is inside the RAM
- But actually, the process is inside the hardddisk

- So in harddisk, it is generally for closed program
- but in SWAP part of harddisk, there are opened process

✔️ **Format for `Page File` and `SWAP area`**

- This area is in the secondary memory
- ⚠️ the format is different from starndard( NOT `FAT32`, `exFAT`, `NTFS`, `ext 2, 3, 4` ❌)
- the format of `Page File` and `SWAP area` is called **swap**
- as `Page File` and `SWAP area` is for helping the RAM, `swap format` is similar to the RAM

✔️ **Virtual Memory**

- VIrtual Memory = my RAM ➕ SWAP in Harddisk
- `VM 🟰 MM ➕ SWAP area(SM)`

✔️ **Calculate the VM**

- If RAM is small ⬇️ SWAP must be big ⬆️
- If `RAM < 4GB`, SWAP must be two times the RAM `SWAP = RAM * 2`
- If `RAM = 4GB`, SWAP must be same as the RAM `SWAP = RAM`
- If `RAM > 4GB`, SWAP must be half of the RAM `SWAP = RAM / 2`

```
❓ 3GB of RAM, my SWAP should be?
👉🏻 6GB

❓ Then how much is my VM?
👉🏻 9GB
------
❓ 4GB of RAM, my SWAP should be?
👉🏻 4GB

❓ Then how much is my VM?
👉🏻 8GB
------
❓ 16GB of RAM, my SWAP should be?
👉🏻 8GB

❓ Then how much is my VM?
👉🏻 24GB
```

⚠️ **Error we can get if we do not follow the VM caculation rule**

- If we follow these rules, we will never have a problem with the virtual memory
- However, if we do not follow these rules, we might get a problem

[![Screenshot-2025-11-19-at-17-34-44.png](https://i.postimg.cc/Xvm2hcJp/Screenshot-2025-11-19-at-17-34-44.png)](https://postimg.cc/sBP9GW5r)

- ⭐️ When you have a VM error, the error starts by `0x000000`
- cannot read instruction on `0x000000`
- if you see this error, you have a virtual memory problem

- this error occurs bc many OS take SWAP smaller than needed
- many OS prefer more pure HD than more SWAP
- 💊 deactivate the automatic VM supply(administración automatica memoria virtual)
- 💊 and supply VM manually

✔️ **Perfect limits for VM**

- `SWAP` should always be between half and double the size of the `RAM`
- `half of RAM` < size of swap < `double of RAM`
- if my RAM is big, if my SWAP small, SWAP is `half of RAM` my VM would be `RAM + RAM/2 = 1.5RAM`
- if my RAM is small, if my SWAP big, SWAP is `twice the RAM` my VM would be `RAM + RAM*2 = 3 RAM`
- Thus, the VM size should always be
- `RAM * 1.5` < size of VM < `RAM * 3`

- 👉🏻 This size of VM would avoid the problem of VM `0x` error

```
❓ I have 8GB of RAM. Study the minimum and maximum limits of VM so I do not get the VM error.
👉🏻 8 * 1.5 < VM size < 8 * 3
👉🏻 thus, 12GB < VM size < 24GB
👉🏻 as long as I guarantee that my computer makes VM from 12 to 24GB, I will never get the 0x error.
```

> 1/2 RAM <= SWAP area <= 2 RAM <br>
> 3/2 RAM <= VM <= 3 RAM <br>

- these formulas guarantee that we will not have the `0x000000` error
- if I keep this formula, I will protect my computer from having the `0x000000` error

✔️ **Command to solve the VM error**

```
sysdm cpl
```

- system setting commands start with `sys`
- all the commands that start with `sys` are for setting the system

- all the commands that contain/end with `dm` is for device management
- all the commands that end with `cpl` are commands that are reachable through the control panel

✔️ **How to run the commmand**

- ⚠️ This process very very hidden,
- need to open three windows!
- bc of security purposes

[![image.png](https://i.postimg.cc/pTqBKN42/image.png)](https://postimg.cc/nj97tWn5)

1. in order to run this command, press `windows key` and `R`

- then type the command `sysdm cpl`
- a new window appears

2. go to advanced options
3. Performance area
4. Configuration button
5. new window appears
6. Advanced options
7. Change button
8. new window appears
9. virtual memory
10. Untick the automatic administration
11. Choose custom size
12. custom size needs to include the limits for the `virtual memory`
13. So adopt the `virtual memory formula`
14. If we use this formaula, we protect the system from VM errros
15. initial size will be `1.5 * RAM, but in MB`
16. maximum size will be `3* RAM, but in MB`
17. we only manually choose the size **when we get the `0x000000` error**

- We should do this when we really have a problem, at the moment we have a problem
- So do not manually change the size when you do not have an error
- If we do it even if we do not have an error, we are stealing capacity of the HD when we do not need it, so why do it?

18. After writing the size manually, click on `accept ➡️ accept ➡️ accept three times`, and close all three windows
19. Restart the computer
20. Now you will not see the 0x000000` error!

✔️ **How do you find the size of the RAM?**

1. Open task manager(administrador de tareas)

- shortcut: `Ctrl` + `Alt` + `Supr`
- or `Ctrl` + `Shift` + `Esc`

2. Task Manager
3. Performance
4. Memory
5. You can find the size of the RAM in the top right corner

```
If my RAM is 8GB,

inicial size will be 8 * 1.5 = 12 GB
change to MB: 12 * 1024 = 12288 MB

maximum size will be 8 * 3 = 24GB
change to MB: 24 * 1024 = 24576 MB
```

## 3️⃣ Lets help the Secondary Memory

#### 💊 Harddisk Buffer

[![image.png](https://i.postimg.cc/dVqKVJqL/image.png)](https://postimg.cc/kBhHj3Rm)

- harddisk buffer is in the `Harddisk`
- buffer: **temporal storage** for making profit of a **data transaction**

- the portion that you need now ➡️ goes to the RAM
- the portion that you do not need now, but you took following the proximity principle ➡️ goes to the buffer

💡 **Proximity principle**

- when you open a program, most probably you will need more than that
- 👉🏻 open more, also the ones next to the pointed program
- 👀 if you opened ejercicio 1, you will also open 2, 3,4...
- the extra can be stored in the `harddisk buffer` to have it **closer** to you.

#### 💊 Web cache, Broswer cache

- when we download elements from the web and we visit web pages
- most probably, we will use the element/web page later
- store the elements in the broswer cache
- web cache is a folder in the harddisk
- when we empty the cache, we are emptying the web cache

✔️ **Two things you save in the web cache?**

- web cache saves the 1️⃣ history of web pages
- and components you have 2️⃣ downloaded from the web pages

✔️ **Where is broswer cache?**

- Harddisk

✔️ **How many web cache?**

- one folder per user
- one folder per browswer
- also the same for cookies, one folder per browser, one folder per user
- 🆚 cookies: my preferences/ web cache: my history, downloads

```
❓ If I have two users, and three web browsers, how many web cache do I have?
👉🏻 6 web caches
```

```
❓ When you delete the history in your browser, what are you deleting?
👉🏻 you are just deleting the list of visited web pages,
but not downloads, components history

👉🏻 so you are not fully deleting, you can still see downloads history
```

## 4️⃣ Lets help the Peripherals

🤒 **Problem that RAM suffers**

- 🐢 normally peripherals are slower than the other computer compoenents
- so we need to help peripheral speed

#### 💊 Peripherals buffer

[![image.png](https://i.postimg.cc/vmj0KwX7/image.png)](https://postimg.cc/v1r71jJD)

- specific folder
- in which the peripherals stores the pending documents
- and takes them at its own speed
- 👀 like the printer queue

- If the peripheral uses the `peripheral buffer`
- we say it is using `Buffering`

#### 💊 Spooling

[![Screenshot-2025-11-24-at-16-18-22.png](https://i.postimg.cc/zvNFmzh0/Screenshot-2025-11-24-at-16-18-22.png)](https://postimg.cc/qhm3ydj3)

- If the buffer is shared by several computers on the network
- one printer is shared by several computers
- we call it spooling
- same as buffer, but with several computers connected to one peripheral

## ✅ How can I protect my system?

- Due to optimization techniques, all the computer components are interconnected
- so one problem in one component can affect the whole computer
- 👀 If I have a problem in SWAP, will affect HD and also the RAM

✔️ **Stamp a process**

- when a process creates a problem in one component
- the process is **stamped**
- **Stamp a process: set a flag `NX: Non Execute` to 1**
- `NX` means `please, do not execute the proecss!`
- so when the process reaches another component,
- if `NX = 1`, the entrance will be blocked! forbidden

- Then the process that is stamped `NX` will be swapped out
- and if it is a malware
  - (the anti virus will tell you)
- 3 layer protection(me, my parent, my children)
- antivirus will expel the process and its 3 generations from the RAM

✔️ **Where is the `NX` flag?**

- the flag is stored inside the process table, in the OSRAM
- 👉🏻 way a protecting the system

## ✅ Type of memories

[![Screenshot-2025-11-24-at-16-26-30.png](https://i.postimg.cc/nzBNYLZC/Screenshot-2025-11-24-at-16-26-30.png)](https://postimg.cc/dkQWJwhY)

✔️ **ROM**: memory you can only read, you cannot modify

- these days, the only element that is `ROM` is `BIOS`
- find the battery, and the `BIOS`/`ROM` will be next to the battery

✔️ **SM/EM**: HDD, SSD

- files when they are closed, stored

✔️ **RAM, MM**

- opened processes
- Random: bc processes will be placed randomly, incontinguously, not ordered

✔️ **VM**:

- combination of memory both in HD(SWAP) and RAM
- Can you point to the VM physically? 👉🏻 NO, VM is a concept

✔️ **CPU Cache:**

- inside the CPU

✔️ **Web Cache:**

- in the harddisk, it is a folder

✔️ **Disk Buffer:**

- in the harddisk

✔️ **Buffering and Spooling:**

- in the peripherals

✔️ **Disk Cache:**

- A portion of the RAM helping the HD
- for frequently opened/closed applcations

- Sometimes, you have free space in the RAM
- 🐇RAM is always faster than the 🐢HD

- If we have an application that we `open(RAM)` and `close(HD)` several times,
- if there is free space in the RAM,
- it makes sence to just keep it in the RAM
- even when you close it
- beacuase `1. as RAM is fast` and `2. we have free space on the RAM`
- 👉🏻 So the RAM is helping the HD
- We call that **disk cache**

🆚 **Disk cache and Virtual Memory**

- Disk cache: RAM helping HD
- Virtual Memory: HD helping RAM
