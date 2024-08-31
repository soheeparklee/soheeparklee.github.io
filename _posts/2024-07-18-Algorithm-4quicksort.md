---
title: Quick Sort
categories: [Coding Test, Algorithm]
tags: []
---

## ✅ Quick Sort

> divide and conquer 분할 정복 <br>
> ⭐️ pivot <br>

1. Choose a Pivot: <br>
   select pivot element from array <br>
2. Divide(Partitioning): <br>
   divide the array into two sub arrays <br>
   - front of pivot: smaller than pivot<br>
   - behind pivot: bigger than pivot <br>
3. Recursion for two divided subarrays<br>
   repeat step 1, 2 until sub array has zero or one element<br>

![코딩공책-87](https://github.com/user-attachments/assets/2325d0c5-2465-4e93-97e7-c046112371c6)

## ⭐️ Keyword

- pivot

## ✅ Code

### ✔️ Conquer

```java
public void quickSort(int[] arr, int left, int right) {
    if(left >= right) return;

    // divide
    int pivot = partition(arr, left, right);

    // recursion for two sub arrays
    // pivot is not included
    quickSort(arr, left, pivot-1);  // Conquer left(smaller than pivot)
    quickSort(arr, pivot+1, right); // Conquer right)bigger than pivot)
}
```

### ✔️ Divide

Divide the array into two subarrays  
based on **pivot**  
<br>

- left: smaller than pivot
- right: bigger than pivot

```java
public int partition(int[] arr, int left, int right){
    int pivot= array[left]; //choose the leftmost element as pivot

    int i = left-1;

        // Traverse through all elements, compare each with the pivot
        for (int j = left; j < right; j++) {
            if (arr[j] < pivot) {
                // If element smaller than pivot is found, swap it with the greater element pointed by i
                i++;

                // Swap element at i with element at j
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }

        // Swap the pivot element with the greater element specified by i
        int temp = arr[i + 1];
        arr[i + 1] = arr[right];
        arr[right] = temp;

        // Return the position from where partition is done
        return i + 1;
}
```

## ✅ Time complexity

### ✔️ Best scenario, **O(log₂n)**

if `n=2^k`, **k(k=log₂n)**  
<br>

`T(n)=2T(n/2)+O(n)` <br>
O(n): partitioning process. <br>
caculation for each recursion = n <br>
thus, `depth of recursion * caculation for each recursion`= `nlog₂n` <br>

### ✔️ Worst scenario, **O(n^2)**

Worst scenario: when the array is ascending, descending sorted <br>
and the pivot is smallest or largest element repeatedly <br>
if `n=2^k`, recursion for `n` times <br>
thus, `depth of recursion * caculation for each recursion`= `n^2` <br>

### ✔️ average **O(log₂n)**

## ✅ Space complexity

sort is done by swapping in the given array.  
thus space complexity would be **O(n)**

## 👍🏻 Pros

- one of the fastest algorithms
- in-place sorting

## 👎🏻 Cons

- unstable sort
- if the array is sorted, might take longer because of unbalanced dividing

## 💡 Reference
