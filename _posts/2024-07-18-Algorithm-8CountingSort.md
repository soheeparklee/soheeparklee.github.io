---
title: Counting Sort
categories: [Coding Test, Algorithm]
tags: []
---

## ✅ Counting Sort

> non-comparison-based sorting algorithm
> counting: how many times does this element appear in input array?

1. input array <br>
   get the biggest number `max` <br>
2. count array <br>
   size: `max +1` <br>
3. output array <br>
   <br>

4. get input array <br>
5. get the biggest number `max` <br>
6. make count array with size of `max +1` <br>
7. in count array, store count of unique element of input array at their respective indices <br>
   if 0 appears 2 times, input `2` at index `0`. <br>
8. store cumulative sum in count array <br>
9. Update output array `outputArray[ countArray[ inputArray[i] ] – 1] = inputArray[i]` <br>
10. also Update count array `countArray[ inputArray[i] ] = countArray[ inputArray[i] ]– -` <br>

## ⭐️ Keyword

![코딩공책-90](https://github.com/user-attachments/assets/7f2fd1d6-30bf-41fd-a21b-f1f4880a2925)

## ✅ Code

## ✅ Time complexity

**O(n+k)** <br>
n: size of input array <br>
k: size of count array(range of input value) <br>

## ✅ Space complexity

**O(n+k)** <br>
n: size of output array <br>
k: size of count array <br>

## 👍🏻 Pros

- stable algorithm
- if range of input is of the order of number of input, faster
  (when k is smaller, faster)

## 👎🏻 Cons

- does not work for decimal value
- not in-place sorting algorithm

## 💡 Reference

<https://www.geeksforgeeks.org/counting-sort/?ref=shm>
