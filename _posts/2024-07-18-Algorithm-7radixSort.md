---
title: Radix Sort
categories: [Coding Test, Algorithm]
tags: []
---

## ✅ Radix Sort

> sorts elements by processing them **digit** by **digit**.

## ⭐️ Keyword

integers, strings with fixed-size keys <br>

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
d: number of digits <br>
n: number of elements <br>
b: number of system being used <br>
<br>
number of digits ⬆️ time complexity ⬆️ <br>

## ✅ Space complexity

**O(n+b)**
n: number of elements <br>
b: base of number system <br>
need to create nuckets for each digit value <br>
cpoy elements back to original array <br>

## 👍🏻 Pros

- could be faster than other comparison based sorting algorithm

## 👎🏻 Cons

- cannot sort element without digit
- not in-place memory

## 💡 Reference

<https://www.geeksforgeeks.org/radix-sort/> <br>
<https://gyoogle.dev/blog/algorithm/Radix%20Sort.html>
