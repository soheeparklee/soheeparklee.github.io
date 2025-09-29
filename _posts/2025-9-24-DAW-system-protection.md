---
title: 1.4 Protection of bits 1.5 Hashing
categories: [FP DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

## ☑️ ECC and CRC

- 🛠️ protection for transport/download
- network
- protection for files

## ✅ ECC

> Error Checking and Correction <br>
> added by groups <br>

- add extra bits(`Redundance`) in order to correct possible failures
- send extra information to check if the information is correct
- need to transmit both `data + extra bits`
- several ECC techniques exists, each technique has its own subset creating method

#### ✔️ How to apply ECC

- 1️⃣ Initial sequence
- 2️⃣ Create subsets of bits of the initial sequence
  - each ECC technique has its own subset creating method
- 3️⃣ On each subset, apply an `even parity`
- 4️⃣ All extra `1s` are added at the end of the sequence
- 5️⃣ Using the extra `1s` we can use **reverse engineering** to find the original initial sequence
- 👉🏻 We can check if the initial sequence has been changed using the `extra 1 bits`

## 📌 Even parity

- 👉🏻 **even parity**: number of `1s` has to be even

- if number of `1` is even, add `0`
- if number of `1` is odd, add an extra `1`

#### ✔️ Example of subsets

[![Screenshot-2025-09-24-at-15-30-59.png](https://i.postimg.cc/vBwcJJN7/Screenshot-2025-09-24-at-15-30-59.png)](https://postimg.cc/2qTkvKm3)

- **subset 1**: `0100`
- ➡️ odd number of `1s`
- ➡️ according to `even parity`, need to add extra `1` to make it even
- **subset 2**: `1101`
- ➡️ odd number of `1s`
- ➡️ according to `even parity`, need to add extra `1` to make it even
- **subset 3**: `0100`
- ➡️ odd number of `1s`
- ➡️ according to `even parity`, need to add extra `1` to make it even
- In total, we have to add extra `1, 1, 1` in the end

#### ✔️ Example of getting extra bits

```
001101011010
( 12, 11, 10, 9, 8, 7, 6, 5, 4, 3, 2, 1, count from right to left, but write from left to write)
subset1 = 1, 2, 3, 4      = 1010 ➡️ do not add ➡️ 0
subset2 = 4, 5, 6, 7      = 1011 ➡️ add extra ➡️ 1
subset3 = 4, 6, 7, 8      = 0101 ➡️ do not add ➡️ 0
subset4 = 9, 10, 11, 12   = 0011 ➡️ do not add ➡️ 0

extra bits: 0100
result: 001101011010 + 0100
```

[![IMG-7537.jpg](https://i.postimg.cc/9FVJWKwP/IMG-7537.jpg)](https://postimg.cc/Jt6bxTqt)

#### ❓ What do we need to create a computer with ECC?

- 1️⃣ need a **counter** to count the `extra bits`
- 2️⃣ **comparison chip** to compare if the `count of 1s` are even or not
- 3️⃣ **flag** to give you an `extra bit` if the count of 1 is odd
- normally called ECC flag

## 📌 Logic Gates

- pre-built chips that perform mathametical operations

#### ✔️ 3 main logic gates

[![Screenshot-2025-09-24-at-16-02-35.png](https://i.postimg.cc/R03LvJL7/Screenshot-2025-09-24-at-16-02-35.png)](https://postimg.cc/p9HFZT7r)

- 1️⃣ chip `AND` gate
- two for input, one output
- output `1`, only if input is both `1` and `1`

- 2️⃣ chip `OR` gate
- two for input, one output
- output `1`, whenever there is any `1`

- 3️⃣ chip `XOR` or `Exclusive OR`
- very picky!
- symbol: OR triangle with a border to the left
- two for input, one output
- output `1`, when there is only one `1`
- output `1`, when there is one `1`, but when there is 2 `1`s, it outputs `0`
- 두꺼비집, when electicity is too high, everything goes down
- so when there is too many `1`, outputs `0`. very picky!

## ✅ CRC

> Cyclic Redundance Code <br>

- send `extra bits` protected with another `extra bit`
- however, need to send more data
- more cyles(more redundance) ⬆️ more secure ⬆️ efficiency ⬇️
- uses `XOR`

#### ✔️ How does CRC work

[![Screenshot-2025-09-24-at-16-03-51.png](https://i.postimg.cc/tCqB6Tz6/Screenshot-2025-09-24-at-16-03-51.png)](https://postimg.cc/mhn3fTJZ)

- CRC = Initial sequence + `Polynomial`
- each CRC uses has own `Polynomial sequence` method

- 1️⃣ Convert `Polynomial` into a sequence of bits
- exponents of the `x` indicate which bits are `1`
- if exponent of `Polynomial` is `8, 2, 1, 0` then bit position `8, 2, 1, 0` will be `1`
- other bits will be `0`
- ⭐️ In CRC, has different changes the numbering of the bit
- most right bit is `0`
- result: `100000111`
- Thus the size of the sequence will depend on the exponent of the `Polynomial`
- 2️⃣ Write the `Polynomial sequence` below the original sequence
- starting by the left
- ⭐️ but, discard all the `0s` on the left
- 3️⃣ `XOR` bit by bit
- 4️⃣ the rest of the original sequence, just retype again, copy
- 5️⃣ Now repeat the step 2️⃣~4️⃣, cyclic
- ⭐️ remember, first `0s` will be discarded
- 6️⃣ repeat until the final result is shorter or same length as the original polynomial, stops
- 7️⃣ Final result `checksum` get we get will be added at the end of the original message
- Then, will be transmitted
- 8️⃣ Reciever will perform the reverse engineering, then will check if the message has any errors

#### ✔️ Checksum

- final result of the CRC process
- used to check if the message has arrived correctly

## ✅ Hashing

- 🛠️ used for protecting passwords
- needs to be more secure than file protection
- example of hashing: `yescrypt`

- there is always a mathematical function in Hashing ➡️ `Hash function`
- apply the `hash function` to the password that you type
- Hashing applies `hash function` to **each** of the the original bits
- if my password is `ZORRO`, as each `CHAR is 8 bits`, will be 40 bits
- apply `hash function` to each of the 40 bits

- method for `Hashing`

#### ✔️ Goal of hashing

- goal is to get something very different from the original password
- even if two passwords are very simmilar, the result will be totally different

- If the system has hashing, you can use simmilar passwords, as they will be converted into totally different results(GMAIL)
- However, if the system does not have hashing, you can not use simmilar passwords(HOTMAIL)

```
Q: If the teacher can use `hola` and when it expires uses `hola1`, what kind of technology is the systems using?
A: Hashing
```

## ✅ Salt

> use hashing, use math <br>
> store in hard drive <br>

- add salt to a password
- salt: random `0s and 1s`, transforming the password before hashing the password
- add salt: get random sequence of `0s and 1s` to the original password
- then `XOR` the salt and the original password
- then hash the result of `original password + salt XOR`

#### ✔️ Where do we use salt? Where is it stored?

- `salt` needs to be recorded/stored in order to log in the system
- ⭐️ thus, `salt` should be stored in the **hard-disk of the computer**, so it is kept involatile
- which means you can use only that computer for logging in
- we use salt for computers that should be protected themselves

## ✅ Pepper

> use hashing, use math <br>
> store in cloud <br>

- store `salt(pepper)` in a **cloud/server**
- 1️⃣ Now `salt(pepper)` can be accessed from all, several computers
- We can log-in from any computer
- not me, but a compnay server would be protecting my `salt(pepper)`
- 2️⃣ As `salt(pepper)` is protected by a company, `pepper` is considered more protected than `salt`

#### ✔️ Clouds

- clouds are comuters protected physically and logically with protocols

## ✅ Security

### ☑️ Logic Security

- Security using software
- example:
- ✔️ **Hashing**: `salt`, `pepper`
- ✔️ **Anitivirus**
- ✔️ **Firewall**: machine with specific software that opens or closes ports

  - if I close HTTP, you cannot browse internet
  - if I close SMTP, you cannot send emails

- ✔️ **DMZ**: Demilitarized Zone, in a company a set of computers that are free of public access with no much protection, normally contain non-essential information

  - having DMZ protects MZ from being extra abused
  - for example, `DMZ: public webpage for FP`, `MZ: my private aula virtual, need to log-in`

- ✔️ **Mirroring**: having my computer mirror/copy another computer

  - mirroring is NOT a backup
  - 👎🏻 backups are not totally updated
  - 👍🏻 mirroring is duplicated in real-time
  - with mirroring, you can sync both computers only when an important and correct
  - can sync just incase you have to go back to the past

- ✔️ **Backups**: every x months make a backup of your data

  - backups should be taken into isolated environments

- ✔️ **Security Patch**: software that solves an error found _without_ needing to reinstall the operating system

### ☑️ Physic Security

- Security using hardware

- ✔️ **Clouding**: Taking my company data to the cloud

  - Three types of clouding
  - 1️⃣ **IaaS**: Infrastructure as a Service
    - I do not have computers in my company, I use the computer of another company
    - use the computer of another company, I do not have the infrastructure
    - not very commonly used
  - 2️⃣ **Paas**: Platform as a Service
    - contract another company's computers and their software
    - you log-in to their applications
    - a lot of loss of control of your company
    - the platform will not be tailored to your needs
  - 3️⃣ **SaaS**: Software as a Service
    - Everything belongs to the other company
    - including the products that are created by you
    - very expensive
    - streaming platform, you do not have any rights to keep the movie, paying for the service
    - When a traditional company contracts a company to take the company into the Internet

- ✔️ **Security and High Availability(5 9's)**

  - `3 9's`: The company is available for `99.9%`
  - `4 9's`: The company is available for `99.99%`
    - Linux OS, AMAZON has a `4 9's` certificate
  - `5 9's`: The company is available for `99.999%`
    - out of 100,000 only 1 will fail
  - systems company always aim for the `5 9's`

- ✔️ **Load Balancing**

  - workload is evenly distributed among the computers
  - apply RAID

- ✔️ **UPS**

  - Uninterrupted Power System
  - system for solving electicity failures
  - generators

- ✔️ **DPC**

  - Data Process Centers
  - building specialized in databases
  - need very strict architectural security

- ✔️ **Access Controls**
  - finger prints

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅
