---
title: 1.2 Coding Techniques
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

- ⭐️ concept of coding and decoding
- ⭐️ combination of both: codec
- ⭐️ coding: make into binary
- ⭐️ VLC, FLC difference
- ⭐️ short questions

```
⭐️ What kind of coding techniques are there?
```

## ✅ VLC

> Variable Length Code

- code in which every symbol(`word`) has a **different length** in binary
- there are always special rules and special characters to seperate the letters and to seperate words

```
A ➡️ 01
H ➡️ 0000
U ➡️ 001
```

- 👎🏻 More difficult to figure out the portions of the message as each symbol has different legnth
- 🛠️ used in war environments
- 🛠️ morse code

## ✅ FLC

> Fixed Length Code

- code in which all symbols have the **same length**
- the number after `FLC` means the length of every symbol
- `FLC-4`: is code is `FLC`, and each symbol has length of `4`

```
red ➡️ 0011
blue ➡️ 1100
yellow ➡️ 0001
```

```
❓ If I got 010111001101(12bits) and it is FLC-4
A: it would be 0101/1100/1101
```

- 👍🏻 Easy to break the message into portions
- 👍🏻 much less accidents in `FLC`
- 🛠️ used for commercial or standard purposes
- 🛠️ `SHA-256`, `SHA-512`
- `SHA-512` is stronger as each symbol would have longer length

## ✅

## ✅

## ✅

## ✅
