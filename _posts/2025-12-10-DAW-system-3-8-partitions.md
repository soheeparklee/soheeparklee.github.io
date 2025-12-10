---
title: 3.8 Partitions
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

## ✅ Partitions and Harddisk

[![Screenshot-2025-12-10-at-17-20-15.png](https://i.postimg.cc/d11f5cRv/Screenshot-2025-12-10-at-17-20-15.png)](https://postimg.cc/Y458SVyy)

- in secondary memory = hard disk

- the plates can use the two sides at the same time
- so one header per one side
- in total, two headers

- plates rotate using spindle motor
- header does not move

[![image.png](https://i.postimg.cc/DyZqmyvf/image.png)](https://postimg.cc/8s2F0Gfx)

✔️ **Track circle**

- concentric circles called **Track circle**
- outmost circle is `0`
- as you go inside, the number of the circle increses `1, 2, 3...`

✔️ **Sectors**

- the circles are divided into **sectors**
- the triangles goes from 12 o' clock : sector 0
- it turns like the clock direction

✔️ **Unit 0**

- intersection of sector 0 and circle 0
- unit 0 stores the booting system
- if we damage unit 0, the disk is useless, as we cannot run the booting system
- also the key of transparent encryption in linux is stored in Unit 0

- But modern disks have a copy of unit 0 in the **interior** unit of the **last** disk
- 👍🏻 so more difficult to break, and more safer

✔️ **Rest of the units**

- rest of the units are called just units, they are not numbered

✔️ **Two technology of disks**

- **Magnetic technology disk**
- old
- the headers are magnetic
- and the tracks had magnetic material
- if you use magnetic tech, in each of the unit, you can store 512Bytes, if the units are old

- **Optical technology disk**
- new
- headers are lazer
- tracks are valleys`(lazer is kept, 0)` and hills`(lazer is reflected, 1)`
- 2048Bytes if new (🆚 4times more than magnetic disk)
- optical disks keep much more data than magnetic disk

- the size of bytes you can store per unit does not change on the size of the disk
- as disk is a circle shape, external units are bigger, but the amount of bytes we can save is the same
- the ones interior the disk the bits are more compressed, but save the same bytes
- 👉🏻 if you want to hide the information, save it in interior, compressed
- 👉🏻 for more safetey, use the internal tracks
- 👉🏻 so modern disks have a copy of unit 0 in the **interior** unit of the **last** disk

✔️ **Cylinder**

- if we take the same track in every plate, you have a cylinder
- number of cylinder is the same as number of tracks

- if you get an error in track 20, linux will say `you have an error in cylinder 20`
- it means the same thing!

## ✅ **Cluster**

- if you take several consecutive units, you have a cluster
- it means _minimum size of a file_
- even if the file is smaller than the size of the cluter, you need to fill it
- 👀 My picture is `3kb` but the cluster size is `4kb`. This picture file will still occupy `4kb` in the harddisk.
- and the extra `1kb` added to fill the cluster size is called **redundance**

✔️ **Redundance**

- used for **parity**
- used for protection of the file
- 👀 If the picture is `13kb` and cluster size is `4kb`, the picture file will occupy `16kb`.
- File size will be cluster size, or be the multiple of cluster size
- the redundance will be `3kb`
- more redundance ⬆️ more secure the file ⬆️

✔️ When you predesign a harddisk, what should I choose? small cluster or big?

- small cluster size:
- files can be small, will not occupy a lot
- 👍🏻 you can store many files
- 👎🏻 but the files will be not very protected
- 👉🏻 for normal standard ppl who wants many files in one disk

- big cluster size:
- file sizes will be big
- 👎🏻 will not be able to save so many files
- 👍🏻 files will be very protected, lots of redundance
- 👉🏻 for servers, for companies who need protection

- ❓ I do not know for what I will use this harddisk
- use standard, default for harddisk

✔️ **How to change cluster size**

- need to format the disk
- make sure to backup the disk
- right click(contextual)
- format the disk
- choose `unidades asignacion = cluster size`
- you can also choose harddisk format(NTFS, exFAT...)here

✔️ **DEFRAG tool**

- Due to clusters and redundancies, your HD will have several many holes
- what would happen all the extras are moved to the end of the disk
- and create a huge big extra at the end of the disk
- you can clean it and use it for extra files
- that can free up more space

- **DEFRAG** tool: to collect all the holes and make a big space
- it improves the capacity of the disk
- you can use DEFRAG tool when your harddisk seems out of space

✔️ **Patition**

- If we go on with the cluster
- we change sides, and to another plate, we create a partition

- partitions have a name
- disk: devices, called `/dev/sd/`
- connected by SATA
  - dev: device
  - sd: SATA
  - letter: order of the disk(first/second/third...)
    - A: internal
    - B, C, D: external
  - then a number indicating partition of the disk
- so, `/dev/sd/A/1`, `/dev/sd/B/1`

## ✅

## ✅

## ✅

## ✅❌

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
