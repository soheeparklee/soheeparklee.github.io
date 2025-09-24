---
title: 1.4 Protection of bits
categories: [FP DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

## ✅ ECC

> Error Checking and Correction <br>
> added by groups <br>

- add extra bits(`Redundance`) in order to correct possible failures
- send extra information to check if the information is correct
- need to transmit both `data + extra bits`
- several ECC techniques exists, each technique has its own subset creating method

- 1️⃣ Initial sequence
- 2️⃣ Create subsets of bits of the initial sequence
- each ECC technique has its own subset creating method
- 3️⃣ On each subset, apply an even parity
- `even parity`: number of `1s` has to be even
- if number of `1` is even, add `0`
- if number of `1` is odd, add an extra `1`
- 4️⃣ All extra `1s` are added at the end of the sequence
- 5️⃣ Using the extra `1s` we can use **reverse engineering** to find the original initial sequence
- We can check if the initial sequence has been changed using the `extra 1 bits`

[![Screenshot-2025-09-24-at-15-30-59.png](https://i.postimg.cc/vBwcJJN7/Screenshot-2025-09-24-at-15-30-59.png)](https://postimg.cc/2qTkvKm3)

- subset 1: `0100`
- ➡️ odd number of `1s`
- ➡️ according to `even parity`, need to add extra `1` to make it even
- subset 2: `1101`
- ➡️ odd number of `1s`
- ➡️ according to `even parity`, need to add extra `1` to make it even
- subset 3: `0100`
- ➡️ odd number of `1s`
- ➡️ according to `even parity`, need to add extra `1` to make it even
- In total, we have to add extra `1, 1, 1` in the end

## ✅ CRC

> Cyclic Redundance Code <br>

- send `extra bits` protected with another `extra bit`
- however, need to send more data
- more cyles(more redundance) ⬆️ more secure ⬆️ efficiency ⬇️

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅
