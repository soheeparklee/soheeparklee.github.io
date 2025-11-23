---
title: 2.10 Optimization management
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

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
- ☝🏻 one L1I per core

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

w❓ hich element of the CPU cache helps the following?
- IPC to the kernel
- ISA
- IRQ
- DRQ
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

## 3️⃣ Lets help the HardDisk

#### 💊 Harddisk Buffer

- buffer: temporal storage for making profit of a data transaction

💡 **proximity principle**

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

## 4️⃣ Lets help the

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

------
❓
👉🏻
❓
👉🏻
❓
👉🏻
```
