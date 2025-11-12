---
title: 2.8 Process Dispatch
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

## 📌 Process Management 
> 🟰 Process Dispatch <br>
> planificacion de processes

- once the process are in the RAM, I need to give them a certain order to run
- all processes need to be run

- ✔️ **Goal of Process Dispatch**
- once the processes are in the RAM
- Organizing all the processes to run/end successfully
- Important that user feels everything runs smooth, 
- smooth: all processes is running at the same time

- ✔️ **The processes in the RAM have different priorities**
- In the RAM, there are processes you know that they are going to fail
- ❓ Should I pay attention to them with high priority?
- No, leave them fail, give them know priority at all

- Other processes can have urgency, priority
- 1️⃣ Some urgent processes can be solved **without** the intervention of the CPU
- Some processes can be solved by another/other computer compoenent/resources

- 2️⃣ And the other urgent processes need to be priorized by the CPU
- CPU needs to think of the **consequences** of the intervention 
- in order to give priority to the processes
- **consequences**: Maybe if the CPU does not interrupt, the urgent process might die, so this process has priority
- ☠️ goal is not to let any process die! 

- ✔️ **Aging**
- Aging: letting a process get old is ok
- make a process wait is ok
- Some processes age
- if they do not die, its ok
- So CPU has to take consequences, aging into account before intervention

- ✔️ ** Standard Processes**
- Standard Processes 🟰 not urgent processes
- Not urgent processes are left for the left

## 📌 Process Table
> stored inside `OS in RAM`

- also `.csv` file like `pages table`
- data seperated by `, commas`
- but bc it is so complicated, we draw the `process table` like a real table

- ✔️ **PCB**
- the `process table`  has a portion for each of the processes
- The block is called `PCB, Process Control Block`
- the `PCB` has information about the process

```
Process Table
block for p1 = PCB1
block for p2 = PCB2
block for p3 = PCB3
```

- ✔️ **Inside the `PCB` we have fields**

