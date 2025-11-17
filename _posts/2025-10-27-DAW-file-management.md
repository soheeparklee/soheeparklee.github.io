---
title: 2.6 OS Function1_File Management
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

- ⭐️ Practical questions: SoHee wants to play music automatically. What file management system should we use?
- ⭐️ Transactional Files will be test questions

## ✅ File Management

> ✔️ File: Set of bytes ➕ Metadata <br>
> ✔️ Folders(windows)/directories(linux): we group similar files <br>

- managing the files not opened in the Secondary Memory/External Memory(HDD or SSD)
- files: closed files in secondary memory

## ✅ Windows

[![image.png](https://i.postimg.cc/DzjDCfQG/image.png)](https://postimg.cc/bGn3rhBY)

- 🗂️ in windows, structure of folders is called `cascade`
- ✔️ **Drive/Unit**: the beginning of the system always has a letter assigned
- If I go up, I am going to my `father folder`
- Going down, means going to my `sub/childern folders`

## ✅ Linux

[![Screenshot-2025-10-27-at-17-54-06.png](https://i.postimg.cc/C5YjkkZN/Screenshot-2025-10-27-at-17-54-06.png)](https://postimg.cc/1nCnZgrn)

- 🌲 in linux, structure of folers is a `tree`
- the beginning of the system is called `root`, which is shown as `/`
- If I go up, going to `sub/children folders`
- Going down, means going to the root, main branches of the structure

## 📌 4 Basic formats of the secondary memory and some extras...

> Format of a secondary memory <br>
> for all USBs, HDD, SSD... <br>
> File systems are for all the secondary memory, **but RAM ❌**

- Depending on the **use** that we want to give to the secondary memory
- you have to give a special format to the secondary memory

- Sometimes, we can divide the secondary memory into partitions
- and we can give a different format to each partition

- 👉🏻 Thus, we decide the format to secondary memory depending on its use
- And we can divide the secondary memory into partitions, and allocate each format for each partition

### 1️⃣ FAT 32

> File Allocation Table

[![Screenshot-2025-10-29-at-15-25-50.png](https://i.postimg.cc/26Sncx0Y/Screenshot-2025-10-29-at-15-25-50.png)](https://postimg.cc/kVLVDWrY)

- 1️⃣ **FAT32 use `32 bits` for managing the files, files need to be less than 4GB**
- 🟰 thus, `2^32` 🟰 **4GB**
- 👎🏻 In FAT 32 the files need to be less or equal to `<= 4GB`

```
⭐️⭐️⭐️ EXAM ⭐️⭐️⭐️
❓ Sohee has a pendrive of 64GB and the pendrive is new and empty.
She is trying to store/write a video.
The video is 6GB.
But when she tries to save it, she gets an error message. Why?

👉🏻 The pendrive is formatted in FAT 32.
and in FAT 32, limit of the file is 4GB.

👉🏻 Becareful! Capacity and Format are two different things in harddrive
Even if you have a lot of capacity,
if you have a format that limits your file size, you cannot save more than the limit.
```

- 2️⃣ **FAT32 only allow file extensions with three characters**
- 👎🏻 Only allows three file extensions
- only `.doc`, `.jpg`, `ext` ⭕️
- cannot save `.docx`, `.jpeg` 4 characters extensions ❌
  - the 4 characters extensions were for more flexibility
- However, since year 2011, most of FAT32 is now also compatible four character extensions
- FAT 32 is more generous now

- 3️⃣ **FAT 32 is compatible w all external devices**
- 👍🏻 FAT 32 is 100% compatible w external devices
- 👀 compatible with all printers, scanners...

```
⭐️⭐️⭐️ EXAM ⭐️⭐️⭐️
❓ SoHee has a pendrive. However, she cannot connect it to the printer. She cannot print with this pendrive. The pendrive seems incompatible to the printer. What should she do?

👉🏻 Reformat the pendrive to FAT 32.
⚠️ However, if you want to make a reformat, you might lose your memory
So make a backup!
```

- 4️⃣ **FAT32 can play automatically**
- If you add many music `.mp3` to the FAT32 pendrive
- the pendrive will play automatically
- no need to click...

```
⭐️⭐️⭐️ EXAM ⭐️⭐️⭐️
❓ What do you choose for the format of the pendrive if you want the pendrive to play automatically?

👉🏻 FAT 32
```

- 5️⃣ **FAT 32 is compatible with both linux and Windows**

- 🛠️ very used nowadays in bootable USBs

### 2️⃣ exFAT

> Extended File Allocation Table <br>
> Extended FAT

[![Screenshot-2025-10-29-at-15-41-21.png](https://i.postimg.cc/8zPSKJL0/Screenshot-2025-10-29-at-15-41-21.png)](https://postimg.cc/mtqJhrXY)

- 1️⃣ No limit in the file size! 👍🏻
- 2️⃣ No limit in file extensions 👍🏻
- 3️⃣ Not 100% compatible w external devices 👎🏻
- 4️⃣ No automatic playing 👎🏻

- exFAT is the opposite of FAT

```
⭐️⭐️⭐️ EXAM ⭐️⭐️⭐️
❓ SoHee has a FAT32 USB. Then she wants to add a 30GB virtual machine.
What should she do?

👉🏻 Change the format, reformat to ExFAT
But remember to make a backup before reformatting!
```

- 🛠️ Normally used for big files
- has a small partition

- In general, we only use FAT32
- using exFAT means more space, means more management, more cleaning, more work...

### 💡 How do we reformat a secondary memory format?

1. Insert the secondary memory
2. Go to windows explorer
3. Find the drive(letter), origin of the cascade of your secondary memory
4. `Right click` on your secondary memory 🟰 `Open the contextual menu`
5. In button `Format`, there will be three dots `...`, so a new window will be opened, not formating right away!
   - In menu if an option has three dots `...` it will open a new menu
6. When you click on `Format` it will open a small window
7. 1️⃣ In the menu `capacity`, you will see the **size of the secondary memory**
8. 2️⃣ In the menu `file system`, this is same as **format**
   - You can click on the dropdown, and see the possible options of formats
9. Sometimes, we do not see all the possible formats, we only see some
10. It is bc of the internal technology of the secondary memory, due to the way it is manufactured, it is out of your control
11. You choose the format option that you want
12. 3️⃣ In the menu `cluster size`, means the **minimum size of the files** you can save on this pendrive
    - If `cluster size` is 4KB, your files have to be minimum 4KB
    - If your file size is smaller, like 2KB, the pendrive will save your file, **adding extra automatically** 2KB to the original file
    - this extra data is normally used for **redundance**, 👀 **ECC**, protecting information
    - The `default cluster size` is for standard use
13. 4️⃣ In the menu, `Label`, the name you want to give to the secondary memory
    - It is a good practice to change the name to your needs
14. 5️⃣ The checkbox `Fast format`, if you tick, the reformat will be done faster
    - slow is better
    - if the format is slow, you are avoiding unformatted portions
    - by doing it slow, you can make the best use of the secondary memory
    - slow format cleans, deletes transitions, makes everything smooth
    - if you do it too fast, you keep transitions, still dirty, some things not formatted, you make small holes
15. When you click on start, your memory is all deleted., there is no way back The format will be changed.

```
⭐️⭐️⭐️ EXAM ⭐️⭐️⭐️
❓ What happens if I have a 64GB, but when I try to format it, the capacity is 32GB?
👉🏻 That pendrive is partitioned, divided into two pieces
And for whatever reason, one partition is not visible
👉🏻 The partition is BLOCKED
```

```
⭐️⭐️⭐️ EXAM ⭐️⭐️⭐️
❓ What do you choose, small cluster size or big cluster size?

1️⃣ If I choose a small cluster size, the files I can save can also be small
👍🏻 I am not wasting space on secondary memory
👎🏻 less redundance
👎🏻 less safe, files are not protected
🛠️ For personal use, I want to save more files on my pendrive

2️⃣ If I choose a big cluster size, your files always have to be big
👎🏻 You will run out of capacity very soon
👍🏻 Your files are well protected, will have lots of redundance
🛠️ For servers, big cluster size, they prioritize protection

3️⃣ Default cluster size is the best option for OS
smth between small, big cluster size
🛠️ normally, recommended to use default cluster size
```

```
⭐️⭐️⭐️ EXAM ⭐️⭐️⭐️
❓ Your pendrive is in format FAT32. Your file is 4.1GB.
You need to save your format in 1 minute. You will not even be able to fast-format your pendrive. What do you do?

👉🏻 Delete a redundant/useless part of your file. Delete some information.
Reformat your pendrive ❌ You might lose all your file.
```

### 3️⃣ NTFS

> New Technology File System

[![Screenshot-2025-10-29-at-16-25-10.png](https://i.postimg.cc/Pq4JPp10/Screenshot-2025-10-29-at-16-25-10.png)](https://postimg.cc/hJXcYGy0)

- 1️⃣ **Only for windows!**
- only valid in windows

- 2️⃣ **No limit in the file size**
- you can save up to 16EB, so mmore or less you can save any file

- 3️⃣ **No automatic playing**

- 4️⃣ **Mostly compatible with external devices**

```
⭐️⭐️⭐️ EXAM ⭐️⭐️⭐️
❓ If your pendrive is not working with the printer, do you change it to NTFS or FAT32?
👉🏻 check the size of the files, and decide on the size of the files
If the file sizes are small, choose FAT32
If the file sizes are big, choose NTFS

⚠️ But becareful with NTFS, it is only compatible with Windows.
```

- 🛠️ Linux professional do not use NTFS.

```
⭐️⭐️⭐️ EXAM ⭐️⭐️⭐️
❓ You have both windows and linux in your computer. The BIOS UEFI always need a portion in the harddisk for booting. This portion would have FAT32, or NTFS?
👉🏻 FAT 32
NTFS would only boot windows
```

- 5️⃣ **NTFS has Journaling**
- Technology for backuping your files
- **Journaling**: instead of backuping all the file system, the complete file system, backup only the changes from the previous file
- 👍🏻 instead of backuping everything, backup only the changes
- do incremental backups
- 👍🏻 So in windows, NTFS, even if you lose all the files, you would be able to get yesterday's backup
- Journaling can be activated or deactivated. Not mandatory
- When journaling is activated, you have more possibilities of recovering

### 4️⃣ EXT2, EXT3, EXT4...

> Extended File System

[![Screenshot-2025-10-29-at-16-32-10.png](https://i.postimg.cc/qMyjW485/Screenshot-2025-10-29-at-16-32-10.png)](https://postimg.cc/jLqH7V3H)

- 2 < 3 < 4 is more modern

- 1️⃣ For linux OS
- 2️⃣ No limits of file size
- 3️⃣ No limits of extensions
- 4️⃣ Not compatible with external devices by default
- but you can change
- 5️⃣ No automatic playing

- 6️⃣ **EXT has Transparent Encryption**
- 👍🏻 **Transparent Encryption**: The files are encrypted with a key, and the key is hidden in the booting system of the secondary memory
- If you want to find the key, you destroy the booting system, and the key will also be useless, the files will also not be able to open
- So the files are very well protected
- you can activate or deactivate Transparent Encryption
- 👎🏻 But if you activate Transparent Encryption, everything is hashed, system will be slower
- ⚖️ Transparent Encryption makes systems more secure, but more slow
- 🛠️ Used for banks, hospital, servers...need to be more safe

- 7️⃣ **EXT has a i-Nodes table**
- 👍🏻 **i-Nodes table**: table with all the metadata of the files
- 👎🏻 in windows, the metadata is all together with the files, next to the data
- In linux, metadata is seperate from the file, in another place of the secondary memory
- 👍🏻 so linux is safer
- In linux in order to access the file, you need to access the `i-Nodes table`
- 👍🏻 double access, more secure
- If a hacker tries to hack a linux, he has to hack the file and also the i-Nodes table, so more difficult to hack
- metadata is like a address of the house, and data is like the key
- even if you have the key(data), if you do not know the address(metadata), you cannot rob the house
- card number is metadata, and the physical card is data
- even if you stole physical card, if you do not have card number, you cannot use the card, more safer

```
⭐️⭐️⭐️ EXAM ⭐️⭐️⭐️
❓ Why is linux safer than windows?
👉🏻 Linux has transparent encryption and i-Nodes table
```

### 💡 More formats for file systems

- 1️⃣ **HFS: Hierarchical File System**

  - for MacOS
  - file system in Mac have different levels
  - any file that is not a Mac file is labeled as low level
  - anything that is external than Mac, it is low level
  - Mac does not open low level files
  - unless you increase the level by opening the files with `iTunes`, `iTerms`...
  - need an external application
  - then the level of the file is updated, and you can open
  - So if you want to open files, increase the file level

- 2️⃣ **APFS: Apple File System**

  - like HFS, but for iOS
  - you cannot open a file from android

```
⭐️⭐️⭐️ EXAM ⭐️⭐️⭐️
❓ Why you cannot open a file from android?
👉🏻 For iphone, android is low level, so you need an external program to open it
```

- 3️⃣ **F2FS: Flash Friendly**

  - when letter and number is together, use the letter as number times
  - so `F2 = FF`
  - Flash: modifiable
  - system for android
  - Flash Friendly: compatible with many things
  - you can open almost everything, with little modification
  - so in android, you can open almost everything without installing external applications
  - Android is top 1 OS thanks to its file system

## ✅ Transactional Files

> different format of files <br>

#### ✔️ Definition of Transaction in file:

- huge file that normally we send from a sender to a reciever, or we store in a secondary memory
- transactions cannot fail
- can succeed totally, or fail totally
- you send all the file, or do not send the file at all

- it is necessary for important file exchanges
- bank files, hospital files, databases

#### ✔️ Transaction Mechanism in files

- How to make a file transactional

- 1️⃣ **Write-Ahead**:

  - before changing anything on the file,
  - first, write all the changes you want to make on the text file(different file)
  - to change the file, send the `original file` and the `text file` with the changes you want to make
  - when you send the file, you need to send both files `original file` ➕ `text file w changes`
  - if there is an error,
  - keep the original file
  - and send the text file again
  - ↔️ guarantee changes

- 2️⃣ **Copy-On**:

  - 🟰 standard backup
  - make a backup of the `original file`
  - then make changes on the `original file`
  - if there is an error
  - make file to `original file` again
  - you guarantee you have the `original file`
  - ↔️ guarantee the original file, does not guarantee changes

- 3️⃣ **Shapshots**:

  - take a picture of the system as you make the changes
  - take picture, make small change, take another picture, make another small change...
  - making a backup after small changes every certain times
  - if there is an error
  - you go to the previous picture, not the original
  - 👀 All the dual booting systems(linux + windows in the same computer) are done using snapshots
  - After installing windows, take snapshots, then after installing linux, take another snapshot

#### ✔️ Extensions of transacional files

- How do you call the transactional files
- Depends on what mechanism you use for transactoinal files

- `Reiser`: if you use mechanism Write-Ahead
- `ZFS`: if you use mechanism Copy-On
- Snapshots: do not have specific format
- `NTFS(TxF)`: transactional files specific for windows OS
- `XFS`: transactional files specific for Linux OS
  - `x` is the same as `x` in `EXT2`

#### ✔️ Evaluation of Transactional files

- 👍🏻 We are increasing security of the file
- 👎🏻 waste capacity of memory as we need to save the original data two times
- 👎🏻 we are using double amount of memory
- 👎🏻 **we increase security ⬆️, but we decrease/damage performance ⬇️**
- we are using more memory

- Transactional files should be stored in harddisk
- bc transactional files are huge, so save it in harddisk
- transactional files are also important, so we want to save in longlasting memory

- For using transactional file, you need a special text editor, specific applications
