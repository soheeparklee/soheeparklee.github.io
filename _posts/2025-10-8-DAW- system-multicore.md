---
title: 1.11 Microprocessor- Multicore and Multithreading
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

- ⭐️ concept of multicore, multi thread
- ⭐️ FSB, BSB
- ⭐️ memory controller
- ⭐️ transport bus
- ⭐️ GPU

## ✅ Multicore

[![image.png](https://i.postimg.cc/YCgKPFJJ/image.png)](https://postimg.cc/189jn8RH)

- CPU is **multicore** if the `neumann machine` is **replicated** several times
- However, even if replicated, not all blocks are replicated

#### ✔️ In CU

> clock, sequencer is NOT replicated

- `clock`: NOT replicated❌ we need only one boss
- `sequencer`: NOT replicated❌ only one clock, only one sequencer to set only one rythm
- `Program counter`: Replicated⭕️ each core has one `PC`, every core can run own instuctions, every `PC` pointing to their own address and has each has own instructions, this is **multi-tasking**
- `Instruction Register`: Replicated⭕️ as each core has each `PC`
- `Decoder`: Replicated⭕️ to help `IR`

#### ✔️ In ALU

> ALL replicated

- `InRA` and `InRA`: Replicated⭕️
- `Operational Circuit`: Replicated⭕️
- `ACCUM`: Replicated⭕️
- `State Register`: Replicated⭕️

  - 👉🏻 Thus, all `ALU blocks` are replicated
  - bc all the instructions use different numbers

#### ✔️ In MU

> RAM is unique <br>
> Memory Controller

- The `RAM` is unique, outside the micro-processor
- thus the `RAM` is NOT replicated❌
- However, as 4 instructions are running at the same time, `MAR`, `MDR` and `MS` will be more stressed!
- 4 instructions will come at the same time
- 😫 So `RAM` is unique, but the internal blocks(`MAR`, `MDR`, `MS`) will be more stressed
- 💊 **Memory Controller**: So we have a super block
- So instead of having `MAR`, `MDR`, `MS`, we have `ONE BIG BLOCK` for controlling everything
- This huge block works simillar to replicating the `RAM blocks`(`MAR`, `MDR`, `MS`), and reduces the stree of the `RAM`
- sometimes, next to the `Memory Controller`, there is a `System Agent block`
- **System Agent block**: to help coordinate several `RAMs`
- When you have several `RAMs`, the `System Agent block` helps coordinating the `divided RAM`

- In the picture, there are `4 cores`, so there are `4 neumann machines`
- So if we have `4 cores`, we will have
  - one clock, one sequencer
  - 4 `PCs`, `IRs` and `Decoder`, all blocks of `ALU blocks`
- if we have `4 cores` we can run 4 instructions at the same time simultaneously
- And we have one RAM, but we have `Memory Controller`

#### ✔️ In Peripherals

> Transport Bus

- 😫 In multicore, the peripherals are also collapsed, very stressed running several instructions at the same time
- 💊 **Transport Bus**(also called Input/Output memory controller (I/O))
- used for controlling the peripherals at a very high speed
- ⭐️ In the exam, this block will be called `Transport Bus`⭕️, and **NOT** `Input/Output memory controller`❌

## ☑️ Graphics Processing Card

- If we are multicore, there can be a portion named `GPU`
- however, not mandatory
- **helps** the other standard graphics card with the graphics(images, videos)
- 🛠️ For games, music, movies

## ✅ Back Side Bus `BSB`

> road inside core

- Each core inside has an internal sturcture for communication
- like internal streets/roads
- ⭐️ one `BSB` per core
- one core will have their own `BSB`
- 🐢 `BSB` is relatively slower to `FSB`

```
❓ If in core 3, the data from InRA is 3,
but cannot reach the OC,
what is the problem?

A: The BSB in core 3 is broken, having problems.
```

## ✅ Front Side Bus `FSB`

> road to communicate among cores

- Apart from `BSB`, there is a circular highway to communicate **AMONG** cores
- circular road to connect all the cores
- ⭐️ there is only ONE `FSB` in one computer

```
❓ In 4 core computer, how many BSB and FSB?

A: There will be 4 BSBs and 1 FSB
```

- Sometimes, we have to send information from one core to another
- 🛠️ Then we need to use `FSB`

```
❓ If the result of operation 1 in core 1 cannot reach InRB of core 4, what is the problem?

A: The FSB is not working properly.
```

#### ✔️ Speed of FSB

- 🐇 `FSB` is the fast speed bus
- If my clock has 2GHz, my `FSB` tends to be `2GHz` too
- so the `FSB` has more or less same speed as the clock

- If the clock is much faster than the `FSB`, it means there is a bottleneck in the `FSB`
- example: If my `clock is 2.5GB`, and my `FSB is 1GHz`

[![image.png](https://i.postimg.cc/2j0DLhRq/image.png)](https://postimg.cc/9zwSv4fV)

## ✅ How many cores?

- In computing, every number should be a `power of 2`
- `1 core`: mono-core

- However, sometimes core is not a `power of 2`, for example: `6 core computer`
- then, it means `4 core` and `2 cores` are for mirroring
- 🛠️ for **protection, backups**

```
❓ In a 8 core computer, what is the result of this?
FSB + BSB + MC + TB
= 1 + 8 + 1 + 1
= 11
```

## ✅ Multi-thread

> Dividing one process into several execution threads

- each of the threads(parts of process) will be processed by different blocks
- If you want your job to be done without interruption/disconnection
- use an **independent** execution thread

#### ✔️ Resource sharing in multi-thread

- being multi-threading means more or less multi-tasking
- you can only do multi-threading if you have a **resource sharing** technique

- `Mono thread`: takes the whole micro processor to itself
- yellow runs, then blue
- `Multi thread`: the threads have to share the micro processor
- The microprocessor would do blue and yellow at the same time

- If I am multi-core, it is easy to be multi-thread
- If you have many cores, it does **NOT** necessarily mean your computer is faster ❌
  - It means your computer can run more things at the same time
  - It means your computer micro processor is more stressed, more hotter, need to ventilate more, need to refresh your computer more

[![image.png](https://i.postimg.cc/Vsr4Q0Bw/image.png)](https://postimg.cc/G9Rvv25g)

#### ✔️ Optimization

- If you are mono-core you can be multi-thread ⭕️
- But you have to share your resources very well
- 💊 **Optimization** tools: help share resources among threads in mono-core

## ✅ Logic Core

- `Physical core`: number of cores we have, `8 core = 8 physical core`
- `Threads per core`: how many thread in a core
- `Logic cores`: how many threads I have in total

```
❓ If we have 4 cores, and each core executes 2 threads, how many threads in total can we execute?
A: 8 threads in total

Physical core: 4
Threads per core: 2
Logic cores: 8

I have a computer of physical core of 4, thread per core is 2
then I have 8 logic cores
⚠️ I have 4 physical cores, but have 8 logic cores, bc I feel like I have 8 workers!
```

## ✅

## ✅
