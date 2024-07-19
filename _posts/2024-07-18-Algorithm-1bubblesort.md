---
title: Bubble Sort
categories: [Coding Test, Algorithm]
tags: [sort]
---

## ✅ Bubble Sort

1. In the first round, compare first and second/ second and third/ third and fourth element...compare (n-1) and nth element.
2. If it does not match the condition, swap
3. After first round, the biggest element would be at the very back.
4. After one round, number of elements to compare would decrease by 1.

## ⭐️ Keyword

## ✅ Code

<https://soheeparklee.github.io/posts/CT-1-45/>

## ✅ Time complexity

Time complexity would be `(n-1) + (n-2) + (n-3) + ......+ 1n= n(n-1)/2`, thus **O(n^2)**.  
Even in the best, worst scenarios, the time complexity would be the same as **O(n^2)**.

## ✅ Space complexity

sort is done by swapping in the given array.
thus space complexity would be **O(n)**

## 👍🏻 Pros

- simple
- in-place sorting: does not require another array, thus saving memory
- stable sort

## 👎🏻 Cons

- time complexity is always **O(n^2)**, inefficient

## 💡 Reference

<https://gyoogle.dev/blog/algorithm/Bubble%20Sort.html>
