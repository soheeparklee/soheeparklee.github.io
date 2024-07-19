---
title: Selection Sort
categories: [Coding Test, Algorithm]
tags: []
---

## ✅ Selection Sort

- **Select index:** place to put the element is fixed(the front)
- decide which element to put(the smallest)
- first find the minimum element and place the minimum element at the beginning
  <br>

1. find the smallest from the array
2. Pass the smallest element to the front index
3. The front part of the array would be sorted.

## ⭐️ Keyword

## ✅ Code

<https://soheeparklee.github.io/posts/CT-1-44/>

## ✅ Time complexity

First round 1 ~ (n-1) ➡️ n-1
Second round 2 ~ (n-1) ➡️ n-2
...
Thus, `(n-1) + (n-2) + (n-3) + ......+ 1n= n(n-1)/2`, conclusion: **O(n^2)**.

## ✅ Space complexity

sort within the given array, thus **O(n)**

## 👍🏻 Pros

- simple algorithm
- less swap than bubble sort
- in-place sorting: does not require more than the given array

## 👎🏻 Cons

- time complexity inefficient
- unstable sort

## 💡 Reference
