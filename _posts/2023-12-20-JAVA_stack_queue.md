---
title: Collection Framework_List(Stack, Queue)
categories: [JAVA, JAVA_Basics]
tags: [list, framework, collection, stack, queue] # TAG names should always be lowercase
---

![코딩공책-41](https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/a02c6601-f733-4f36-ace9-c358b44c38ac)

<img width="609" alt="Screenshot 2024-05-14 at 11 49 23" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/43c89fb7-ce91-4f16-b3fb-84c372b0169e">

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
        queue.contains() //true, false

        //💡 isEmpty
        queue.isEmpty(); //false

        //💡 clear, 모두 삭제
        queue.clear()
    }
}

```

## ✅ Priority Queue

> 저장한 순서에 상관 없이 우선순위(Priority)가 높은 순서대로 꺼낸다.
> heap: Priority Queue에 저장된 각 요소
> 힙은 가장 큰 값이나 가장 작은 값을 빠르게 찾을 수 있다.

```java
        Queue<Integer> queue= new LinkedList<>();

        Queue<Integer> priorityQueue= new PriorityQueue<>();
        priorityQueue.offer(3);
        priorityQueue.offer(1);
        priorityQueue.offer(5);
        priorityQueue.offer(2);
        priorityQueue.offer(4);

        System.out.println(priorityQueue); // [1,2,5,3,4]

        while(priorityQueue.poll() != null){
            System.out.println(priorityQueue.poll());
        }
```

![코딩공책-43](https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/f9ccf519-4448-40cd-8955-f39b39748817)

## ✅ Deque(Double End Queue)

> 양쪽 끝에 추가, 삭제 가능
> stack과 queue를 하나로 합쳐놓은 것과 같음
> 조상: queue
> 구현체: ArrayDeque, LinkedList
