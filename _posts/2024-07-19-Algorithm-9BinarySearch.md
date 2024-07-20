---
title: Binary Search
categories: [Coding Test, Algorithm]
tags: []
---

## ✅ Binary Search

> **search algorithm** <br>
> used on sorted array <br>
> repeatedly divide search interval into two parts(binary) and search <br>

1. **Sort** <br>
2. set left, right, mid <br>
3. While left < right <br>
4. Compare mid and serach value <br>
5. If mid == search value, search terminates <br>
   - If mid < search value, search right <br>
   - If mid > search value, search left <br>

## ⭐️ Keyword

## ✅ Code

<https://soheeparklee.github.io/posts/CT-1-51/>

## ✅ Time complexity

**O(log N)**
search interval is halved in each step

## ✅ Space complexity

**O(1)**

## 👍🏻 Pros

- do not have to search all the array, just search half

## 👎🏻 Cons

- array has to be sorted

## 💡 Reference
