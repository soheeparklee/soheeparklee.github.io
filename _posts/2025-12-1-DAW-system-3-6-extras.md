---
title: 3.6 OS Managers and HW visualizations
categories: [DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

> Extra things to check

- we can see things hidden by transparancy levels

## 📌 Memory Manager

- to check paging, segmenatation

[![Screenshot-2025-12-01-at-17-41-01.png](https://i.postimg.cc/MGJxRYmC/Screenshot-2025-12-01-at-17-41-01.png)](https://postimg.cc/LJDrFL7D)

#### 1️⃣ How to check memory manager 1\_ task manager

- Use task manager

```
Ctr+Alt+Supr>Administrador tareas > performance(rendimiento label) > memory
```

✔️ **In task manager you will find the following things**

- top right corner: capacity in RAM
- `paged block`: how much of RAM is using paging
- `non-paged block`: how much RAM is using segmentation

- `speed`: not frequency of access

  - means speed taking into account the delays

- `slots used/ranuras usadas`: if you can add more cards or not
- `reservada para hardware`: size of the OS in RAM
- `cache`: size of the disk cache, free portion of the RAM used for frequent applications, helps the harddisk

#### 2️⃣ another way of checking memory manager_resmon

- use test resmon
- `windows` + `R` + `resmon`
- resmon: resources monitor

✔️ **In resmon you will find the following things**

- name of the process
- `PID`
- how many errors the process had
- how much the process occupies the RAM(different occupations of the process in the RAM)

✔️ **In the important errors window**

- errores grave
- in the right down corner
- you will the see IPCs in the kernel, due to the processes in the RAM

- if there is a peak in the IPCs window
- and the peak disapeears,
- it means the kernel solved the problem

- If you see a lot of IPCs, a lot of peaks
- 💊 save what you have been working on, and reboot your copmuter
- so you can clean your computer

## 📌 Process manager visualization

Dispatcher

- use **task manager**

#### ☑️ process label

- we can see the list of all the processes
- we can see both `user processs` + `internal processes`(`deamons/services`)

✔️ for each of the processes we can see the the following

- percent of CPU used
- percent of RAM used
- percent of secondary memory used
- percent of network used
- percent of CPU used
- percent of energy used

✔️ **Kill and SIGKILL**

- If we choose a process and click on `end task/finalizar tarea` we can kill a process
- this is killing a process with a command `KILL`
- however, this is different from killing a process with `KILL-SIGKILL`
- command `KILL` will end a process, but the processes will leave traces
- so you can maybe later check
- whereas, `KILL-SIGKILL` will kill the process without leaving any traces

✔️ **Forensic Analysis**

- so when a system expert looks for traces
- for rebringing, restarting processes,
- he is doing Forensic Analysis

#### ☑️ Details

- name of process
- PID
- state of process
- CPU/ RAM consumption
- name of the user
- if it is using Virtual Memory or not

```
choose the details screenshot
and for the process with the smallest PID
tell me the state and if it is using the VM or not
```

#### ☑️ services label

- we only see deamons
- we do not see user services

- deamon(process) name
- PID
- description
- state of the deamon
- group of the deamon

## ✅ to check processes command

- `Windows` + `R` > cmd > tasklist

- tasklist shows
- both `internal/deamons` + user services
- process name
- PID
- memory use

```
use tasklist
What is the smallest PID, and what is its RAM usage?
```

## 📌 Interruptions and input, output management

- use **Device manager**(administrador de dispositivos)

✔️ how to access device manager

- search/buscar > Administrador de dispositivos

- when you open Administrador de dispositivos, you always get a error message
- bc os hides info from peripherals

✔️ what we can see in device manager

- for every peripheral, show what driver that the peripheral is using
- if there is no exclamation sign it is perfectly working
- however, if there is an excalamation sign, the driver is corrupted
- 💊 you should update the driver

- you can also see the properties of the driver
- brand, model, date of driver, driver of the peripheral...

## ✅

???
Also Win+R>devmgmt.msc
Also Win+R>cmd>driverquery (list of active windows drivers)

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
