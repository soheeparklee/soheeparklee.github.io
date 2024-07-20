---
title: Adjacency Matrix, Adjacency List(인접 행렬, 인접 리스트)
categories: [Coding Test, Algorithm]
tags: []
---

## ✔️ Adjacency Matrix, Adjacency List

```java
//input
1 2
1 3
1 4
2 4
3 4
```

```java
0 1 2 3 4
1 0 1 1 1
2 1 0 0 1
3 1 0 0 1
4 1 1 1 0
```

- time complexity low
- matrix caculation possible
- if the graph has node ⬆️ but edge ⬇️, lot of memory loss
- difficult to add, delete node

## ✔️ Adjacency List

```java
//input
1 2
1 3
1 4
2 4
3 4
```

```java
1: [2, 3, 4]
2: [1, 4]
3: [1, 4]
4: [1, 2, 3]
```

- efficient memory usage
- easy to add/delete efge
- time complexity high for checking if two nodes are connected
