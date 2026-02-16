---
title: 4.16 Extra-RAID
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

## 1️⃣ IDE should never be empty

✔️ **IDE with nothing does not boot**

- If `IDE` really has nothing, it will not boot
- virtual machines does not understand a IDE without an `iso`
- phisically, its like a wire that is left hanging, without connected to anything
- computers do not like this situation ☹️
- IDE without nothing inside ❌
- IDE without an iso existing ❌

💊 **So add an empty `iso`**

[![Screenshot-2026-02-13-at-16-18-25.png](https://i.postimg.cc/bYtjHfK0/Screenshot-2026-02-13-at-16-18-25.png)](https://postimg.cc/grm5mQcr)

- Even if we do not need the `iso`, at least create an `empty iso`
- atleast need `iso vacio`
- so add `iso` and leave it empty
- the `iso` does not do anything, but just make an `empty iso`
- IDE with` empty, useless iso` ⭕️

[![Screenshot-2026-02-13-at-16-18-55.png](https://i.postimg.cc/ZqM1pwjR/Screenshot-2026-02-13-at-16-18-55.png)](https://postimg.cc/Mc1P8bC2)

## ⭐️ GPartEd iso

- it is needed for
- 1️⃣ creating partitions
- 2️⃣ viewing the partitions
- After creating the partitions, we deleted the `iso` file
- by doing `Send shutdown signal`
- ⚠️ But then, if you do not have the `GPartEd.iso` in your IDE
- you will not be able to see the partitions!
- if you do not have the `iso` in IDE, you will not be able to see the partitions you created
- 👉🏻 `GPartEd.iso` is also used for viewing the partitions

## 2️⃣ It is ITIL when IDE zone exists

- What happens if I need an iso
- But the IDE zone does not exist
- And I add the `iso` to the SATA zone
- 👉🏻 This will make VM work,
- 👉🏻 But it is not ITIL
- 👉🏻 As technicians, this is not ideal

❓ **How to create the IDE zone(review)**

- add the area that is missing, create IDE
- elimiate the `iso` file in the SATA
- then add the `iso` to the IDE

## 3️⃣ RAID

- What if I want to create a RAID?
- RAID: Redundant Area of Independent Disks
- you need to add extra `vdi`s to create RAID
- then need to combine the different `vdi`

#### 💡 Two possibilities of creating a disk

- 1️⃣ `Disk` + `Mirror of the disk` (information is identical on both disks)
- 2️⃣ `Disk` + `Second disk` (information is split)

✔️ **How to create a RAID**

[![Screenshot-2026-02-13-at-16-19-19.png](https://i.postimg.cc/WbvxGFmp/Screenshot-2026-02-13-at-16-19-19.png)](https://postimg.cc/F1TPmKnw)

- `vdi` should be inside `SATA` zone
- click on harddisk(right top square)
- choose create
- decide size of new `vdi`
- decide dynamic

⚠️ **Never change the name of the vdi**

- when you add extra `vdi`s
- never change the name!
- virtual box will automatically add a number

✔️ **Each `vdi` has their own schema**

- when we have several `vdi`s
- we can choose the specific `vdi`s
- and partition the `vdi` differently
- Each of the `vdi`s of the RAID can have a different partition schema
- 👀 I can make first `vdi` as GPT and second `vdi` as MBR
- ⚠️ Unless you want a mirror, if you want a mirror, they should be the same schema

👍🏻 **Advantages of RAID**

- distributing information on several disks
- protecting the important information

✔️ **Delete `vdi`**

- if you do not need it,
- press and click on `eliminar conexión`
