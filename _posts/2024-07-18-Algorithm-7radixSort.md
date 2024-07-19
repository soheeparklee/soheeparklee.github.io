---
title: Radix Sort
categories: [Coding Test, Algorithm]
tags: []
---

## ✅ Radix Sort

> sorts elements by processing them **digit** by **digit**.

## ⭐️ Keyword

integers, strings with fixed-size keys

## ⭐️ MSD, LSD

**MSD**

> Most Significant Digit
> counting from biggest digit

<br>

**LSD**

> Least Significant Digit
> counting from smallest digit
> branch free algorithm

## ✅ Code

![코딩공책-89](https://github.com/user-attachments/assets/e982c72b-fdf9-468a-a0a8-29b6b569ae2f)

## ✅ Time complexity

**O(d\*(n+b))**
d: number of digits
n: number of elements
b: number of system being used

number of digits ⬆️ time complexity ⬆️

## ✅ Space complexity

O(n+b)
n: number of elements
b: base of number system
need to create nuckets for each digit value
cpoy elements back to original array

## 👍🏻 Pros

- could be faster than other comparison based sorting algorithm

## 👎🏻 Cons

- cannot sort element without digit
- not in-place memory

## 💡 Reference

<https://www.geeksforgeeks.org/radix-sort/>
<https://gyoogle.dev/blog/algorithm/Radix%20Sort.html>
