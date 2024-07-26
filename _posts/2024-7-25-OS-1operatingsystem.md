---
title: What is Operating System
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ Operating System

> collection of software that manages computer hardware resources and provides common services for computer programs <br>
> communication channel between system hardware and system software <br>

## ☑️ Functions of OS

1. Processor Management
   - start, stop, manage process, program
   - ⭐️ scheduling
   - ⭐️ processing, thread
   - ⭐️ synchronization
   - ⭐️ IPC communication
2. Memory Management
   - ⭐️ manage primary memory
   - optimize memory use
   - ⭐️ virtual memory
   - ⭐️ file system
3. Networking
   - establish, manange network connections
   - network protocols
   - share files, printers over network
   - ⭐️ TCP/IP
4. User Interface
   - interface for users to interact w the computer
   - GUI: Graphical User Interface
   - CLI: Command Line Intereface
5. Device Driver
   - ⭐️ 순차접근 장치
   - ⭐️ 임의접근 장치
   - ⭐️ 네트워크 장치

## ☑️ Detailed Explanation of functions

1. Processor Management

- Processor Scheduling
  - determines which process has access to processor
  - how much processig time each process has
- Process
  - keep track of status of process
  - traffic controller
  - allocates CPU to process
  - when process is no longer required, de-allocates

2. Memory Management

- for a program to be run, needs to be loaded in the main memory
- OS manages allocation, deallocation of memory

3. Networking

- Network communication
  - cops for internet traffic
  - manage how data is packaged and sent over a network
  - check if the data arrived safely and in correct order
- Settings and Monitoring
  - network connections(WIFI)

4. User Interface

   > user ➡️ OS ➡️ computer interface
   > high level language ➡️ interpreter ➡️ machine language

5. Device Driver

- manages hardware
- decide which process gets acess to a certain device and for how long, and deallocate

6. Job Accounting

- if more than one user is using the OS
- track resource usage of particular user
- determine which application should run in which order, allocation

## 💡 Reference

<https://www.geeksforgeeks.org/functions-of-operating-system/>