[![Screenshot-2025-11-12-at-15-48-25.png](https://i.postimg.cc/jd2sJ0Mb/Screenshot-2025-11-12-at-15-48-25.png)](https://postimg.cc/7fvvpcvs)

- fields of the processes
**(1) PID**
- process ID
- name of the process

**(2) Parent Process ID**
- the name of the process I come from/was born from
- ID of my parent process
- If I am malware, kill me, my parent, my children process
- 👉🏻 `Parent Process ID` and `Pointer to the BCP Child` is stored in `PCB` for the `3 generation killing technique`

**(3) Pointer to the BCP Child**
- the processes I created
- my children processes
- so where my children processes are located in the RAM
- pointer: address of the memory, address of position of the RAM
- If I am malware, kill me, my parent, my children process
- 👉🏻 `Parent Process ID` and `Pointer to the BCP Child` is stored in `PCB` for the `3 generation killing technique`

**(4) Process state**

[![Screenshot-2025-11-12-at-16-07-33.png](https://i.postimg.cc/3JGt19Jk/Screenshot-2025-11-12-at-16-07-33.png)](https://postimg.cc/gnYykVhp)

- There are 6 different states
    - 1️⃣ `new`: when process has just swapped into the RAM
    - 2️⃣ `execution`: when process has the CPU, **foreground(primer plano)**
    - 3️⃣ `waiting`: another process has the CPU foreground, so I have to wait, so the process is in **background(segundo plano)**
        - some processes can be executed in the background, they are being executed but do not have the CPU
        - 👀 automatic processes called **deamons/services**
        - deamons: processes that be executed in the background automatically, without CPU
        - in linux, they are called deamons
        - in windows, they are called services

    - 4️⃣ `FOK: Finished OK`: when the process finishes, `swap out` of the RAM
    - 5️⃣ `FKO: Finished Not ok`: does not finish ok, finish bc it has an error, or the user forces it to finish
        - 👀 process with an error, or administrator finishes bc it is collapsing the computer
        - the process is `swapped out` from the RAM radically, forcefully
    - 6️⃣ `Blocked`: 
        - (1) when the process is waiting for user interaction 
            - when the user accepts, the process goes back to `execution` state, and continue executing
            - when the user cancels, the process becomes `FKO`
            - finished forcefully
        - (2) when the process is waiting for the peripheral
            - 👀 you are printing and the printer is out of paper
            - the printing process is waiting for the peripheral (printer) to be solved, to have paper again
        - (3) sometimes processes are blocked bc of another processes

**(5) Priority**
- presented in integer
- in linux, priority is a number from `-19 ~ 23`
- in other OS, priority goes from `0 ~~ onwards`
- ⭐️ In computing, `0` priority is the highest priority
- In linux, `-19` is the top priority 

- ❓ **How do you fight aging of a processes?**
- aging: CPU does not pay attention to the process for a long time
- die: SWAP OUT
- 👉🏻 **Improve the priority** of the process that are old
- 👉🏻 Improving prioity⬆️ means making my priority number smaller⬇️, make me `0`

**(6) Main Memory Pointers**
- Pointer: addresses of the RAM where the process has portions
- pointers point to the beginning to the address that the process is located
- pointers point to the base register(expressed in hexadecimal)
- but not in frames, it is written in hexadecimal
- 👍🏻 more secure
- MMP acts like a backup, written two times in `page table base register` and `hexadecimal in PCB`

**(7) Program Counter**
- indicator of which instruction was last executed
- backup of the PC in the neuman machine CU

**(8) I/O status**
- keeps information about the peripherals
- 👀 when I am writing on word, but I minimize and then maximize again
- the cursor is still blinking where I stopped. 
- This is using the `I/O status`
- 👀 when I was playing music on youtube
- but I run another application, then I come back to youtube, 
- youtube has where I stopped the music, instead of playing the music from the beginning again
- This is done using the `I/O status`

**(9) Accounting Info**
- 1️⃣ **how much CPU** I am using
- If one process occupies 99% if the CPU and does not stop, you can `FKO`
- the process that takes too much of CPU, the computer collapes, you can expel
- 2️⃣ the **Bytes** that the program(when it was closed) occupied in the Harddisk
- the size of the program in the HD
- to check if the process is occupying too much space in the secondary memory
- 3️⃣ **owner** of the program
- 👀 Microsoft for word, excel
- 4️⃣ **Permission**
- what that process can do on my computer
    - if permission is `r : read`, the process can only read information
        - 👀 adobe reader, you cannot modify PDFs, you can only read
        - bc the permission is `r`
    - if permission is `w : write or modify`, the process can write and modify on the computer
        - some processes with the `w` permission, sometimes you can `delete`
        - but the other processes, if the file has `honey`, you cannot delete it
    - if permission is `x : execute`, the process can execute things, create children processes


- 👀 **EXAMPLE**

```
PCB1 = P1, P3, Ex, 0, FAh, FBh, screen10*20, 90, 2MB, todovirus, w, P4, P5

name of the process: P1
parent: P3
Execution(state)
priority 0, with top priority
in RAM, stored in FAh
PC is FBh, the process has just started
    the process started in FAh, but if I executed now FBh, only executed a little bit
periperal, screen is doing smth like screen10*20
the process is using 90% of the CPU
small process, only uses 2MB
the creator of the process is toodvirus
the process has writing permission, it can write and modify my data
the process has two children, P4 and P5

👉🏻 You have to stop the process immediately
with top priority
collaping your CPU with 90%,
can modify with write permission

👉🏻 kill P1, P3(parent), P4 and P5(children process)

👉🏻 In case of doubt, the OS is a monarch
if some process looks wierd, they just kill the process
can the process have been innocent? 
Yes, but still, if doubtful, kill
```

## 📌 6 Dispatching Algorithms
> different algorithms of solving a RAM, processes

- These algorithms are also applied to daily situations
- 3 are not preemptive: once a process gets the CPU, no interruptions
    - `FIFO`, `SJF`, `PNPE`
- other 3 are preempritve:(expulsivo)
    - although a process had the CPU, if a process has a higher priority
    - the process gets interrupted
    - `RR`, `SRTF`, `PPE`

## GANTT Diagram
✔️ **GANTT Diagram**
- GANTT Diagram: diagram to show how processes will evolve, will behave
- we need to check in the `processes table` three things
    - 1️⃣ **Time in**: The arriving time of the process to the RAM, the swap-in time 
    - 2️⃣ **Execution time(Tx)**: how many seconds the process needs to exectute
    - 3️⃣ Priority of the process

- The diagram is 2D
- `x`: time
- `y`: process

✔️ How to draw the GANTT Diagram
- step 1: Draw the x: time, y: processes
- step 2: Write the processes in order `P1~P4`
- step 3: Draw the arrival times and guide lines of all the processes
- step 4: Draw the beginning point of the each process
- step 5: ⭐️ Overlapping is forbidden. Cannot have a process on top of another
    - The CPU can only run one process
    - so only one **solid bar**
    - 🆚 solid bar: executing
    - In order to avoid overlapping, the process **wait** until the previous process to finish. 
    - waiting bar is described in **non-solid bars**
    - 🆚 dotted bar: waiting
- From step 6 is continued in each algorithm...

- 🖥️ The computer does not draw any diagrams, just calculates the result table

✔️ Rule of Algorighm
- 1️⃣ Mandatory: `P1` always comes first, always has `TW` of `0`
- 2️⃣ All the algorithm finishes in the number of adding the process execution times
    - `7 + 4+ 3+ 2 = 16`
    - all algormithms must end in 16 seconds
- 3️⃣ If the best algorithm does not use priority, priority is useless in this case. 
    - So priority might not be the best option! Sometimes priority is useless
    - 👀 Wrap up of results
        - FIFO WT: 5.5
        - FIFO RT: 9.5
        - SJF WT: 4.5
        - SJF RT: 8.5
        - PNPE WT: 5.25
        - PNPE RT: 9.25
        - for these four processes, the best is SJF

## ✅ FIFO

> First In First Out <br>
> non-preemptive


✔️ **Rules**
1. The processes are attended in arriving order to the RAM
2. Non-preemptive
3. P1 is always the first to run with the CPU, then P2, P3...

[![Screenshot-2025-11-12-at-17-02-40.png](https://i.postimg.cc/rsLhWr6Z/Screenshot-2025-11-12-at-17-02-40.png)](https://postimg.cc/tZ2tG74F)

- The process that arrives in the second 0
- its a `deamon/service,` automatic process
- the user did not click and run the program ❌
- the process is run automatically
- so `P1` is a `deamon`


✔️ **Draw a GRANTT Table**
- step 6: As we are in FIFO, draw each process
- step 7: Time that processes is run is drawn in **solid bar, and you must indicate the end**
- step 8: Create a `results table` with **waiting time**`TW` and **result time**`TR`
    - waiting time: the dotted bars
    - result time: add dotted bars + solid bars
    - 💡 Mandatory: `P1` always has `TW` of `0`
- step 9: After creating the `results table`, calculate the average waiting time and average result time 
    - average is shown with a bar on top

✔️ **Result of FIFO**
- This means that with the processes `P1~P4`, 
    - FIFO makes them **wait** on **average of 5.5 seconds**
    - and **solve** the RAM in **average 9.5 seconds**



## ✅ SJF

> Shortest Job First <br>
> non-preemptive

✔️ **Rules**
1. Although P4 is the shortest, P1 always first!
    - Even P1 is long, we cannot waste time waiting for P4!
2. After P1, then from short to long

- 👍🏻 lowers the temperature of the computer
- 👍🏻 you can swap the process out of your RAM

✔️ **Result of SJF**
- SJF has lower average `WT` and lower average `RT` ⬇️
- SJF is better for these set of processes
- 🖥️ The computer pre-calculates the 6 algorithms and uses the one that is the most efficient
- The process dispatcher changes continuously from one algorithm to another.


## ✅ PNPE

> Priority Non-Pre-Emptive<br>
> non-preemptive

- In the data table, you need the `priority` from the `processes table`

✔️ **Rules**
1. P1 always runs first
2. When P1 finishes, them from better priority(**low** in number) to worse priority(**high** in number)


✔️ **Result of SJF**


## ✅ RR
## ✅ SRTF

## ✅ PPE

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
