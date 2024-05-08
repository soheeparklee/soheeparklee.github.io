---
title: Collection Framework_List(Stack, Queue)
categories: [JAVA, JAVA_Basics]
tags: [list, framework, collection, stack, queue] # TAG names should always be lowercase
---

## ✅ Stack: LIFO

> LIFO: Last In First Out
> added and removed from the top of the stack
> the last to be added will the the first to be removed

```java

import java.util.Stack;

public class StackExample {
    public static void main(String[] args) {
        Stack<Integer> stack = new Stack<>();

        //💡 push(add)
        stack.push(10);
        stack.push(20);
        stack.push(30);

        //💡 pop
        //remove and return the element at the top of the stack
        stack.pop(); // 30

        //💡 peek
        //return the element at the top of the stack wo removing
        stack.peek(); //20

        //💡 isEmpty
        stack.isEmpty(); // false
    }
}
```

## ✅ Queue: FIFO

> FIFO: First In First Out
> added at the last of the stack, removed from the first of the stack
> 그래프의 넓이 우선 탐색(BFS)에서 사용
> contains를 통해 어떤 값이 포함되어있는지, 없는지의 유무는 알 수 있지만, index이 개념은 없어서 몇 번째 값이 무엇인지 알 수 는 없다.

💡 Example of Queue interface: <br>

- Linked List <br>
- ArrayDeque <br>
- PriorityQueue <br>

```java
import java.util.LinkedList;
import java.util.Queue;

public class QueueExample {
    public static void main(String[] args) {
        Queue<String> queue = new LinkedList<>();

        //💡 offer(add)
        queue.offer("A");
        queue.offer("B");
        queue.offer("C");

        //💡 poll
        // remove and return the first element
        queue.poll(); //A

        //💡 peek
        //return the first element wo removing
        queue.peek(); // B

        //💡 contains
        queue.contains()

        //💡 isEmpty
        queue.isEmpty(); //false

        //💡 clear, 모두 삭제
        queue.clear()
    }
}

```
