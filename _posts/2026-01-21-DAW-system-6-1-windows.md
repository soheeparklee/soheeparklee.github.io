---
title: 6.1-3 Windows
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

## 💡 Digital Barrier

- if you do not have some tech, you are not part of the technology
- 👀 `windows 3` was the first digital barrier

## 💡 Service Pack

- remember both:
- **updates**
- **security patches**
- from `windows XP`

## 💡 UPnP

- universal Plug and Play
- automatically installs any new hardware
- ready to use without needing extra drivers
- the drivers are automatically updated

- from `windows XP`

```
What arised from windows XP?
- service pack
- UPnP
```

## 💡 MiniOS

- light version of a OS
- light means: official created by MS, but not detailed, bad, worse
- eliminiate non-necessary feature
- created without depth

👀 **Example of MiniOS**

- Windows XP PRO (32 Bits).
- Windows 7 PRO (32 & 64 Bits).
- Windows 8.1 PRO (32 & 64 Bits).
- Windows 10 LTSB (32 & 64 Bits). Long-Term Servicing Brand
- Windows 10 LTSC (32 & 64 Bits). Long-Term Servicing Channel
- Windows 10 PRO (32 & 64 Bits).
- ⭐️⭐️⭐️ Windows 11 LTSC 64bits

## ✅ In Windows 10...

### 💡 Multiplatform

- adaptive to different devices
- the GUI is **resizeable**
- `Windows 10`

### 💡 Bitlocker

- Transparent Encryption for windows

### 💡 Microsoft Edge

- web browser
- 👎🏻 too many advertisement, marketing
- 👎🏻 came too late, already chrome and firefox had the market
- Microsoft had nothing unique, so lost to chrome and firefox

```
📖 Rule of development 📖
1. limit too much adversitement
2. need to be unique
```

### 💡 Windows Defender

- security center
- 👎🏻 compatibility problem with other anti-virus system
- windows try to trap the user into their system

```
📖 Rule of development 📖
1. limit too much adversitement
2. need to be unique
3. should be compatible with other systems
```

### 💡 Hyper-V

- VM in MS
- similar to Virtual Box
- 👎🏻 Hyper-V works only for window hosts
- not successful

```
📖 Rule of development 📖
1. limit too much adversitement
2. need to be unique
3. should be compatible with other systems
4. Application should be dual, not only for Windows, not only for Linux...
5. Should be multiplatform, resizeable
```

## ✅ Windows 10 editions

### ☑️ HOME Edition

- for **domestic** environment
- no Bitlocker ❌
- no Hyper-V ❌
- no technical things

### ☑️ PRO

- for **small** companies
- contains Bitlocker ⭕️
- contains Hyper-V ⭕️

### ☑️ Enterprise

- for **big** companies

✔️ **LTSC**

- use LTSC version
- Long Term Service Channel
- no updates for a long time
- 🟰 normal employees do not have to update each computer
- 🟰 they will update all computers at the same time

### ☑️ Educational

- for educational communities

### ☑️ N

- no multimedia, no audio, no video
- No Windows Media Player
- 🛠️ for servers
- 🛠️ for computers with no customer in front

### ☑️ IoT

- Internet of Things
- has OS for IoT
- but you will not see the OS of an IoT
- 🛠️ cache ATM

## ✅ Windows Lite

- not official OS by MS
- no tech support
- they wanted to make smth like chromebook
- do not install, bad security

- as MS was embarrased that Windows Lite failed,
- they changed name to `Windows 10X`

## 📢 Chrome

- Chrome started as a broswer, but entered the OS market
- Chrome browser was created by Linux

```
📖 Rule of development 📖
1. limit too much adversitement
2. need to be unique
3. should be compatible with other systems
4. Application should be dual, not only for Windows, not only for Linux...
5. Should be multiplatform, resizeable
6. Stay in your field, chrome should stay in browser, not in OS market
```

## ✅ Problem of Windows 11

