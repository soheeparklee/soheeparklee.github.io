---
title: BitMask
categories: [Coding Test, Algorithm]
tags: []
---

## ✅ BitMask

> modify numbers into binary representaion <br>
> Bit: binary digit, smallest unit for computer <br>

## ✅ Code

✔️ present in array

```java
//array
int[] array1 = [1, 1, 1, 1, 0];
int[] array2 = [1, 1, 0, 1, 0];
int[] array3 = [1, 0, 1, 0, 0];
```

✔️ present in bitmask

```java
//bitmask
{ 0, 1, 2, 3, 4 } => 11111 = 16 + 8 + 4 + 2 + 1 = 31
{ 1, 2, 3, 4 } => 11110
{ 1, 2, 4 } => 10110
{ 2, 4 } => 10100 = 16 + 4 = 20
{ 1 } => 00010
```

✔️ modify binary back to decimal

```java
//into decimal
{ 0, 1, 2, 3, 4 } => 11111
{ 1, 2, 3, 4 } => 11110
{ 1, 2, 4 } => 10110
{ 2, 4 } => 10100
{ 1 } => 00010
```

### ✔️ Caculators

- AND
- OR
- NOT ~
  `~1010 = 0101`
- Shift <<, >>
  `00001010 << 2 = 101000` <br>
  `00001010 >> 2 = 000010`  <br>

  ### ✔️ change 0 to 1

```java
//1010
//change i=2 to 1

1010 | 1 << 2
//1 << 2 = 100
1010 | 0100 => 1110
```

### ✔️ change 1 to 0

```java
1110 & ~1 << 2
// ~1 = 1110
// 1110 << 2 = 1011
1110 & 1011 => 1010
```

## 💡 Reference

<https://mygumi.tistory.com/361> <br>
