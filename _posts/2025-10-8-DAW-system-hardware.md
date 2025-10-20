---
title: 1.12 Hardware specifications_1
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

## 📌 A. Motherboard, Printed Circuit Board

> main board of the computer <br>
> also called Printed Circuit Board `PCB`

- normally mother boards contain
  - `microprocessor`: north
  - `RAM`: at the east
  - `Expansion slots`: some slots for extending the capabilities according to your needs(`TV card`, `ecography card` for hospitals, `vibration measurement card` for measuring earthquakes...)

### ☑️ Two different form factors(structures) of motherboard

> Which PCB form factor do you want to buy to make a computer?

#### 1️⃣ **ATX**

[![image.png](https://i.postimg.cc/3xZnSCKz/image.png)](https://postimg.cc/NK56LX2x)

- Advanced Technology Extended
- the `Extention slots` are **perpendicular** to the `RAM`
- 🛠️ Used more these days

#### 2️⃣ **BTX**

[![image.png](https://i.postimg.cc/XJqHyG0b/image.png)](https://postimg.cc/34MCswRS)

- `microprocessor`: the micro chip is shown as a diamond
- the `Extention slots` are **parallel** to the `RAM`
- not many computers select `BTX` these days
- 👎🏻 `BTX` has a worse air flow than `ATX`
- 👎🏻 more heat, has worse ventilation
- 🛠️ `BTX` is still used in servers
- so server rooms are very cold
- but `ATX` is more preferred for personal computer
- ↔️ the distribution of heat

✔️ There were more form factors, like `DTX`, but failed to become commercial

#### 3️⃣ **IXT**

- Model based on ATX, without so many expansion slots
- No expansion slot ❌
- example: we cannot add `ecography card` to the phone

```
❓ What is a form factor that the RAM and the exention slot are perpendicular?
- ATX

❓ What is a form factor that the RAM and the exention slot are parallel?
- BTX
```

### ☑️ Size of motherboard

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

## ✅ Two different connectors to supply

[![Screenshot-2025-10-08-at-17-21-34.png](https://i.postimg.cc/RZHNv9sb/Screenshot-2025-10-08-at-17-21-34.png)](https://postimg.cc/dhJqBMK8)

- All mother boards need both `ATX-P1` and `ATX-P2`, mandatory
- `ATX-P3` is optional, is an extra distributor to energy
- 🗺️ connectors are always close to the component they feed

#### 1️⃣ **ATX-P1**

- If you are using `ATX` motherboard
- has **24 pins**
- 🛠️ to supply electricity to the **mother board**
- there is a place to connect normally on the East
- 🗺️ close to the motherboard

#### 2️⃣ **ATX-P2**

- has **4 pins**, but sometimes has 6 pins
- 🛠️ to give **extra** electricity to the **micro processor**
- give extra electricity for the micro processor
- 🗺️ close to CPU(micro processors)

#### 3️⃣ **ATX-P3**

- optional
- an extra distributor to energy
- extra wire distribute **extra energy** to extra components
- example: to `extra HDDs`, `extra DVDs`

## ✅ Sockets

- where to put the CPU
- structure to insert the micro-processor

### ☑️ Two different types of sockets

#### 1️⃣ **PGA**

> Pin Grid Array

[![image.png](https://i.postimg.cc/kXkg1zMn/image.png)](https://postimg.cc/QHJDV6WP)

- If the socket is PGA
- the micro-processor has the pins(male)
- and the socket has the holes(female)
- pins are in the micro processor

#### 2️⃣ **LGA**

> Land Grid Array

[![image.png](https://i.postimg.cc/Kc1K0n7M/image.png)](https://postimg.cc/bdjNJSBy)

- micro-processor is female
- socket is male(pins on the land)

#### 3️⃣ **ZIF**

> Zero Insertion Force

[![image.png](https://i.postimg.cc/d3jg27Vx/image.png)](https://postimg.cc/sG1nygSY)

- most of the sockets these days have a levering structure
- and the levering structure helps the insertion of the micro-processor to the motherboard

[![IMG-7572.jpg](https://i.postimg.cc/qR6LGv8d/IMG-7572.jpg)](https://postimg.cc/WFjgNjW9)

- So we have `ZIF PGA` and `ZIF LGA`

```
❓ How do we position the micro processor on the motherboard?

- The micro processor has a small golden triangle
- There is a triangle in the micro processor
- that has to match/fit the triangle on the socket
```

## 📌 B. RAM Memory(Main Memory)

- ✔️ Two ways of distinguishing RAM
  - depending on physical structure
  - depending on internal technology

### ☑️ Three types of RAM depending on the physical structure

- `RAM` comes in cards
- 🛍️ When we buy a RAM, we have to look at the **slots** of the mother board

  - if same two sets ➡️ SIMM
  - different size of sets, more than two sets ➡️ DIMM
  - need to be encapsulated ➡️ RIMM

#### 1️⃣ **SIMM**

> Single Inlay Memory Module

[![image.png](https://i.postimg.cc/q77mYbvf/image.png)](https://postimg.cc/YvJfLxF8)

- always 2 sets of pins
- two sets of pins of the same size
- very old version of SIMM can have only one set of pins

#### 2️⃣ **DIMM**

> Double Inlay Memory Module

[![image.png](https://i.postimg.cc/CxnTtxPq/image.png)](https://postimg.cc/G4R5Td1L)

- the size of the pins are **different**
- and there can be more than two sets/portions
- can have three portions

#### 3️⃣ **RIMM**

> Rambus Inlay Memory Module

[![image.png](https://i.postimg.cc/vZCgFDGk/image.png)](https://postimg.cc/rDCF5V0N)

- everything is hidden
- **encapsulated**
- 👍🏻 RIMM's capsule helps with the airflow
- 🛠️ RIMMs are used for RAMs that need better ventilation
- 🛠️ Computers dedicated to graphic design, architecture(more heat) use RIMM for better ventilation

### ☑️ How to measure a RAM

✔️ **Frequency**: The final speed of the RAM

- How many times per second we can access the RAM(`Hertz`)
- example: I can access the RAM 1 time per second
- How often I have an appointment with the RAM

✔️ **Latency**:

- How much I have to wait before getting data from the RAM
- waiting time, once you are inside the RAM, once you have access to the RAM, before getting the information
- measured in `nano seconds`
- nano second: `0.000 000 001 second` = `1 * 10^(-9) seconds`

✔️ **Word width**:

- number of bits per address/in each address of the RAM
- how much data we can save per address in a RAM
- length of the data we can save on one address of the RAM

✔️ **Bandwidth**:

- combination of all the `frequency`, `latency`, `word width`
- `Giga bits/second` = `Gbps`
- how much data, real amount of data you can read/write per second

```
👉🏻 Thus, an ideal RAM is

high frequency ⬆️
low latency ⬇️
word width ⬆️
high bandwidth ⬆️
```

✔️ **Channeling**

- combination of RAM cards
- in order to increase
- combine several RAM cards to increase capacity of memory
- **Multi Channeling**
- ✔️ Dual Channel: two sets of two cards, so we have 4 RAMs
- ✔️ Triple Channel: three sets of two cards, so we have 6 RAMs
- ✔️ Quadruple Channel: four sets of two cards, so we have 8 RAMs

[![Screenshot-2025-10-15-at-17-35-09.png](https://i.postimg.cc/Pr7ZPMKF/Screenshot-2025-10-15-at-17-35-09.png)](https://postimg.cc/xcKqZMwK)

[![image.png](https://i.postimg.cc/0j8G02JD/image.png)](https://postimg.cc/0MBJ8vny)

- All the RAM cards that are combined, so in the same color should be equal
- equal means: same frequency, same latency, same wordwidth, same capacity, same age(time used)
- Recommended, so if you are going to change one RAM, change the others too!

- memory controller, system agent block would help channeling

✔️ **Capacity**

- RAM of `32bits` is `4GB`
- so capacity is measured in `GB`

### ☑️ Three types of RAM depending internal technology

> Depending on **HOW a RAM works**(internal technology)

#### 1️⃣ **SDRAM**

> Synchronized Dynamic Random Access Memory

- `Random`: address is not decided in order, can access address/directions randomly, not in order
- `Synchronized`: the RAM is synchronized with the ⏰ **clock**
- Synchronized does not mean it has 2GHz like the clock ❌
- Synchronized means that RAM only works when the clock changes from `0` to `1` ⭕️
- Thus, the speed of this SDRAM is slow 🐢
- ⭐️EXAM⭐️ only `133MHz` = `133 million times per second`
- I can only access `133Mega times per second` to the RAM
- **Frequency**: This is called the **Frequency** of the RAM

- 👎🏻 Nowadays, SDRAM exists, but considered very slow

#### 2️⃣ **DDR**

> Double Data Rate RAM

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

#### 3️⃣ **RDRAM**

> Rambus Dynamic RAM

- RAM that is encapsulated
- interal technology of the `RIMM`
- Frequency: around **1GHz**
- this RAM would read/write `1000million times per second`
- 🛠️ Design, Architecture
- 👍🏻 Encapsulated, fast, good ventilation

#### 💡 SO-DIMMS

- DIMM for laptops
- smaller DIMM for laptops

## 📌 C. Chipset

> Only _traditional_ motherboards have north bridge and south bridge <br>
> Set of chips you can find on the motherboard <br>
> purpose: **helpers** of the CPU, help the micro processor, CPU <br>

- In the traditional motherboard `PCBs`,
- chipset is a set of two bridges

- In chipsets, there are two parts
- north bridge and the south bridge
- north: in charge of elements that need more efficiency
- south: in charge of elements that can be a bit slower

[![image.png](https://i.postimg.cc/RZtfkH97/image.png)](https://postimg.cc/MnWvRXnH)

[![Screenshot-2025-10-15-at-17-36-47.png](https://i.postimg.cc/CMXL86TK/Screenshot-2025-10-15-at-17-36-47.png)](https://postimg.cc/0rGsRnNg)

[![Screenshot-2025-10-15-at-17-41-14.png](https://i.postimg.cc/0j83Kvk3/Screenshot-2025-10-15-at-17-41-14.png)](https://postimg.cc/FdBGw2Jg)

#### 1️⃣ North Bridge

> has two jobs, 1️⃣ help fast work for CPU, and 2️⃣ responsible for south bridge

- 1️⃣ help with high speed elements
- help important elements of the motherboard
- processor is in the north, so north bridge is also in the north, close to the processor

- 🥵 gets more warmer
- we need to ventilate, refrigirate
- so it has a structure of a corridor
- need airflow
- ✔️ **Heat sink**: to provide airflow, ventilation for the north bridge
- purpose of heatsink: create airflow, for refreshing

- 2️⃣ north bridge is also in charge of controlling the south
- north is in charge of supplying the south

❓ **What is controlled by the north bridge?**

- `Memory controller`: for controlling several RAMs
- `Graphic cards and expansion cards` are normally inserted in the expasion slots
- `Front side bus`: for communication among cores
- `Peripherals in Transport bus`: for peripherals in multicore

❓ **If south bridge and north bridge is helping CPU, then what does the CPU do?**

- CPU: backside bus + ALU + CU
- and rest of the work would be helped by south bridge and north bridge

#### 2️⃣ South Bridge

- Sometimes South bridge is called `Input Output Controller(I/O controller)`

- relatively not so fast, not so important parts of the processor
- situated in the south of the motherboard

- does not need as much as ventilation
- does not get so hot
- does not have heatsink

❓ **What is controlled by the south bridge?**

- `Peripherals in mono-core`, can be slower, normal keyboard
- `External connectors` in the motherboard
- `BIOS`: booting system of the computer

## 📌 External connectors

> connect to audio, internet, USBs, mouse, keyboard...

[![image.png](https://i.postimg.cc/7PMTnk9t/image.png)](https://postimg.cc/hhvjKNHV)

- at the west side of the motherboard(left)
- there are lots of connectors for the peripherals
- in the motherboard, there are connectors for the external connectors
- green for earphones

- all the external connectors connect to the **south bridge** of the **chipset**

- In a computer `all-in-one` (computer with no tower, like the one in Clara Del Rey)
- the motherboard is placed differently
- so for connecting USBs, peripherals, they are behind the screen

## 📌 Modern PCBs

- in modern PCBs, there is no north bridge nor south bridge

[![image.png](https://i.postimg.cc/PrfsPWN8/image.png)](https://postimg.cc/6TP1PGr9)

#### ✔️ North bridge

> inside CPU, control MC only

- the north bridge inserted/internal in the CPU/processor
- so we do not see
- but as it is inside the CPU, north bridge only controls the Memory Controller

#### ✔️ Platform controller HUB(PCH)

> South bridge works more, needs ventilation, change name to PCH

- and the south bridge gets all the job of the traditional north bridge
- and does all the work
- it becomes very very powerful
- 🥵 and now south needs the ventilation
- now called **Platform controller HUB(PCH)**

## 📌

## 📌

### ☑️

#### ✔️

#### 1️⃣

#### 2️⃣

#### 3️⃣
