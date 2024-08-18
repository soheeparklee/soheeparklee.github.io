---
title: Array/ Array list/ Linked list
categories: [Computer Science, DataStructure]
tags: [] # TAG names should always be lowercase
---

<img width="903" alt="Screenshot 2024-07-24 at 10 46 24" src="https://github.com/user-attachments/assets/2855f0b4-f5ab-4fdc-8a62-9468abc81af8">

## Array 🆚 Array List 🆚 Linked List

#### Array

- 👍🏻 can access directly with index to element
  - time complexity: O(1)
- 👎🏻 need to fix size while creating

#### Array List(Array)

- use dynamic array to store data
- 👍🏻 **dynamic**
- 👍🏻 has list, can access directly
- 👍🏻 fast in searching data
- 👍🏻 insertion, deletion slow

> **Why slow in insertion, deletion?** <br>
>
> > 데이터 추가 및 삭제 때 데이터를 **재할당**한다. <br>
> > thus, insertion and deletion slower than array <br>

#### Linked List(Node)

- use doubly linked list to store data
- 👍🏻 dynamic: do not need to fix size
- 👍🏻 insertion, deletion easy
  - has address that saves the location of previous, next nodes
  - for insertion, deletion, just need to change value of previous, next node
- 👎🏻 cannot access directly, need to search from head

> **Why use array, instead of linked list?** <br>
>
> > fast in search <br>
> > can access element using index <br>

<br>

> **When to use array, when to use linked list?** <br>
>
> > array: search <br>
> > linked list: insertion, deletion <br>

## 💡 Reference

<https://soheeparklee.github.io/posts/JAVA_list/> <br>
<https://soheeparklee.github.io/posts/JAVA_collectionFramework/> <br>
