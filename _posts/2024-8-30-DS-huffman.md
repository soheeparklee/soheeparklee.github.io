---
title: Huffman coding
categories: [Computer Science, DataStructure]
tags: [] # TAG names should always be lowercase
---

## ✅ Huffman coding

> 문자의 빈도수를 가지고 압축하는 과정 <br>
> assign variable length code to input characters, <br>
> lengths of the assigned codes are bsed on the frequencies of corresponding characters <br>

- 부모 노드를 만들 때 `왼쪽에는 0`, `오른쪽에는 1` 배치

✔️ **접두부 코드**

- 각 문자에 부여된 이진 코드가 다른 이진 코드의 접두부가 되지 않는 코드
- 겹치지 않도록 이진 코드 만들기

✔️ **최적 코드**

- 인코딩 메세지의 길이가 가장 짧은 코드

## ✅ Steps of huffman coding

1. 빈도수 별로 노드 만들어 배치하기 <br>

<img width="368" alt="Screenshot 2024-08-30 at 20 54 47" src="https://github.com/user-attachments/assets/740ff58e-a415-4dc3-b518-af593be5fa16">

2. 가장 작은 빈도수를 가지는 알파벳 `c`, `d`를 합쳐서 부모 노드 만들고, 값은 2 <br>
3. 합쳐진 `c+d` 부모노드 `왼쪽은 0`, `오른쪽 1` <br>
4. 이런식으로 빈도수를 합치면서 부모 노드 만들기 <br>
5. 최종적으로 6을 가진 부모노드와 a가 합쳐져서 11을 가진 노드 생성 <br>
   <br>
6. 결론 <br>
   <img width="265" alt="Screenshot 2024-08-30 at 20 55 09" src="https://github.com/user-attachments/assets/e43b9d26-5429-46de-bbd9-9f2b7de0adaa">
