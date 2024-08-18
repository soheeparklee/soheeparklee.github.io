---
title: Binary Search Tree/ Comparison of heap, tree, BST
categories: [Computer Science, DataStructure]
tags: [] # TAG names should always be lowercase
---

## ✅ Binary Search Tree

> binary search ➕ linked list <br>
> 👍🏻 searching data

- binary search:

  - search time complexity: O(longN) 👍🏻
  - insertion, deletion time complexity: impossible 👎🏻
    <br>

- linked list:

  - search time complexity: O(N) 👎🏻
  - insertion, deletion time complexity: O(1) 👍🏻

## ☑️ Binary Search Tree characteristics

- max **two** child nodes
  - left: smaller than node's key
  - right: bigger than node's key
- duplication of node not possible, all node unique
- search by `in order` method(중위순회 왼-루트-오)

## ☑️ Search in Binary Search Tree

- start in root node
- compare key value with searching value
- if `searching value < key`: search `left`
- if `searching value > key`: search `right`

## ☑️ Insertion in Binary Search Tree

- same as search
- if fail in search, insertion in failed place
- time complexity: O(N)

## ☑️ Deletion in Binary Search Tree

- if deleting end node: delete connection with parent node
- if deleting node with one subnode: add the subnode to parent node, and delete node
- if deleting node with two subnodes: find the most similar node and add the two subnodes, and delete node

## 🆚 Comparison of heap, tree, binary search tree

<img width="1115" alt="Screenshot 2024-07-24 at 11 51 38" src="https://github.com/user-attachments/assets/b98ae8f4-f1e1-47c8-939e-8573afbf2bd6">

- heap
  - kind of tree
  - types: max heap, min heap
  - **ordered**
  - priority queue
- tree
  - types: binary tree, BST, AVL...
  - **not ordered**
- Binary Search Tree
  - **ordered**
