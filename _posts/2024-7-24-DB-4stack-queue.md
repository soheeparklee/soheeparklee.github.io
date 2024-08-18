---
title: Stack/ Queue
categories: [Computer Science, DataStructure]
tags: [] # TAG names should always be lowercase
---

## ✅ Stack

> input, output same direction <br>
> LIFO <br>

#### 💡 usage

- DFS
- 문자열 역순
- 연산자 후위표기법

#### 💡 methods

- `push`
- `pop`
- `isEmpty`
- `isFull`: requires MAX_SIZE

## ✅ Queue

> input, output different direction <br>
> front: deQueue <br>
> rear: enQueue <br>
> FIFO <br>

#### 💡 usage

- linked list
- buffer
- BFS

## ⭐️ Can you make a queue with stack?

YES, with `two stacks` I can make a `queue`

1. main stack enque 12345

```
main stack: 12345
```

2. pop main stack, enqueue in substack

```
main stack:
sub stack: 54321
```

3. Deque: pop from substack

```
main stack:
sub stack: 5432

pop: 1
⭐️ like queue FIFO, first number 1 is popped
```

4. Enqueue: pop substack, enqueue in mainstack
   then enqueue new number `6`

```
main stack: 23456
substack:
⭐️ like queue FIFO, 6 is added to the end
```

## 💡 Reference

<https://soheeparklee.github.io/posts/JAVA_stack_queue/> <br>
