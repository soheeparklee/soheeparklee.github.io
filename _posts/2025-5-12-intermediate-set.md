---
title: Set, Hash, HashSet, LinkedHashSet, TreeSet
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## List 🆚 Set

- List: duplication⭕️, index⭕️, used for `order`
- Set: duplication❌, no index ❌, used for `search`

## ✅ Set

- uniqueness, no duplication
- no order, no index
- fast search

## ✅ Hash

- 👍🏻 search, get value: `O(1)`, if hash collision `O(n)`
- use `hash index`
- save data: `O(1)`, if hash collision `O(n)`
- use `division`
- use remainder as `hash index`

```java
Integer[] intArray = new Integer[10]; //array size: 10

//14 -> 14%10 -> hash index: 4
intArray[4] = 14;
//99 -> 99%10 -> hash index: 9
intArray[9] = 99;
```

- hash index will always be smaller than array size

## 💥 Hash collision

- 💥 `division remainder(hash index)` can be same
- if hash collision occurs, `hash index` will be the same

```java
9 % 10 -> hash index 9
99 % 10 -> hash index 9
// what should we have in array index 9? both [9, 99] in new array
```

<img width="460" alt="Image" src="https://private-user-images.githubusercontent.com/97790983/442839673-5963de41-66dc-4e00-bcb0-b3c520a441d4.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDc4NjA5NjUsIm5iZiI6MTc0Nzg2MDY2NSwicGF0aCI6Ii85Nzc5MDk4My80NDI4Mzk2NzMtNTk2M2RlNDEtNjZkYy00ZTAwLWJjYjAtYjNjNTIwYTQ0MWQ0LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA1MjElMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwNTIxVDIwNTEwNVomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTMxZDUwNDRmNGQzMWJmNzc0MTlhNDY1NGFlZjk0MmUyMzQ2Yzc4YTZjODJkMjE3MzYyODA2NGI4ZTNmODk2ZjgmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.0v-wiF41RJ6LNMvus1nG7RnQy0JZC_eisEMBhn9swrM" />

- 💊 create **another** `new array` inside array
- save both `[9, 99]` in `hash index 9`
- to search `hash index 9`, go to `index 9`, and search `new array`

## ✅ Hash Code Function

- function that can change `value` into certain length `hash code`
- same `value` should always return same `hash code`

```java
//hashCode function that change string into int
hashCode("A") = 65
hashCode("B") = 66
hashCode("AB") = 131
```

- by using `hash code function`, we can save any type of data on hashSet

```java
MyHashSetV2 set = new MyHashSetV2(10);
Member memberA = new Member("idA");
set.add(memberA); //save Member on hashSet

idA.hashCode(); //can get hashCode of memberA
```

- need to override `hashCode()` and `equals()`
- `hashCode()`: to create `hash index`
- `equals()`: to get, search data with `equals()`
- 👍🏻 a good `hash function` is widely distributed, 💥 less hash collision

## ☑️ HashSet

- no duplication
- no order
- add data: `O(1)`
- search data: `O(1)`
- get all hashSet: in random order(save with `hash index`)
- must override `hashCode()` and `equals()` to use hash index
- **Rehashing**: 💥 if a lot of hash collision occurs, create bigger(\*2) `new array` ➡️ copy old `array`

## ☑️ LinkedHashSet

- `HashSet` ➕ `LinkedList`(order)
- value ➕ `node`
- use `node` to connect, know front and after `node` of myself
- get all linkedHashSet: in input order(linked with `node`)

## ☑️ TreeSet

- binary tree
- can have order(input `3, 1, 2` ➡️ ordered in `1, 2, 3`)
- add, search data: `O(logN)`

- `parent node` ➕ `child node`
- binary tree: can have two `child node`
- binary search tree: `left child node` is smaller than `right child node`
- when add data, **order** and save the data
- search: if value is smaller than node ➡️ go left, if bigger ➡️ go right, `O(logN)`
  - 검색할 때 한번에 절반을 날려버릴 수 있다
- get all tree: in ascending order(small➡️big), 중위순회(`left node` ➡️ `myself` ➡️ `right node`)

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅
