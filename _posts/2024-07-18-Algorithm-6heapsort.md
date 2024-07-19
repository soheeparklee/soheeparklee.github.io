---
title: Heap Sort
categories: [Coding Test, Algorithm]
tags: []
---

## ✅ Heap Sort

> Complete Binary Tree <br>
> binary tree that adds from left<br>

1. Build complete binary tree from array <br>
2. Convert array into heap data structure using heapify <br>
   - transfrom heap into max heap <br>
   - max heap: parent node always be greater than or equal to child node <br>
3. Swap root element of heap(biggest) with the last element of heap <br>
4. Remove last element of Heap <br>
5. Heapify again <br>
6. Recusrive <br>
7. Sorted array is reverse(up side down) <br>

## ⭐️ Keyword

max heap, eliminate highest element

## ✅ Code

![코딩공책-88](https://github.com/user-attachments/assets/5d9a0ee9-bce7-414b-a10f-9b008b0f7df6)

```java
private void solve() {
    int[] array = { 230, 10, 60, 550, 40, 220, 20 };

    heapSort(array);

    for (int v : array) {
        System.out.println(v);
    }
}

public static void heapify(int array[], int n, int i) {
    int p = i;
    int l = i * 2 + 1;
    int r = i * 2 + 2;
    //left node
    if (l < n && array[p] < array[l]) {
        p = l;
    }
    //right node
    if (r < n && array[p] < array[r]) {
        p = r;
    }

    if (i != p) {
        swap(array, p, i);
        heapify(array, n, p);
    }
}

public static void heapSort(int[] array) {
    int n = array.length;

    // init, max heap
    for (int i = n / 2 - 1; i >= 0; i--) { //based on parent node, left node, right node
        heapify(array, n, i); //array to heap
    }

    // for extract max element from heap
    for (int i = n - 1; i > 0; i--) {
        swap(array, 0, i);
        heapify(array, i, 0); //max heap again after removing biggest element
    }
}

public static void swap(int[] array, int a, int b) {
    int temp = array[a];
    array[a] = array[b];
    array[b] = temp;
}
```

## ✅ Time complexity

O(N log N)

## ✅ Space complexity

O(log n) due to recursice call stack

## 👍🏻 Pros

- in-place algorithm

## 👎🏻 Cons

- unstable sort

## 💡 Reference

<https://www.geeksforgeeks.org/heap-sort/>  
<https://gyoogle.dev/blog/algorithm/Heap%20Sort.html>