- 👎🏻 **Windows 11 had lots of security problems**
- very bad first impression

- 👎🏻 **Windows 11 was very different from the previous version**
- ppl found it too new, too difficult to adjust
- ppl like things they are used to, that are similar

- 👎🏻 **Very bad performance for videogames**

- 👎🏻 **Windows Copilot**
- Windows own, propietary AI
- only related to MS, limits its use
- you can disinstall, but will leave hidden traces
- and the traces can make other applications fail

- 👎🏻 **TPM 2.0**
- Trusted Platform Module
- for extra security
- TPM will contain `encryption key` + `digital certificates`
- TMN also controls the VPN

```
VPN: create a virtual private network, get a new IP, hide yourself, also giving access to application that you would not have access to
```

- TPM also does SSL

```
SSL: protocols to give security to the transactions that do not have security
https = http + SSL
```

- TPM in general, controls the security of the computer
- in a separate chip
- and when you split things, better

- TPM is only connected to the CPU
- There is no connection between `HD, RAM` and the TPM
- So if elements wants security, it needs to go through the CPU
- then the CPU will give/deny access
- as CPU is an intermediate
- we have an extra layer of security
- 👉🏻 3 layer of security

- 👍🏻 So, TPM is good for `encryption key` + `digital certificates` + `VPN` + `SSL` + security

- 👎🏻 Most computers before Windows 11 do not have the chip in the motherboard
- TPM comes on the motherboard
- you cannot install TPM easily
- but old computers, if they were expensive, maybe they have the TPM chip

- 👎🏻 ESU
- 👎🏻 Existence of control pannel depends on HW

```
📖 Rule of development 📖
1. limit too much adversitement
2. need to be unique
3. should be compatible with other systems
4. Application should be dual, not only for Windows, not only for Linux...
5. Should be multiplatform, resizeable
6. Stay in your field, chrome should stay in browser, not in OS market
7. Security is the most important!
8. If you are the same product, do not be too different from the previous version
9. Take into consideration your customers
```

## ✅ How to check if you have TPM chip

> Windows + R > tpm.msc

- you need admin permission to see
- if the message is a red cross: TPM not available, you cannot install `Windows11`
- if the message is TPM activated: you can install `Windows11`
- you can deactivate it, accessing the BIOS or just in `tpm.msc`
- but only can activate if you have a `UEFI`

- ❓ Why deactivate TPM?
- when we have CPU performance problems

- ❓ If a computer does not have TPM, you have to go on with `windows 10 with tech support?`
- some years ago, MS obliged users to pass onto windows 11

## ✅ ESU

❓How do you switch to a windows 11 if you do not have a TPM?

- buy another computer or
- some motherboards have a small slot for adding the TPM
- but not all motherboards have the slot for TPM
- so, MS created the ESU

✔️ **ESU1**

- Executed Security Update 1
- extend tech support for 1 year for 30 dollars
- so you can have `Windows 10 + 30 dollars per year per computer`
- so you can have tech support until Nov 2026
- then next year, pay `Windows 10 + 60 dollars per year per computer`
- so you can have tech support until Nov 2026
- 👉🏻 If you find expansion problems, make that API for extension should be cheap/free
- 👉🏻 or create a group fee, for a whole company

```
📖 Rule of development 📖
1. limit too much adversitement
2. need to be unique
3. should be compatible with other systems
4. Application should be dual, not only for Windows, not only for Linux...
5. Should be multiplatform, resizeable
6. Stay in your field, chrome should stay in browser, not in OS market
7. Security is the most important!
8. If you are the same product, do not be too different from the previous version
9. Take into consideration your customers
10. If you find expansion problems, make that API for extension should be cheap/free
```

## ✅ Control Pannel in Windows 11

- Control Pannel in Windows 11 **depends on the HW** of the computer
- so if your computer have low resources(low RAM, low CPU...)
- it will not have control pannel
- it will only have setting window
- 👎🏻 less freedom to change several settings

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
