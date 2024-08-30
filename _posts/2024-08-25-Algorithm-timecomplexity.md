---
title: Time Complexity/ Space Complexity
categories: [Coding Test, Algorithm]
tags: []
---

## ✅ Time Complexity

> time taken by an algorithm <br>
> to run as a `function` of the `length of the input` <br>
> 시간복잡도: `입력 크기 n`에 대해 `걸린 시간`을 `함수T(n)`로 표현 <br>

- 상수는 1로 취급
- `가장 영향력이 큰 값(dominant)`만을 나타낸다.
- Example: `T(n) = 2n^2 + n + `1일 경우, `O(n^2)`

- Big-O: 최악의 경우
- Big-Ω: 최선의 경우
- Big-θ: 최악, 최선의 평균

<img width="628" alt="Screenshot 2024-08-26 at 00 08 24" src="https://github.com/user-attachments/assets/6bb6b3d2-c334-462f-b035-3901e3e3e9f8">

복잡도 순서:
O(1) < O(log N) < O(N) < O(N log N) < O(N^2) <
O(2^N) < O(N!) <br>

✔️ **O(1)**

- 상수
- 실행 시간은 입력 크기와 관계없이 일정
- search in hash table

✔️ **O(N)**

- 선형
- 실행시간과 입력 크기가 비례
- 입력 크기 ⬆️ 실행 시간 ⬆️
- compare all elements in list to a certain value

✔️ **O(N^2)**

- 실행 시간은 입력 크기의 제곱 함수
- for in for loop
- check two different lists for matching value

✔️ **O(2^N)**

- 실행 시간은 입력 크기에 따라 기하급수적으로 증가
- 👎🏻 매우 비효율적
- three-coloring problem

✔️ **O(log N)**

- 입력 크기가 크게 증가해도 실행 시간은 선형적으로 증가
- [입력 크기 1000개, 실행 시간 1초], [입력 크기 100000개, 실행 시간 2초], [입력 크기 10000000개, 실행 시간 3초]...
- binary search

## 🆚 Time complexity of sorting algorithms

- Big-O 기준으로

<img width="441" alt="Screenshot 2024-08-30 at 20 58 01" src="https://github.com/user-attachments/assets/fbed33a9-4d90-4bab-84c4-70ff94bff056">

- quick sort is the fastest

## ✅ Space Complexity
