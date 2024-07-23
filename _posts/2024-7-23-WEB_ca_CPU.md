---
title: CPU
categories: [Computer Science, Computer Architecture]
tags: [] # TAG names should always be lowercase
---

## ✅ CPU component

![Screenshot 2024-07-23 at 10 36 12](https://github.com/user-attachments/assets/e6331ca4-2ab2-4fb9-8fe4-2b67e296785f)

### 📍 ALU, CU, MU

#### **ALU (Arithmetic Logic Unit)**

연산, AND, OR, and NOT

#### **CU (Control Unit)**

- **manages** and coordinates the operations of the CPU
- directing the operation of the other components within the CPU to execute the instructions of a program
- CU & ALU 연산의 **순서 조정**
- decodes order, sends the order to according units(memory unit, ALU, Input/Output devices)

#### **MU (Memory Unit), Register**

> small set of data holding place
> for fast data processing by CPU

- 고속 기억장치
- 연산하다가 작은 값들 저장해두기

- Types of Registers
  - Accumulator: register for storing arismetic data
  - MAR: Memory Address Registers
    - holds address of location to be accessed from memory
    - MAR and MDR facilitate communication between CPU ↔️ memory
  - MDR: Memory Data Registers
    - save data to be written into or to be read out from addressed location
  - PC: Program Counter
    - contain memory of next instrucion to be fetched
  - IR: Instruction Register
    - holds instruction that is just about to be executed

#### ➕ CPU clock frequency

- CPU의 동작 속도
- ALU, CU, MU가 유기적으로 동작하는 것을 1사이클이라고 쳤을 때  
  1Hz(1초에 한 사이클) = 1cycle/s  
  헤르츠가 높으면 높을수록 1초안에 여러번 돈다는 것이니 성능이 더 좋은 것이다.

#### ➕ CPU multi-core

- CPU안에 여러 개의 코어가 있다.
- CPU 코어: ALU, CU
- CPU 코어가 많을수록, 멀티코어일 수록 성능이 좋다.

## 💡 Reference

<https://www.geeksforgeeks.org/different-classes-of-cpu-registers/?ref=header_search>
