---
title: Insertion Sort
categories: [Coding Test, Algorithm]
tags: []
---

## ✅ Insertion Sort

- **Insert** the element in the correct index  
  <br>

1. start from index 2, sort the elements before index
2. if the element is not bigger than `tmp`, insert the element and `break` the `for loop`.

## ⭐️ Keyword

Insert an element in an already sorted array

## ✅ Code

<https://soheeparklee.github.io/posts/CT-1-46/>

## ✅ Time complexity

Worst case scenario(sorted as inverse) **O(n^2)**.  
Best case secnario, compare just once, thus, **O(n)**.

## ✅ Space complexity

sort is done by swapping in the given array.  
thus space complexity would be **O(n)**

## 👍🏻 Pros

- simple
- if the array is sorted, very efficient
- in-place sorting
- stable sort
- reletively faster than bubble, selection sort

## 👎🏻 Cons

- in worst scenario, time complexity inefficient

## 🆚 Selection Sort

- common:
  both sorts after repeating `k` times, the first `Kth` element would be sorted.
- Selection sort: to find `K+1th` element, need to search **all** remaining elements
- Insertion sort: to find `K+1th` element, search only the elements that are `smaller` than `K+1th`
  If encounters element bigger than `K+1th` element, return and insert the element

## 💡 Reference

<https://gyoogle.dev/blog/algorithm/Insertion%20Sort.html>
