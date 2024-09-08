---
title: What is Operating System
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ Operating System

> collection of software that manages computer hardware resources and provides common services for computer programs <br> > **communication** channel between system **hardware** and system **software** <br>

- windows 10
- UNIX
- MS-DOX
- LINUX: OS for servers

## ☑️ Purpose of OS

- **thouroughput** ⬆️

  - how much work a system can manage in certain time
  - 일을 얼마나 헀는가

- **turn around time** ⬇️

  - time it takes from request until the job is finished
  - 일하는데 시간 얼마나 걸렸니

- **availability** ⬆️

  - 시스템 사용하려고 할 때 즉시 사용 가능한 정도

- **reliability** ⬆️
  - 시스템이 주어진 문제를 정확하게 해결하는 정도

## ☑️ Functions of OS

**1. Processor Management**

- start, stop, manage process, program
- ⭐️ scheduling
- ⭐️ processing, thread
- ⭐️ synchronization
- ⭐️ IPC communication

<br>

**2. Memory Management**

- ⭐️ manage primary memory
- optimize memory use
- ⭐️ virtual memory
- ⭐️ file system

<br>

**3. Networking**

- establish, manange network connections
- network protocols
- share files, printers over network
- ⭐️ TCP/IP

<br>

**4. User Interface**

- interface for users to interact w the computer
- GUI: Graphical User Interface
- CLI: Command Line Intereface

<br>

**5. Device Driver**

- ⭐️ 순차접근 장치
- ⭐️ 임의접근 장치
- ⭐️ 네트워크 장치

## ☑️ Detailed Explanation of functions

**1. Processor Management**

- **Processor Scheduling**
  - determines which process has access to processor
  - how much processig time each process has
- **Process**
  - keep track of status of process
  - traffic controller
  - allocates CPU to process
  - when process is no longer required, de-allocates

**2. Memory Management**

- for a program to be run, needs to be loaded in the main memory
- OS manages allocation, deallocation of memory

**3. Networking**

- Network communication
  - cops for internet traffic
  - manage how data is packaged and sent over a network
  - check if the data arrived safely and in correct order
- Settings and Monitoring
  - network connections(WIFI)

**4. User Interface**

> user ➡️ OS ➡️ computer interface <br>
> high level language ➡️ interpreter ➡️ machine language <br>

**5. Device Driver**

- manages hardware
- decide which process gets acess to a certain device and for how long, and deallocate

**6. Job Accounting**

- if more than one user is using the OS
- track resource usage of particular user
- determine which application should run in which order, allocation

**7. Virtual Caculator**

## ⭐️ Virtual Caculator

- one computer to function as several computers
