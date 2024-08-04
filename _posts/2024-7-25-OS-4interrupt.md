---
title: Interrupt
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ Interrupt

> signal emmited from hardware or software when process or event needs immediate attention<br>
> if an error occurs during running a program<br>
> stop the program<br>
> and alert CPU for immediate attention<br>
> allow processor to act quickly<br>

- **Interrupt Detection:**
  - device raises `interrupt` at `process i`
- **Interrupt Acknowledgment:**
  - CPU sends device acknowledgement sign
  - device stops sending interrupt request signal
- **Interrupt Handling**
  - processor first completes execution of `process i`
  - address of interrupted instruction move to temporary location
  - processor handles interrupt
- **Context Saving, Transfer Control**
  - processor loads `Program Counter` with the address of first instructino of the ISR
- **Interrupt Servicing**
  - after handling interrupt, processor can continue with `process i+1`

## ✅ Types of Interrupt

1. Software Interrupts
   > interrupt produced by software <br>
   > also called **Trap** <br>

- command, data w error
- divide by 0, overflow, exceptions

2. Hardware Interrupts

> occurs bc of external cause

- i/o device, timing device, power

## ✅ Managing Multiple Devices

> when more than one device raises interrupt <br>
> additional info is needed to decide which device to be considered first <br>

### ✔️ Polling

- first devide encountered with the IRQ bit set has priority
- easy to implement
- lot of tame is wasted by interrogating the IRQ bit of all devices

### ✔️ Vectored Interrupts

- device requesting interrupt
- and identifying directly by sending special code to processor over the bus

### ✔️ Interrupt Nesting

- device is organized in a priority structure

## 💡 Reference

<https://www.geeksforgeeks.org/interrupts/>
