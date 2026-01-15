---
title: 3.12 Conclusion_Perfect installation plan
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

## ✅ WHat is a Perfect plan?

[![Screenshot-2026-01-14-at-17-24-24.png](https://i.postimg.cc/qMBNG95r/Screenshot-2026-01-14-at-17-24-24.png)](https://postimg.cc/MX4Z6rw3)

1️⃣ It must get adapted to different user types: **Dual booting Lin-Win** <br>
<br>
2️⃣ It must allow **version hopping** or **distrohopping** <br>
have data separated from the OS <br>
👍🏻 You can change OS without losing information <br>
<br>
3️⃣ It must allow interaction between OOSS: **tunneling** <br>
common channel between both OS <br>
<br>
4️⃣ No matter the circumstances, the system must work <br>
Linux will boot windows <br>
But just incase you uninstall Linux, make windows independent <br>
💊 Create booting for windows too, do not rely on linux. Maybe oneday you want to uninstall Linux <br>

- ➡️ If we follow this plan, disks will be adaptative

## ✅ Steps on installation

#### 1️⃣ **Check your specs, limits**

- use commands
- use CPU-Z

- check the following

[![Screenshot-2026-01-14-at-17-26-12.png](https://i.postimg.cc/HsJgHzJg/Screenshot-2026-01-14-at-17-26-12.png)](https://postimg.cc/N5wVk17J)

- check motherboard architecture
- check BIOS, UEFI

[![Screenshot-2026-01-14-at-17-27-36.png](https://i.postimg.cc/sxWCPDCn/Screenshot-2026-01-14-at-17-27-36.png)](https://postimg.cc/m1TnB4DM)

#### 2️⃣ Use **GPartEd** in order to create the **partitions manually**

- do not use nextmode

[![Screenshot-2026-01-14-at-17-27-54.png](https://i.postimg.cc/j5WpKd5h/Screenshot-2026-01-14-at-17-27-54.png)](https://postimg.cc/47gLQGpK)

💡 **Conclusion**

[![Screenshot-2026-01-14-at-17-28-29.png](https://i.postimg.cc/TPsskM9D/Screenshot-2026-01-14-at-17-28-29.png)](https://postimg.cc/yJFndG21)

#### 3️⃣ **Install each OS**

[![Screenshot-2026-01-14-at-17-30-23.png](https://i.postimg.cc/bJ8nfd3Z/Screenshot-2026-01-14-at-17-30-23.png)](https://postimg.cc/FfWzjFtv)

💡 General Rule

- need to install windows first
- then linux second
- linux repsects windows, but not viceversa

- (⭐️ exam question)
- for `win+win`
- install old version first
- new second
- new over old
- 7 ➡️ 8 ➡️ 9 ➡️ 10

[![Screenshot-2026-01-14-at-17-31-21.png](https://i.postimg.cc/W1gtpTDk/Screenshot-2026-01-14-at-17-31-21.png)](https://postimg.cc/0z59cg0k)

#### 4️⃣ **Install Bootstrap Loader**

- create the menu
- if you did things in order, the linux gives you the order automatically
- name of the menu in linux: **GRUB**

[![Screenshot-2026-01-14-at-17-34-41.png](https://i.postimg.cc/mrhLz4k9/Screenshot-2026-01-14-at-17-34-41.png)](https://postimg.cc/B899kdxZ)

- (⭐️ exam question)
- in a `win+win`
- you need to add the menu manually
- you need an external program to create the menu
- use Windows Boot Manager(`winload.exe`)
- or BCEdit(`BCEdit.exe`)

#### 5️⃣ Format GRUB

- decorate your menu
- add company/customer logos...

- (1) change the **wallpaper** of the menu
- (2) choose the **OS by default**
- (3) **waiting time**: how much we will wait before booting the OS

```
❓ What happens if waiting time to 0 seconds?
- fast booting
- we will not see the menu(bootstrap loader)

🛠️ when you want to hide the expert OS
so clients cannot go into other OS
```

## ⭐️ Important!

- all the partitions that need to exist
- in all the possible situations
- in order to have a perfect disk

[![Screenshot-2026-01-14-at-17-41-53.png](https://i.postimg.cc/t4BPG98m/Screenshot-2026-01-14-at-17-41-53.png)](https://postimg.cc/0zJrp1kp)

✔️ **legacy ❤️ windows**

- all partitions are NTFS
- **two mandatory partitions:**

  - `MSR`: for booting windows if Linux is uninstalled, windows will boot independantly, NTFS, Primary, contain booting files, needs to be 300MB
  - `C:`: kernel of the system, NTFS

- **recommended partition:**
  - for data: for version-hopping, NTFS

✔️ **UEFI ❤️ windows**

- **three mandatory partitions:**

  - `MSR`: for booting windows independently, needs to be 16MB
  - `C:`: kernel, NTFS
  - `ESP`: (EFI System Partition), **must be FAT32**, only partition in the Windows universe that is NOT NTFS
  - bc if it was NTFS, windows would set a letter
  - then the user can think he can use it, save files inside
  - so the system makes it FAT32
  - so that it does not have a letter, so that users do not access
  - to avoid letters, to avoid users from touching

- **recommended partition:**
  - for data: for version-hopping, NTFS

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
