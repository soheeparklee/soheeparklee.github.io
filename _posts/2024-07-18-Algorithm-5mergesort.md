---
title: Merge Sort
categories: [Coding Test, Algorithm]
tags: []
---

## ✅ Merge Sort

> Divide and Conquer

1. Divide: divide the array into two sub arrays <br>
2. Conquer: each subarray sorted<br>
3. Merge: merge back together<br>
   when merging, since two sub arrays are sorted,<br>
   can merge comparing the two subarrays one by one<br>

![Screenshot 2024-07-18 at 22 22 49](https://github.com/user-attachments/assets/354c5dee-87c0-4045-ba86-f900fd321d1e)

## ⭐️ Keyword

Sorting **Linked List** <br>

## ✅ Code

```java
private void solve() {
    int[] array = { 230, 10, 60, 550, 40, 220, 20 };

    mergeSort(array, 0, array.length - 1);

    for (int v : array) {
        System.out.println(v);
    }
}

public static void mergeSort(int[] array, int left, int right) {
    if (left < right) {
        int mid = (left + right) / 2;

        mergeSort(array, left, mid);
        mergeSort(array, mid + 1, right);
        merge(array, left, mid, right);
    }
}

public static void merge(int[] array, int left, int mid, int right) {
    int[] L = Arrays.copyOfRange(array, left, mid + 1);
    int[] R = Arrays.copyOfRange(array, mid + 1, right + 1);

    int i = 0, j = 0, k = left;
    int ll = L.length, rl = R.length;

    while (i < ll && j < rl) {
        if (L[i] <= R[j]) {
            array[k] = L[i++];
        } else {
            array[k] = R[j++];
        }
        k++;
    }

    while (i < ll) {
        array[k++] = L[i++];
    }

    while (j < rl) {
        array[k++] = R[j++];
    }
}
```

## ✅ Time complexity

each of `log*n*` levels, merging step takes `O(n)` time. <br>
thus, the total time `T(n) = O(n) * log*n*` <br>

### ✔️ Best scenario

Big omega **Ω(nlogn)**

### ✔️ Worst scenario

Big O notation **O(nlogn)**

### ✔️ Average

Theta **Θ(nlogn)**

## ✅ Space complexity

**O(n)**, additional space required for temporarily storing data while **merging**

## 👍🏻 Pros

- stable sort
- guaranteed worst case performance

## 👎🏻 Cons

- space complexity high
- not in-place algorithm
  - requires additional memory while **merging**

## 🆚 Quick sort

QuickSort: pivot ➡️ partition ➡️ divide<br>
MergeSort: divide and sort as much as possible ➡️ merge<br>

## 💡 Reference

<https://gyoogle.dev/blog/algorithm/Merge%20Sort.html>
