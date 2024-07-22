---
title: Computer architecture
categories: [Computer Science, Computer Architecture]
tags: [backend] # TAG names should always be lowercase
---

![IMG_A3186294B3EA-1](https://github.com/soheeparklee/personal_project_musicApp/assets/97790983/ca894f5f-c365-4e37-923f-55627b99a4fc)

## ✅ Computer architecture

### ☑️ CPU

> central processing unit

- 의사결정 및 계산
- 중앙처리 장치, 프로세서
- 논리회로들로 구성되어 있음

#### 📍 ALU, CU, MU

CPU는 ALU, CU, MU가 유기적으로 동작하며 output(의사결정, 연산)이 나온다.  
<br>

- **ALU (Arithmetic Logic Unit)**  
  연산, AND, OR, and NOT

- **CU (Control Unit)**  
  manages and coordinates the operations of the CPU  
  directing the operation of the other components within the CPU to execute the instructions of a program  
  CU & ALU 연산의 순서 조정

- **MU (Memory Unit)**
  연산하다가 작은 값들 저장해두기

#### ✔️ CPU clock frequency

- CPU의 동작 속도
- ALU, CU, MU가 유기적으로 동작하는 것을 1사이클이라고 쳤을 때  
  1Hz(1초에 한 사이클) = 1cycle/s  
  헤르츠가 높으면 높을수록 1초안에 여러번 돈다는 것이니 성능이 더 좋은 것이다.

#### ✔️ CPU multi-core

- CPU안에 여러 개의 코어가 있다.
- CPU 코어: ALU, CU
- CPU 코어가 많을수록, 멀티코어일 수록 성능이 좋다.

### ☑️ Memory

#### 📍 Hierarchy of memory

- Registers: smallest, fastest memory within CPU
- Cache: faster than RAM, multiple levels(L1, L2, L3)
- RAM: main memory
- Secondary Storage: HDD, SSD
- Tertiary Storage: external storage(USB)

#### 📍 RAM

> random access memory

- random access: any memory cell can be accessed directly
- temporary storage
- primary memory(주 기억장치)
- volatile memory
- 전기 제어(전기로 데이터가 저장, 전기 없으면 데이터 손실)

<br>

- Loading Data: when open program, data is loaded from HD to RAM
  - why? bc RAM is faster
- Execution: CPU caculates, results on RAM
- Temporary Storage: temporarily holds data that CPU might need imminently, long storage data will go to HD.

##### ✔️ shell

- shell영역에 데이터가 저장이 된다.

##### ✔️ Ram Data Rate frequency

- 램의 속도  
  마찬가지로 1Hz(1초에 한 사이클) = 1cycle/s

##### 📍 SRAM (Static RAM)

> "static" because it doesn't need to be refreshed constantly to maintain its contents, unlike DRAM.

- 속도: 매우 빠르다
- 보존: 비 휘발성(전기가 없어도 데이터가 사라지지 않는다.)
  단, 데이터를 보기 위해서는 전원 공급이 필요함.
- 용량/가격: 구조가 복잡해 용량이 크지 않고 비쌈
- 용도: **CPU내부 Cache memory**
- smaller, high-speed cache

##### 📍 DRAM(Dynamic Ram)

> "dynamic" because the capacitors need to be periodically refreshed to maintain the data, as the charge stored in them tends to leak away over time.

- 속도: 충분히 빠르다
- 보존: 휘발성(전기가 들어오지 않으면 데이터 사라짐!)
- 용량/가격: 구조가 비교적 간단해 용량이 적당히 크고, 비교적 싸다
- 용도: **Main memory**
- more cost-effective and used for main system memory where larger capacity is crucial.

#### 💡 cache memory

small sized volatile memory  
serve as a buffer between the main memory (RAM) and the central processing unit (CPU)  
faster access to data than fetching it from the main memory  
multiple levels(L1: fastest, smallest)

### ☑️ Disk

- 장기 기억 Hard Disk
- Secondary Memory
- 보조 기억장치
- HDD, SSD 둘을 같이 사용하기도 함.
- 로딩하는데 오래 걸리는 데이터는 HDD, 자주 써서 금방금방 로딩되는 데이터는 SSD에 저장

#### 📍 HDD

> Hard Disk Drive

- 저장방식: magnetic storage
- slow, cheap
- 가격: 저렴
- 전력 소비: 자기장의 원리이나까 전력 소비 적음
- 속도: 느림
- 용도: 장기 보존

#### 📍 SSD

> Solid State Drive

- 저장방식: flash memory for storage
- faster, more expensive, better durability
- 가격: HDD에 비해 8배정도 비쌈
- 전력 소비: 많음
- 속도: 빠름
- 주의: 전기로 활용하는 면이 있어 데이터 자연 소멸 가능!!

## ❓ Word 프로그램을 클릭하면 일어나는 일?

- 장기 기억 Hard Disk에 저장되어 있던 워드 프로그램을 불러온다. 데이터 호출
- 동작하기 위해서는 RAM(= 메모리)에 업로드 되어 입력할 수 있는 상태가 된다.
- 키보드로 이것저것 입력을 하면 CPU에서 연산을 하여 기계어를 해석해 보여준다.
- 종료를 하면 CPU는 작업을 멈추고 저장을 하면 RAM의 데이터들이 장기 기억 Hard Disk에 저장
- 완전히 종료되면 RAM에는 워드 데이터들이 남지 않음.
