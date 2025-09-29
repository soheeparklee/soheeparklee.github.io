---
title: 1.7 Main memory(RAM) Addressing
categories: [FP DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

## ✅ RAM

> storage of **open** files and applications = processes

- process: open and running file and application
- RAM is divided into address

- addresses are numbered in **hexadecimal**
- the address at the user area the most top, is `0`
- the address the the most bottom is `F`

```
Q_1: If the last address of the RAM is FFFFFFFFh, how many bits are there in this address?
A: each F has 4 bits internally, has 4 * 8 = 32 bits
- thus, this RAM is using 32 bits for the address
- thus, this RAM is using 32 bits for addressing(direcionar) the RAM
```

### ☑️ Capacity of RAM

- ⭐️ by looking at the last address, we can know the capacity of the RAM
- ⭐️ each F has `4 bits` internally

- Following the `computing principle`, if the RAM has `FFFFFFFFh` 32 bits, RAM can have `2^32` combinations of address
- If in each address, I store `1 byte = 8 bits` of information
- I can save up to `2^32 * 1 byte` in my RAM
- more or less `4 * 1000 * 1000 * 1000 bytes`
- `1000 = Kilo`
- `1000 * 1000 = Mega`
- `1000 * 1000 * 1000 = Giga`
- so, `4 * Giga bytes`
- in conclusion, if the last address of the RAM is `FFFFFFFFh`, this RAM has a total of `4 Giga Bytes`

## 📌 hexadecimal

> numbering system that groups bits by 4, starting by the right <br> > `1111` = 15 = F

- 1️⃣ divide bits by grouping them into 4, starting by the right
  - if the group is not complete, complete left with 0
- 2️⃣ then applies the weight rule to each group of 4
- 3️⃣ then changes the weight of 10 into the letter A
- 11 ➡️ B
- 12 ➡️ C
- 13 ➡️ D
- 14 ➡️ E
- 15 ➡️ F
- 4️⃣ add a `h`

```
address = 010101111111

1️⃣ divide into groups of 4, from the right
- 1111
- 0111
- 0101

2️⃣ apply weight
- 8421 /  8421 /  8421

- 1111 = 1 + 2 + 4 + 8 = 15
- 0111 = 1 + 2 + 4 = 7
- 0101 = 1 + 4 = 5

3️⃣ change weight into letter
- 15 = F
- 7
- 5

💡 result is 57F

4️⃣ always add h to say this address is hexadecimal
💡 result is 57Fh
```

```
address = 1110110

1️⃣ divide into groups of 4, from the right
if group is not complete, add 0 to the left
- 0111
- 0110

2️⃣ apply weight
- 0111 = 7
- 0110 = 6

3️⃣ change weight into letter
nothing to change
- 7
- 6

💡 result is 76

4️⃣ always add h to say this address is hexadecimal
💡 result is 76h
```

```
1110
weight = 14
💡 result is Eh
```

## ✅

## ✅

## ✅

## ✅

## ✅
