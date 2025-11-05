---
title: 2.7 Memory Management
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

## ✅ Memory Management

> Memory Management is for managing the RAM <br>
> does not apply for SM, HD

- how to save processes in the RAM
- when we open the files

[![Screenshot-2025-10-29-at-17-36-39.png](https://i.postimg.cc/MHGBYk7S/Screenshot-2025-10-29-at-17-36-39.png)](https://postimg.cc/jwGCsF3g)

- RAM and Secondary Memory are very far away
- To communicate between RAM and Secondary memory, we need an intermediate block to help
- They are
- 1️⃣ segmentation unit
- 2️⃣ paging unit
- these units are inside the Microprocessor

- As there are two units, there are two techniques to maange the RAM
- 1️⃣ segmentation
- 2️⃣ paging
- each of the units proposes a way of placing processes in the RAM
- from the two techniques that places more processes⬆️ in the RAM using small amount⬇️ of RAM

[![image.png](https://i.postimg.cc/T12sqP7z/image.png)](https://postimg.cc/2bJTCCfG)

## 1️⃣ Segmentation

- No possibility of breaking the memory
- One process goes completely goes inside the RAM, or cannot go on the RAM at all
- If a process cannot go on a RAM, and it is left outside the RAM, you will not be able to run the process

- last space left in the RAM that is free is called `FREE SPACE`

```
❓ Why does my program not running?
- No space on the RAM, cannot go on the RAM
```

[![Screenshot-2025-11-05-at-15-58-16.png](https://i.postimg.cc/mrZH1p2J/Screenshot-2025-11-05-at-15-58-16.png)](https://postimg.cc/Mn4ThDBm)

```
❓ Swap out
My RAM looks like this
P1 300MB
P2 200MB
P3 400MB
P4 500MB

If I want to run P5, which is 300MB, which process should I swap out?
- P1 or P3 or P4
```

#### ✔️ Free Space

- The free empty portions in the middle of the RAM are known as `FREE SPACE`
- However, when free spaces are seperate they remain seperate

```
❓ Imagine future processes P6, 7, 8,,,,,are all greater than 200MB, and you cannot swap out.
Can they swap in?

- NO
```

#### ✔️ External Fragmentation

[![Screenshot-2025-11-05-at-15-58-36.png](https://i.postimg.cc/jScWT6QW/Screenshot-2025-11-05-at-15-58-36.png)](https://postimg.cc/VJSsBCh1)

- So the wasted areas that are not occupied anymore are called **External fragmentation**
- empty portions in the middle of the RAM
- they are normally colored in 🔴 RED, to show that they are wasted
- `External fragmentation` = `100MB`

#### ✔️ Order of putting program on the RAM

- If you use segemtation,
- open the `big programs`
- then the `small programs`
- If you open the small programs first, later with `external fragmentation`, you will not be able to open in big problems.

```
❓  Why in some companies, big programs like database, HR applications and the invoicing applications
are opened automatically in the begining of the session?

- Bc that system use segmentation
```

## 2️⃣ Paging

1. RAM is divided into portions, which is called `FRAMES(Marcos)`
2. your processes will also be divided into portions called `Pages`
3. the `size of the frames` need to be greater than the size of `pages`
   `size of the frames` >= `pages`
4. One page per frame
5. The process **SWAPS IN** if **ALL** its pages can go in
6. Pages do not need to be in order when it goes into the frames

[![Screenshot-2025-11-05-at-16-15-22.png](https://i.postimg.cc/FHGHJ961/Screenshot-2025-11-05-at-16-15-22.png)](https://postimg.cc/BjL0rG4G)

1. Divide Process1 into 3 pages of 100MB each
2. Divide Process2 into 2 pages of 100MB each
3. Divide Process3 into 4 pages of 100MB each
4. Divide Process4 into 5 pages of 100MB each

[![Screenshot-2025-11-05-at-16-17-51.png](https://i.postimg.cc/0Q0W9Bjx/Screenshot-2025-11-05-at-16-17-51.png)](https://postimg.cc/TLhq9QnH)

- If the whole process cannot go ALL on the RAM, then it cannot go on the RAM at all
- `Process4 of 5 pages` cannot go on the RAM at all, even if there is one frame left

- The frames that are not used at the end are called `FREE SPACE`

#### ✔️ Internal Fragmentation

[![Screenshot-2025-11-05-at-16-26-40.png](https://i.postimg.cc/tCKMtPKY/Screenshot-2025-11-05-at-16-26-40.png)](https://postimg.cc/nC12nscJ)

- Problem of Paging
- If frames are bigger than pages
- the frames are fragmented to 100MB and 50MB
- we are wasting space in each of the frames
- they are called **Internal Fragmentation**
- they are called internal as frames inside are fragmented, they have wasted portions

```
⭐️⭐️⭐️ EXAM ⭐️⭐️⭐️
❓ How much data is internal fragmentation in P1?
👉🏻 150MB

❓ How much total internal fragmentation of the RAM?
👉🏻 450MB
- Internal fragmentation does not take free space at the end into account
- Free space at the end is not Internal Fragmentation
```

- Can you get rid of internal fragmentation?
- Yes, make the `size of the page` to the `size of the frame`
- `size of the page` = `size of the frame`

- However, the `size of the frame` is a factory setting that comes with a RAM
- so when you buy a RAM, pay attention to `size of the frame`
- and adopt/modify OS `size of the page` to the `size of the frame`

```
⭐️⭐️⭐️ EXAM ⭐️⭐️⭐️
❓ How can you minimize  external fragmentation?
👉🏻 Open processes in a good order,
first big then small processes
```

- In general, `external fragmentation` and `internal fragmentation` is difficult to get rid of it
- Thats why sometimes RAM seems to be smaller, less capacity then I think

[![Screenshot-2025-11-05-at-16-36-49.png](https://i.postimg.cc/C5H9RKKB/Screenshot-2025-11-05-at-16-36-49.png)](https://postimg.cc/T51tSfgf)

```
⭐️⭐️⭐️ EXAM ⭐️⭐️⭐️
❓ Swap P1 out, and decide if P4 can fit in.
P4: Process4 into 5 pages of 100MB each

👉🏻 No, still only 4 frames
so P4 cannot go in
P4 stays out of the RAM
```

[![Screenshot-2025-11-05-at-16-37-40.png](https://i.postimg.cc/50WP8MTH/Screenshot-2025-11-05-at-16-37-40.png)](https://postimg.cc/PLKzk0th)

```
⭐️⭐️⭐️ EXAM ⭐️⭐️⭐️
❓ Then what happens to P5,
P5: Process5 of 4 pages
👉🏻 YES, as there are 4 frames
and in Paging, order does not matter
but you can go on the RAM if there is sapce
```

- When process go in the RAM
- **ALL or NONE**
- but **ORDER does not matter**

#### ✔️ Program Counter in Paging

[![Screenshot-2025-11-05-at-16-43-19.png](https://i.postimg.cc/nhCnMNyQ/Screenshot-2025-11-05-at-16-43-19.png)](https://postimg.cc/ZWtGMsKT)

- In paging, the processes are not in order ❌
- so the computer should somehow know from P5 and jump over P2 and jump to P5
- so you need to know the order of the processes
- So paging needs `Program Counter` of the Neuman Machine
- so `PC` tells you which instruction comes next

- Goal: give user a smooth experience
- I want my video to run smoothly, not suddenly pop up word file

#### ✔️ Pages Table

- I need a schema that has the order of the processes
- This **Pages Table** is located in the `forbidden area of the RAM`, the **OS in RAM**

- `Pages Table` is a file with `.csv` file
- `.csv` file: Comma Seperated Values
- everything in this file is seperated with `commas` `,`

- `Pages Table` contains the following
- `PID`, `Frames of the process`, `Base Register`, `Limit Register`, `...rest of the processes...`, `Base Register of the free areas`, `Limit Register of the free areas`

1. PID:
2. Frames of the process
3. Base Register: beginning
4. Limit Register: size of the process, how many frames does this process have

- `Base Register` and `Limit Register` is redundant(repeated)
- as you can know start and size with `Frames of the process`
- 👍🏻 But we repeat for security!

#### 📄 Design a Pages Table

- ✔️ Design a pages table for this RAM

[![Screenshot-2025-11-05-at-17-20-57.png](https://i.postimg.cc/mDypy2vj/Screenshot-2025-11-05-at-17-20-57.png)](https://postimg.cc/PpNMthrv)

```
📄 Pages Table 📄
process name
, frames where is process has portions
, base register
, limit register
,

P5 , 1, 2, 3, 10 , BRP5 , 1 , LRP5, 4
, P2, 4, 5, BRP2, 4, LRP2, 2
, P3, 6, 7, 8, 9, BRP6, LRP3, 4
FBR(Free Base Register, there is none free)
, FLR(Free limit Register, there is no free limit register)
```

- ✔️ Design a pages table for this RAM

[![Screenshot-2025-11-05-at-17-34-17.png](https://i.postimg.cc/x80mL0QX/Screenshot-2025-11-05-at-17-34-17.png)](https://postimg.cc/r0Pzk2KT)

```
📄 Pages Table 📄
P1, 1, 2, 3, BRP1, 1, LRP1, 3
, P11, 6, 7, 8, BRP11, 6, LRP11, 3
, P3, 11, 12, 13, 14, BRP3, 11, LRP3, 4
, P4, 15, BRP4, 15, LRP4, 1
, P12, 17, 18, BRP12, 17, LRP12, 2
, P7, 23, BRP7, 23, LRP7, 1
, P8, 24, 25, BRP8, 24, LRP8, 2
, P13, 26, BRP13, 26, LRP13, 1
, P10, 27, 28, BRP10, 27, LRP10, 2
```

## 📌 Segmented Paging

- Paging is more complicated for the CPU
- If things work with segmentation, they use **segmentation**
- Computer tries segmentation
- However, if the process cannot SWAP IN
- if things do not work with segmentation,
- then the computer uses **paging**

- you **page** the free space of the RAM
- then use paging

## ✅

## ✅

## ✅

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
