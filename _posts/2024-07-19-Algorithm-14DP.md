---
title: Dynamic Programming
categories: [Coding Test, Algorithm]
tags: []
---

## ✅ Dynamic Programming

> solve problem by breaking down into simple **subproblems** <br>
> solve subproblem once, store the result, avoid redundand computation <br>
> find a subproblem with **repeated caculation** <br>

1. Top-Down Dynamic Programming
   - memoization
   - recursive
2. Bottom-Up Programming
   - start with solving subproblems, build up solutions to solve large problems.

#### 🆚 Divide and Conquer

- simmilar in the sence that we divide a problem to solve

- but different
  - Divide and Conquer: divide problem into smaller problem
  - DP: find a **repeated caculation(반복되는 연산)** to solve

## ✅ Conditions for DP

**1. Overlapping subproblem**

- require repeated caculation

**2. Optimal Substructure 최적 부분구조**

- can retrieve answer for new sub problem from another subproblem
- 새로운 부분 문제의 정답을 다른 부분 문제의 정답으로부터 구할 수 있다.

## ⭐️ Memoization

> store(memoize) results to avoid recomputation <br>
> 한 번 계산한 문제는 다시 계산하지 않도록 저장 <br>

## 👍🏻 Pros

- memoization
- avoid recomputing
- break down into smaller problems

## ✅ Usage

- Shortest path in graph
- fibonacci
  <https://soheeparklee.github.io/posts/CT-1-57/>

## 💡 Reference

<https://www.geeksforgeeks.org/dynamic-programming/> <br>
<https://gyoogle.dev/blog/algorithm/Dynamic%20Programming.html> <br>
