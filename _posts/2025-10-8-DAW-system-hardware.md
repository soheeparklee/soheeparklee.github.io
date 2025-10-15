---
title: 1.12 Hardware specifications
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

## ✅ A. Motherboard, Printed Circuit Board

> main board of the computer <br>
> also called Printed Circuit Board `PCB`

- normally mother boards contain
  - `microprocessor`: north
  - `RAM`: at the east
  - `Expansion slots`: some slots for extending the capabilities according to your needs(`TV card`, `ecography card` for hospitals, `vibration measurement card` for measuring earthquakes...)

#### ✔️ Two different form factors(structures) of motherboard

> Which PCB form factor do you want to buy to make a computer?

1️⃣ **ATX**

[![image.png](https://i.postimg.cc/3xZnSCKz/image.png)](https://postimg.cc/NK56LX2x)

- Advanced Technology Extended
- the `Extention slots` are **perpendicular** to the `RAM`
- 🛠️ Used more these days

2️⃣ **BTX**

[![image.png](https://i.postimg.cc/XJqHyG0b/image.png)](https://postimg.cc/34MCswRS)

- `microprocessor`: the micro chip is shown as a diamond
- the `Extention slots` are **parallel** to the `RAM`
- not many computers select `BTX` these days
- 👎🏻 `BTX` has a worse air flow than `ATX`
- 👎🏻 more heat, has worse ventilation
- 🛠️ `BTX` is still used in servers
- so server rooms are very cold
- but `ATX` is more preferred for personal computer

✔️ There were more form factors, like `DTX`, but failed to become commercial

3️⃣ **IXT**

- Model based on ATX, without so many extension slots
- No extension slot
- example: we cannot add `ecography card` to the phone

```
❓ What is a form factor that the RAM and the exention slot are perpendicular?
- ATX

❓ What is a form factor that the RAM and the exention slot are parallel?
- BTX
```

#### ✔️ Size of motherboard

[![Screenshot-2025-10-08-at-16-57-52.png](https://i.postimg.cc/ZYr7vhGB/Screenshot-2025-10-08-at-16-57-52.png)](https://postimg.cc/8szBxxPN)

- put a size of motherboard before `ATX/BTX`
- example: `Standard ATX`

- `Standard ATX`: normal size computer
- `Micro ATX`: tablet
- `Mini ATX`: smaller tablet
- `Nano ATX`: phone
- `Pico ATX`: smart watch
- There were more sizes, but they did not become commercial

```
❓ What is the smallest motherboard?
- Pico ITX
- ⭐️ The sizes orders will be in the exam
```

## ☑️ Two different connectors to supply

[![Screenshot-2025-10-08-at-17-21-34.png](https://i.postimg.cc/RZHNv9sb/Screenshot-2025-10-08-at-17-21-34.png)](https://postimg.cc/dhJqBMK8)

- All mother boards need both `ATX-P1` and `ATX-P2`, mandatory
- `ATX-P3` is optional, is an extra distributor to energy
- 🗺️ connectors are always close to the component they feed

1️⃣ **ATX-P1**

- If you are using `ATX` motherboard
- has 24 pins
- 🛠️ to supply electricity to the mother board
- there is a place to connect normally on the East
- 🗺️ close to the motherboard

2️⃣ **ATX-P2**

- has 4 pins, but sometimes has 6 pins
- 🛠️ to give extra electricity to the motherboard
- give extra electricity for the micro processor
- 🗺️ close to CPU(micro processors)

3️⃣ **ATX-P3**

- optional
- an extra distributor to energy
- extra wire distribute extra energy to extra components
- example: to `extra HDDs`, `extra DVDs`

## ☑️ Sockets

- structure to insert the micro-processor

#### ✔️ Two different types of sockets

1️⃣ **PGA**

> Pin Grid Array

[![image.png](https://i.postimg.cc/kXkg1zMn/image.png)](https://postimg.cc/QHJDV6WP)

- If the socket is PGA
- the micro-processor has the pins(male)
- and the socket has the holes(female)

2️⃣ **LGA**

> Land Grid Array

[![image.png](https://i.postimg.cc/Kc1K0n7M/image.png)](https://postimg.cc/bdjNJSBy)

- micro-processor is female
- socket is male(pins on the land)

3️⃣ **ZIF**

> Zero Insertion Force

[![image.png](https://i.postimg.cc/d3jg27Vx/image.png)](https://postimg.cc/sG1nygSY)

- most of the sockets these days have a levering structure
- and the levering structure helps the insertion of the micro-processor to the motherboard

[![IMG-7572.jpg](https://i.postimg.cc/qR6LGv8d/IMG-7572.jpg)](https://postimg.cc/WFjgNjW9)

- So we have `ZIF PGA` and `ZIF LGA`

❓ **How do we position the micro processor on the motherboard?**

- The micro processor has a small golden triangle
- There is a triangle in the micro processor
- that has to match/fit the triangle on the socket

## ✅ B. RAM Memory(Main Memory)

- `RAM` comes in cards
- 🛍️ When we buy a RAM, we have to look at the **slots** of the mother board
  - if same two sets ➡️ SIMM
  - different size of sets, more than two sets ➡️ DIMM
  - need to be encapsulated ➡️ RIMM

#### ✔️ Three types of RAM depending on the physical structure

1️⃣ **SIMM**

> Single Inlay Memory Module

[![image.png](https://i.postimg.cc/q77mYbvf/image.png)](https://postimg.cc/YvJfLxF8)

- always 2 sets of pins
- two sets of pins of the same size
- very old version of SIMM can have only one set of pins

2️⃣ **DIMM**

> Double Inlay Memory Module

[![image.png](https://i.postimg.cc/CxnTtxPq/image.png)](https://postimg.cc/G4R5Td1L)

- the size of the pins are **different**
- and there can be more than two sets/portions

3️⃣ **RIMM**

> Rambus Inlay Memory Module

[![image.png](https://i.postimg.cc/vZCgFDGk/image.png)](https://postimg.cc/rDCF5V0N)

- everything is hidden
- **encapsulated**
- 👍🏻 RIMM's capsule helps with the airflow
- 🛠️ RIMMs are used for RAMs that need better ventilation
- 🛠️ Computers dedicated to graphic design, architecture(more heat) use RIMM for better ventilation

#### ✔️ Three types of RAM depending internal technology

> Depending on **HOW a RAM works**(internal technology)

✔️ **Frequency**: The final speed of the RAM

1️⃣ **SDRAM**

> Synchronized Dynamic Random Access Memory

- `Random`: address is not decided in order, can access address/directions randomly, not in order
- `Synchronized`: the RAM is synchronized with the clock
- Synchronized does not mean it has 2GHz like the clock ❌
- Synchronized means that RAM only works when the clock changes from `0` to `1` ⭕️
- Thus, the speed of this SDRAM is slow 🐢
- only `133MHz`
- I can only access `133Mega times per second` to the RAM

- 👎🏻 Nowadays, SDRAM exists, but considered very slow

2️⃣ **DDR**

> Double Data Rate

- `Double`: you can have **two reads or writes** at the same time
- the speed would be same `133MHz`, but you can read/write 2 times
- 🐇 more faster than SDRAM

- these days we have `DDR-2`, `DDR-3`, `DDR-4`, `DDR-5`...
- `DDR-n` means `n to the power of 2`
- `DDR-2`: you can read/write `2^2` times at the same time
- `DDR-3`: you can read/write `2^3` times at the same time
- `DDR-4`: you can read/write `2^4` times at the same time
- `DDR-5`: you can do `2^5` read/writes at the same time
- the frequency would be highest in `DDR-5`

- Nowaways, faster RAMs would come in modern format, which is `DIMM`

```
❓ Which is the fastest speed we can get in a RAM?
A: RAM would be DDR-5
A: speed would be 133MHz * 32
```

```
❓ What do you say when you go to buy a RAM?
- I want a DIMM, DDR-5
```

3️⃣ **RDRAM**

> Rambus Dynamic RAM

- RAM that is encapsulated
- interal technology of the RIMM
- speed: around 1GHz
- 🛠️ Design, Architecture
- 👍🏻 Encapsulated, fast, good ventilation

## ✅ C. Chipset

## ✅

## ✅

## ✅

## ✅

#### ✔️

1️⃣
2️⃣
