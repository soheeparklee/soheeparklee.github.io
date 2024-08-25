---
title: Array/ Array list/ Linked list
categories: [Computer Science, DataStructure]
tags: [] # TAG names should always be lowercase
---

<img width="903" alt="Screenshot 2024-07-24 at 10 46 24" src="https://github.com/user-attachments/assets/2855f0b4-f5ab-4fdc-8a62-9468abc81af8">

<br>
<br>

## How can we eradicate duplicated value in array?

**1. Set**

- `Set` does not allow duplication
- convert array into `set`

💡 Set <https://soheeparklee.github.io/posts/DS-list_set_map/> <br>

**2. For loop**

- 배열을 돌면서 중복되는 값 삭제

**3. Array.sort**

- 배열을 오름차순/내림차순으로 정렬
- 옆에 있는 값끼리 비교해서 같으면 삭제

**4. Stream API**

- use stream to delete duplicated value
- stream API is added from `JAVA 8`

<br>
<br>

## Array 🆚 Array List 🆚 Linked List

### ✔️ Array

- 👍🏻 can access directly with index to element
  - time complexity: O(1)
- 👎🏻 need to fix size while creating

<br>

### ✔️ Array List(Array)

<img width="587" alt="Screenshot 2024-08-20 at 01 17 55" src="https://github.com/user-attachments/assets/70b98259-5222-498f-a670-142a88eef033">

- use dynamic array to store data
- 👍🏻 **dynamic**
- 👍🏻 has list, can access directly
- 👍🏻 fast in searching data
- insertion, deletion slow

<br>

> **Why slow in insertion, deletion?** <br>
>
> > 데이터 추가 및 삭제 때 데이터를 **재할당**한다. <br>
> > thus, insertion and deletion slower than array <br>

### ✔️ Linked List(Node)

<img width="560" alt="Screenshot 2024-08-20 at 01 19 07" src="https://github.com/user-attachments/assets/8d532bbe-ef59-494f-aeaf-913caec5f4d8">

- use doubly linked list to store data
- 👍🏻 dynamic: do not need to fix size
- 👍🏻 insertion, deletion easy
  - has address that saves the location of previous, next nodes
  - for insertion, deletion, just need to change value of previous, next node
- 👎🏻 cannot access directly, need to search from head

## 📌 Q&A

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
