---
title: 3.9 Partition System
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

## ✅ Partitions schemes = drawing = design = outline

- There are two types of partition systems
- MBR partition system

# 1️⃣ MBR partition system

> Master Boot Record

- MDR can mean two designs

  - (1) max of 4 primary
  - (2) 3 primary and umbrella of several logical partitions

- design of partitions (1) with a maximum of 4 Primary partitions
- we say that a disk is MDR if there is a max of 4 primary partitions
- you can have 1 primary, 2, 3, 4, but not 5
- ⚠️ MDR system can only boot up to 4 OS if you use design type (1)

- It is also MDR when (2) you have 3 primary and one umbrealla(extended, with many logical partitions inside)
- 3p + X(xL)
- when you want to create more than 4 partitions
- 👎🏻 but in logical partitions, the OS is only for testing, cannot install OS for booting
- ⚠️ MDR system can only boot up to 3 OS if you use design type (2)

```
❓ A company wants to create 7 partitions.
Can you create 7 partitions with a MDR schema?

- create 3p + umbrella, extended with 4 logical partitions
```

```
❓ A company wants
- windows 7 bootable
- windows 8 bootable
- windows 9 bootable
- windows 10 bootable
- windows 11 bootable.
Can we use MDR?

- No. MDR will only let up to 4 bootable OS.
```

## ☑️ **The unallocated space in MDR**

- Unallocated space: space/partition for future, always recommended to have some U
- In MDR, we cannot add Unallocated space in MDR design (1)
- So, if you want unallocated space, you cannot use design (1), never not after the fourth primary partition
- 1️⃣ `4P + U` will not work ❌

- So, if you want unallocated space, you should choose design (2)
- 2️⃣ `3P + U` ⭕️

- If you are using the umbrealla, specifically in design (2)
- 3️⃣ `3P + E(xL) + U` will also not work ❌
- the unallocated partition cannot be outside the umbrella ❌
- 💊 So, place it inside the umbrella
- 4️⃣ `3P + E(xL + U)` ⭕️

```
❓ SoHee has a computer of HD of 2TB.
There are 300GB free at the end, but she cannot reach them. It is unreachable.
Why is this problem happening?

- Maybe, possibility 1: she has a MDR with 4 primary partitions
- possibility 2: she has a MDR with 3 primary partitions, then an umbrella, then the unallocated space.

💊 Solution: place the unallocated space inside the umbrella
```

## ☑️ **How to place the unallocated space inside the umbrella**

1. Extend/Expand the umbrella
2. Move the unallocated space inside the extended umbrella
   ⚠️ If you do not expand the umbrella, the other logical partitions will be more 꽉 껴서, will suffer
   💊 G Part Ed can help you expand the umbrella
   💊 Mini tool partition wizard can also help umbrella extend, and move the partitions

## ☑️ **MDR Table**

- If you want to activate the unallocated partition at the end,
- does not make sense to activate all the partition in the middle ❌
- you should be able to jump to the unallocated partition ⭕️
- 💊 Use an index: help to jump to the partition you want
- **MDR table**: index in the MDR design

- **MDR table**: for the HD for finding for the partition
- This MDR table(index) is stored in Unit 0
- **Bootstrap loader**: The menu for the user selecting the OS is also in Unit 0
- the menu is for choosing the OS that the user wants to boot

## ☑️ **Final recap MDR Design**

```
Bootstraploader (Unit0)
➕
MDR table (Unit0)
➕
4P | 3P+U | 3P+E(xL) | 3P + E(xL + U)
```

```
❓ If I destroy the Unit 0 what happens?

- You will not lose the data, will not lose partition
- You will lose the index and the menu
- You will not be able to boot the disk

- But as you do not have the index, you cannot jump within partitions
- to recover the information
- you need to go track by track, sector by sector
- looking for transitions, and trying to recover information

- That is why it takes so long to recover a HD
```

```
❓ What is inside the Unit 0 in MDR?
- bootstrap loader
- MDR table
```

## 2️⃣

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
