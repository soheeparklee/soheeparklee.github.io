---
title: Parity Bits, Hamming Code
categories: [Computer Science, Computer Architecture]
tags: [] # TAG names should always be lowercase
---

## ✅ Parity Bits(redundant bits)

> extra binary bits added to data transfer to ensure that no bits were lost during transfer

```T
2^r ≥ m + r + 1
// r: number of redundant bits
// m: number of bits in input data
```

### ✔️ Types of Parity Bits

1. Even Parity Bit

- number of 1's are counted
- if the count is odd ➡️ parity bit value: 1
- if the count is even ➡️ parity bit value: 0

2. Odd Parity Bit

- number of 1's are counted
- if the count is odd ➡️ parity bit value: 0
- if the count is even ➡️ parity bit value: 1

## ✅ Hamming Code

> error-detecting code to ensure data accuracy during transmission/storage

- error detection and correction

How does hamming code work?
<https://www.geeksforgeeks.org/hamming-code-in-computer-network/?ref=header_search>
