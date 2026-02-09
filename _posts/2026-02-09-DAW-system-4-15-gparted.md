---
title: 4.15 GPartEd
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

- ➡️ is what I should choose in each step

## ✅ Menu of GPartEd

[![1menu-Of-Gparted.png](https://i.postimg.cc/k5F7zJM7/1menu-Of-Gparted.png)](https://postimg.cc/jW2VJrJ1)

- just let it go, no need to choose, it will automatically choose the first option
- ➡️ first option is LIVE
- ⭐️ Live: use smth without installing
- GPartEd Live: use GPartEd without installing

- ❓ Why do we use GPartEd Live?
- to create partitions for the first time,
- without installing it

## ✅ Keymap

[![2keymapfinal.png](https://i.postimg.cc/3J4Y7Crj/2keymapfinal.png)](https://postimg.cc/tYjLN6x7)

- keymap: keyboard distribution
- 👀 keyboard with ñ is a spanish keyboard
- ➡️ `Don't touch keymap`
- means application is using the standard keyboard that it finds

## 💡 How to screenshot in VM

- the screenshot shortcut do not work in VM
- use `recortes tool`

## ✅ Language

[![3language.png](https://i.postimg.cc/q7LdQ1Qv/3language.png)](https://postimg.cc/v1cjZLpJ)

- language of the application
- ➡️ `33`, means US English

## ✅ Mode

[![4mode.png](https://i.postimg.cc/kGV3JqCr/4mode.png)](https://postimg.cc/PvkFKGNK)

- mode of the application

✔️ **There are two modes**

- 1️⃣ command mode
- 2️⃣ graphic mode

- 💡 Rule: for administration, use `command mode`
- administration: creating user

- 💡 Rule: for design, use `graphic mode`
- as we are designing partitions, use `graphic mode`
- most linux applications have `graphic mode` by default

## 💡 Three enter access mode

- 👉🏻 Until here we pressed the enter key three times
- many linux profesisonal applications have a **three enter access mode**

## ✅ GPartEd screen

- after the three enters, the standard `GPartEd` screen will show up

- check the top right corner

[![5GPart-Ed-size.png](https://i.postimg.cc/mrTvcQ4v/5GPart-Ed-size.png)](https://postimg.cc/Jsd6vHGx)

- 1️⃣ check that the size of the disk is correct!
- it should be `100GB`
- 2️⃣ check the direction of your disk
- make sure you are partitioning the `vdi`
- your `vdi` would be in direction `/dev/sda`
- this is your internal disk
- ⚠️ if it is `/dev/sdb` or `/dev/sdc`: then you are partitioning external disk

[![6GPart-Ed-free-disk.png](https://i.postimg.cc/t70f96Dr/6GPart-Ed-free-disk.png)](https://postimg.cc/BPgNgXrD)

- 3️⃣ check the exclamation mark ⚠️
- exclamation mark: means you have to create the index
- in partitions, you create the index first, then the partitions

## ✅ Three embedded windows

[![7embedded-Windows.png](https://i.postimg.cc/xjWTXF4w/7embedded-Windows.png)](https://postimg.cc/Lh3M7vRD)

- When we run any appliaction in a VM,
- we will see three windows

- 👉🏻 **embedded windows**

- internally: language of the application 👉🏻 English
- VM window: language of Virtual Box 👉🏻 Spanish
- Real machine window: language of the host OS

## ✅ Create the index

#### ✔️ How to create the index

[![8menu-Of-Gparted.png](https://i.postimg.cc/W4b2RRdj/8menu-Of-Gparted.png)](https://postimg.cc/21MpvKdX)

[![9create-Index.png](https://i.postimg.cc/bwwMpqRq/9create-Index.png)](https://postimg.cc/KRCQ5SVW)

- menu `device` of GPartEd
- `device` > `Create Partition Table`

#### ✔️ Name of partitions

- MBR 🟰 `msdos`
- `msdos` is the first OS that worked with MBR
- GPT
- ➡️ `msdos`

[![10create-MBR.png](https://i.postimg.cc/0QDXcj9D/10create-MBR.png)](https://postimg.cc/0M5CN8My)

[![11create-MSDOS-final.png](https://i.postimg.cc/8P1XmT9C/11create-MSDOS-final.png)](https://postimg.cc/DmMc232V)

- after choosing your disk partition, the exclamation mark will be gone ⚠️

[![12No-More-Exclamation-Mark.png](https://i.postimg.cc/cCdhhc9S/12No-More-Exclamation-Mark.png)](https://postimg.cc/njwqcqfR)

## ✅ Create partition

[![13p1.png](https://i.postimg.cc/nzJGVktY/13p1.png)](https://postimg.cc/yJLZv0xk)

- when you want to create a partition
- always unallocated should be selected
- if not, the new partition you are creating will be created over the existing partition

- after selecting on unallocated,
- click on plus

#### ✔️ Free space preceding(MiB):

- how much space you want before the partition
- ➡️ `0`
- `0` means no wasted space before the partition
- ➡️ if `0` is not possible, `1`

❓ **Why is it a good idea to put 0 for free space preceding?**

- because we do not want to waste space between the partitions
- you create holes
- and zombie cookies will try to go to that holes
- 👉🏻 to avoid holes, to avoid zombie cookies
- the holes do not belong to any partition, the antivirus cannot check those holes

- ⭐️ cookie: text files for saving preferences
- ⭐️ zombie cookie: changes location, and hides inside the holes, escaping antivirus, easily infect

❓ **Why is it impossible to add a O?**

- sometimes it is not possible, because of two reasons
- 1️⃣ to create Unit 0: need to save the index in unit 0, need some megabytes
- 2️⃣ to change format between partitions: from windows(`NTFS`) to linux(`ext2,3,4`)

#### ✔️ New size(MiB):

- size of the partitions in **MegaBytes**
- from GB to MB, `multiply by 1024`

#### ✔️ Free space following

- do not modify, automatically filled in
- space at the end of the disk

#### ✔️ Align to

- leave as default

#### ✔️ Create as

- type of partition
- primary, logical...

#### ✔️ Partition name

- technical name of the partition
- it is chosen by default, not editable
- `/dev/sda1,2,3...`
- for the system, filled in automatically

#### ✔️ File system

- format of the partition
- 👀 NTFS, ext4...

#### ✔️ Label

- non technical name that the technician to give to the disk
- 👀 kernel, boot, data, tunnel...

## ✅ Primary partitions

#### 1️⃣ Win10/32bits/MSR

- for booting windows

[![13p1.png](https://i.postimg.cc/nzJGVktY/13p1.png)](https://postimg.cc/yJLZv0xk)

#### 2️⃣ Win10/32bits/kernel

- for windows kernel

[![14p2.png](https://i.postimg.cc/nzSrSF2R/14p2.png)](https://postimg.cc/hzxKfqHT)

#### 3️⃣ Linux18.04/32bits/kernel

- for lubuntu kernel

[![15p3.png](https://i.postimg.cc/PrwJKkDG/15p3.png)](https://postimg.cc/mtTT2JVV)

## ✅ Extended

[![16extended.png](https://i.postimg.cc/T3xbDP4Z/16extended.png)](https://postimg.cc/crD6qdZm)

- Extended partitions should be created before the logical partitions

❓ **What should be the size of the external partition?**

- `100GB - 300MB - 30GB - 15GB`
- just select `Create as` as `exteded`, then the remaingin size will be automatically calculated

- ⚠️ space following the extended disk should be 0
- end of the disk should be 0
- so `Free spae following` should be 0, this is not reachable at the end, outside `3P+E`
- `Free Space` should be 0
- 🤦🏻‍♀️ why create unreachable space?

```
❓ When we create the extended partition,
we accidently leave 200MB after/following the extended.
And we have legacy BIOS

- question A: Are they reachable with the legacy?
- No. Legacy can only reach 4 partitions

- question B: Are they reachable with the UEFI and the MBR disk?
- NO. They are more than 4

- question C: How can I reach the 200MB?
- 1️⃣ we change the MBR into GPT
- 2️⃣ need to extract the disk, connect it to the computer with the UEFI
- then we have UEFI and GPT
- now, we can finally reach the 200MB
- and reassign/put it inside the umbrella
- now, bring the disk back to the original computer
```

```
❓ What should be the file system of the external partition?
- extended
```

- Now, unallocated is inside the extended!

[![17unallocated-Inside-Extended.png](https://i.postimg.cc/nLR9gGc0/17unallocated-Inside-Extended.png)](https://postimg.cc/McBGjRBQ)

## ✅ Logicals

- Note: when you select inside the VM, do it slowly

#### ✔️ Lubuntu18.04/32bits/boot

- for lubuntu to boot

[![18L1.png](https://i.postimg.cc/SQzY180B/18L1.png)](https://postimg.cc/NLB05KjD)

#### ✔️ Windows10/32bits/data

- version hopping

[![19L2-Win1032bits-Data.png](https://i.postimg.cc/50QyGcrF/19L2-Win1032bits-Data.png)](https://postimg.cc/62wB2Pt9)

#### ✔️ Lubuntu18.04/32bits/home

- for linux data

[![20L3-Lub180432bits-Home.png](https://i.postimg.cc/2876g70P/20L3-Lub180432bits-Home.png)](https://postimg.cc/sv1sh7dc)

#### ✔️ Lubuntu18.04/32bits/SWAP

- ❗️ attention: `file-system` is `linux-swap`

[![21L4SWAP.png](https://i.postimg.cc/T1Xd4Kmk/21L4SWAP.png)](https://postimg.cc/k6fPVXT8)

#### ✔️ Tunneling

[![22Tunneling.png](https://i.postimg.cc/zDnXRkZc/22Tunneling.png)](https://postimg.cc/xq1SwMdv)

#### ➡️ Final predesign

[![23predesign.png](https://i.postimg.cc/y8WHnmtV/23predesign.png)](https://postimg.cc/HrGRkyTK)

## ✅ Save the partitions

- click on the green tick
- unless clicking on the green tick, nothing is saved
- you can modify before clicking on the green tick

- if you make a mistake,
- you can only change sizes, posistion of the partition, format of the partition
- if you want to change other things, delete and create again

- if you made too many mistakes,
- better to delete and create again

## ✅ Bugs or spurious errors might appear

- error due to the real situation of the host at that moment
- not the technician, your fault
- at the moment of creating the partitions
- the host had other things to do
- so the host intercepted the VM

- 💊 go to the first partition that has a bug
- bugs appear with the exclamation mark ⚠️
- and delete from there onwards
- and start again

- If there was no errors
- the message `All operations successfully completed` must appear

[![24success.png](https://i.postimg.cc/nrTyGr1X/24success.png)](https://postimg.cc/SY21yy34)

## ✅ Enter details

- Then, enter ▶️ details
- mandatory to enter one of the NTFS partitions
- (ideally the kernel)

#### ✔️ There should be four steps

- 1️⃣ **Book the space** `create empty partition`
- 2️⃣ **Clear the old system** `clear old file system signatures in /dev/sda2`
- 3️⃣ **Prepare for the new system** `set partition type on /dev/sda2`

- if you missed one of the four steps, you can run it with a command

- 4️⃣ **Create the file system** `create new ntfs file system`
- mandatory to enter step 4
- `mkntfs -Q -v -F -L 'Win1032bitsKernel' '/dev/sda2/'`
- `mk`: make
- `ntfs`: format is ntfs
- `Win1032bitsKernel`: label
- `/dev/sda2`: technical name of the partition

#### ✔️ enter the `mk` command

[![25cluster-Size.png](https://i.postimg.cc/SxnBcyYD/25cluster-Size.png)](https://postimg.cc/9DjghHp7)

- you will see
- ➡️ **cluster size**
- if I have a cluster size of `4096 Bytes` = `4KB`
- all the files should be a multiple of `4KB`
- this is the cluster size of the windows partition
- and this would be the cluster size of all the disk, even in linux
- cluster size is always balanced

- 💡 in linux name of cluster size is `block size`

```
❓ What is the block size of this disk?
- 4KB
```

## ✅ When 0 operations pending

[![26-0operations-Pending.png](https://i.postimg.cc/tCMfqLvH/26-0operations-Pending.png)](https://postimg.cc/hfVMM3qC)

- it means the partitions are saved in the `vdi`
- now, `iso` is not needed anymore

## ✅ close the VM

- close from inside, to outside
- order should be `Gparted > VM > RM`
- 1️⃣ close black square
- 2️⃣ click on VM `X`: send shutdown signal, to delete the iso
- 3️⃣ close the tray and press enter
- 4️⃣ go to VirtualBox > settings > storage
- and check there is no `iso`

[![27no-ISO.png](https://i.postimg.cc/QMpnqV8k/27no-ISO.png)](https://postimg.cc/R3ZRSSnN)

## ✅ Create a snapshot

- things that you just finished are called `fresh`
- name the snapshot `fresh partitioning`

[![28snapshot.png](https://i.postimg.cc/26GcPJBS/28snapshot.png)](https://postimg.cc/R63LtgRk)
