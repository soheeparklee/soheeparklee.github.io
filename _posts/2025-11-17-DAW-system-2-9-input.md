---
title: 2.9 Input/Output and general interruptions management
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

> 💡 Peripherals interrupt when they have problems <br>
> and more situations that interrupt...

## 👀 Example of interruptions

- mouse that runs out of battery
- mouse/keyboard that lost connection with bluetooth
- keyboard that one key is broken
- printer is out of paper
- Ventilator is broken, temperature is rising
- try to divide by 0
- blue screen bc of an internal problem

- 🛑 If an interruption occurs,
- stop everything
- and pay attention, solve the interruption immediately

- ⚠️ Algorithms are interrupted when there is an interruption

- 💊 There are three techniques to solve the interruptions

## ✅ PIO

> Processed Input Output

- There is an interruption in the middle of executing a process
- If you are in the middle of a process
- and there is an interrption
- 1️⃣ need to stop the process
- 2️⃣ solve the interruption
- 3️⃣ and go back to the same spot of the process

✔️ **Service routine**

- 💊 each interruption has a different solution to solve
- 💊 each interruption needs a different mini program to be solved

- **Service routine**: mini program to solve the interruption
- there is one service routine for possible interruption
- `no paper in printer` -> `show error message "no paper" `
- `computer temperature so hot!` -> `turn the fan on`

✔️ **Area of Service Routines**

- Service routines are on the RAM
- Service routine should be loaded on the `RAM`
- several Service routines are saved at the **end of the RAM**
- called **Area of Service Routines**
- this means that from the RAM, we are using a small portion for the service routines

- 👎🏻 We are reducing the RAM very much, for storing the service routines
- so if you buy a `16GB RAM`, actually you can only use `14GB`
- as you use some for `OSRAM` and `service routines`

✔️ **You need to prepare the RAM for the service routines**

- As the service routines are in the RAM, when we turn the computer off, we delete them from the RAM
- when we switch the computer on, we have to upload the service routines again to the RAM
- when we switch the computer on, and the RAM is not properly connected, the service routines cannot be loaded, causing an error. The computer will not boot. It will make long beeps.

- 🚨 Service routines are important, as computer should be ready for interruptions from `second 0`

✔️ **Jump to the service you need**

- All the service routines are together, one after the other
- however, it makes no sence to run all of them one by one
- Jump to the service routine you need, and exectute **only** the routine you need

✔️ **Vectors table**

- In order to jump to that service routine,
- you need a ** vector table** that acts as an index
- indicating the **beginning** the service routine for each of the interruptions
- tells you where to go if one interruption occurs
- you can go there, and run the service routine
- 👀 `mouse interruptions` -> `FA23h`
- 👀 `keyboard interruptions` -> `FB123h`
- 👀 `temperature interruptions` -> `FF213h`
- This table is loaded in the `OSRAM`, along with the `process table` and `pages table`

✔️ **Tecnique 8**

- Due to the location of the vectors table
- when there is an interruption
- go to the `OSRAM`
- check the `vectors table`
- find the location of the `service routine`
- go down to the location of the `service routine`
- then go back to where you were running

[![Screenshot-2025-11-17-at-17-48-21.png](https://i.postimg.cc/KYWQD4Fd/Screenshot-2025-11-17-at-17-48-21.png)](https://postimg.cc/McyyW6nD)

- This is called the tecnique of the number 8
- bc the shape that yellow arrows make looks like a 8

✔️ **Program Counter**

- program counter is the element that sends you up and down the RAM
- PC is inside the CPU, the micro processor
- that is why this technique is called process input/output
- this technique overloads/uses/warm up the processor
- Processor is involved in this technique

✔️ **Result of PIO**

- warms up the CPU
- collapses the RAM

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
