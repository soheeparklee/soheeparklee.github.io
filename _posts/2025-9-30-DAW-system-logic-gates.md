---
title: 1.9 Logic Gates and Computer Math
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

## 📌 Table

- `2 inputs` and `1 outcome`
- `2 inputs`: `A`, `B`
- `1 outcome`: `Y`

[![Screenshot-2025-10-01-at-16-52-06.png](https://i.postimg.cc/C1X3Tcv5/Screenshot-2025-10-01-at-16-52-06.png)](https://postimg.cc/LYkCj3FF)

## ✅ AND

- `outcome 1` only when **both** input is `1 & 1`
- symbol: semi circle

## ✅ OR

- `outcome 1` only when **any** input is `1`
- symbol: rounded, curved triangle

## ✅ XOR

> Exclusive OR

- `outcome 1` **only when one** input is `1`
- symbol: rounded, curved triangle with a curved line
- When there is too much electricity, the whole electricity goes off
- does not like too much `1s`
- 🛠️ Used in CRC code
- 🛠️ Used in salt

## ✅ NOT

> gate that makes the opposite

- ↔️ only `one input` and `one output`
- symbol: triangle

## ✅ NAND

> opposite of AND <br>
> NOT AND <br>

- outcome is opposite of `AND`
- draw `AND` and make opposite
- symbol: `AND` with a small circle, like `NOT`

```
00 ➡️ 1
01 ➡️ 1
10 ➡️ 1
```

- following the three first outputs,
- NAND is a gate that is active when smth is OFF
- When I **unplug** my `USB(off)`, the data is not lost, data is active
- even when unplugged, the information is active
- so even when USB is unplugged, `1`, which is `5v` is active even when it is not connected to any electricity
- 🛠️ Thanks to `NAND`, we can have **USB** and **SSDs**
- `NAND` gates produces electrocity even when it is not plugged to electricity

## ✅ NOR

> opposite of OR <br>

- draw `OR` and make opposite
- symbol: `OR` with a small circle, like `NOT`

- `NOR` gate produces electricity when it is unplugged
- when it is `0, 0` result is `1`
- but when it is plugged, cuts off the electricity
- ⚠️ `NOR` gate will save information when it is off, disconnected
- but they will lose information when conected
- when you connect/plug in, you delete/destroy data
- Thus, not valid for USBs
- 🛠️ Perfect for **hardware malware**
- create **malware with hardware**, so if somebody plugs in, you destroy all the information in his computer

## ✅ Shift Gate

> moves the bits to the right

```
if 00010000 = 16
with shift gate
result will be 00001000 = 8
```

- 🛠️ Gate used for dividing in two
- Many dividing mathematical operations are done by `Shift Gate`

## ✅ Design gates

[![Screenshot-2025-10-01-at-17-13-18.png](https://i.postimg.cc/pdTVP1Zb/Screenshot-2025-10-01-at-17-13-18.png)](https://postimg.cc/nXyfk2g0)

- normally gates come in groups
- 4 `ANDs`
- 4 `NANDs`
- 4 `NANDs` with shift function

- Logic gates are inside the **micro processor/micro chip**
- 🛠️ For doing all the mathematical operations for the computer

## 📌 How the computer adds

- we need to add in binary
  > computer **adds using `XOR` and `AND`**
  > use `XOR` for `0+0, 0+1, 1+0`
  > and use `AND` for carrying

```
0 + 0 = 0
0 + 1 = 1
1 + 0 = 1
1 + 1 = 0, and carry 1
```

- Looks exactly like `XOR`
- Thus, **add is done by `XOR` gate**
- when you buy `XOR` gate, your computer is adding

- we carry `1` when there are `two 1s`
- Thus, **`1 + 1` carrying is done by `AND`**

[![Screenshot-2025-10-01-at-17-20-47.png](https://i.postimg.cc/2SXdkgD5/Screenshot-2025-10-01-at-17-20-47.png)](https://postimg.cc/jDPnvgCV)

```
01011111 + 00110011
computer adds bit by bit
starting from the right
 - 1+1 result will be 0, and carry 1
👉🏻 10010010
```

- we might carry `1 + 1` at the very left end
- if that happens, we add the `1` at the right and add again
- so it might look like `1` looks small, but this is how computer adds

- 🛠️ When I use google maps, play games I am adding/substracting
- going closer: substracting distance, go further: add distance

## 📌 How the computer substracts

- for substraction, computer uses `NOT` and all the circuits for adding
- for substraction, computer uses `NOT` and `XOR` and `AND`
- the computer needs 2 `XOR`s, 1 `AND` and 1 `NOT`
- so substraction needs more gates
- due to this, in programming, we try to do more adding then substraction
- if possible, we try to do more adding

- 1️⃣ We keep the first number exactly the way it is
- 2️⃣ we make the second number negative, use `NOT`
- 3️⃣ then we add both

```
15 - 12
1️⃣ 15
2️⃣ 12 ➡️ -12
3️⃣ = 15 + (-12)
```

```
010111 - 101011
1️⃣ 010111
2️⃣ 010100
3️⃣ 010111 + 010100 = 101011
👉🏻 101011
```

[![Screenshot-2025-10-01-at-17-39-17.png](https://i.postimg.cc/htjm9WgZ/Screenshot-2025-10-01-at-17-39-17.png)](https://postimg.cc/GHW9Cf4v)

- 🛠️ Micro programming would be done in binary
- so adding, substraction would be done in Micro programming, in binary
- prefer adding
