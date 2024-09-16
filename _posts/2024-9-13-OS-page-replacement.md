---
title: Page Replacement Algorithm
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ Page Replacement Algorithm

- in OS that uses paging for memory management
- which page should be replaced when a new page comes in
- used 1️⃣ when page fault occurs and 2️⃣ there is no free page in memory

💡 Paging <https://soheeparklee.github.io/posts/OS-12paging/>

✔️ **Page Replacement Algorithm**

- FIFO
- Optimal Page Replacement
- Least Recently Used
- Most Recently Used

## ✅ **Page fault**

- program accesses memory page
- memory page that is mapped into virtual address space
- but not loaded on physical memory

💡 Virtual Memory <https://soheeparklee.github.io/posts/OS-virtualmemory/>

- if page fault occurs,
- OS need to replace page with newly added page

## ☑️ FIFO

> First in first out

- oldest(first) in memory to SWAP
- keep track of pages in memory in queue

<img width="383" alt="Screenshot 2024-09-13 at 23 42 01" src="https://github.com/user-attachments/assets/7c078850-ee78-4b4f-a64a-81056c9cffc7">

## ☑️ Optimal Place Replacement

- which page would not be used for the longest duration in the future?
- check future access pattern
- select page based on pattern
- and send to SWAP
- 👎🏻 not possible in practice as OS cannot know future requests

## ☑️ LRU

> Least Recently Used

- page with most time that is not used

## ☑️ MRU

> Most Recently Used

- page that has been used recently

## ☑️ LFU

> Least Frequently Used

- least use frequency

## ☑️ NUR

> Not Recently Used page replacement

- page that has not been referenced in atleast one clock tick
