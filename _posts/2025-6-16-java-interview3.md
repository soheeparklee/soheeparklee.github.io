---
title: Interview_Collection Framework, Thread
categories: [JAVA, JAVA_Basics]
tags: [] # TAG names should always be lowercase
---

## ✅ JCF란 무엇인가요?

- Java collection framework
- handle data efficiently

## ✅ JCF의 계층 구조를 설명해주세요

[![Screenshot-2025-06-16-at-23-23-54.png](https://i.postimg.cc/bYQHvGMf/Screenshot-2025-06-16-at-23-23-54.png)](https://postimg.cc/qgvCb741)

[![Screenshot-2025-06-16-at-23-24-16.png](https://i.postimg.cc/qMws8P4m/Screenshot-2025-06-16-at-23-24-16.png)](https://postimg.cc/CzZn06ZD)

- `Collection` interface: `List`, `Queue`, `Set`
- `Map`: `Map`

## ✅ Map 인터페이스는 왜 Collection 인터페이스에 상속을 받지 않았나요?

- `Map` has `key + value`
- `List` , `Queue`, `Set` does not

## ✅ List 인터페이스는 무엇이고, 구현체의 종류는 무엇이 있나요?

- has order
- allow duplication
- used for order
- flexible in size

- List 🆚 Array: List is flexible in size

- Arraylist
- LinkedList
- Vector

## ✅ ArrayList에 대해 설명해주세요

List ➕ **Array**

- list that uses array, but **flexible** in size
- default size: 10
- if bigger size `ArrayList` is needed, increase capacity by 50%
- 👎🏻 some space might not be used ➡️ waste memory

## ✅ ArrayList의 시간 복잡도

- get with index: `O(1)`
- add, delete last: `O(1)`
- add, delete middle: `O(n)`, 추가/삭제하고 나머지 다 이동시켜야 함
- search: `O(n)`

## ✅ ArrayList는 어떻게 동적으로 사이즈가 늘어나나요?

- default size: 10
- if bigger size `ArrayList` is needed, increase capacity by 50%
- 👎🏻 some space might not be used ➡️ waste memory

## ✅ LinkedList에 대해 설명해주세요

- List ➕ **Node**
- has data + pointer
- pointer references before, next node
- 👍🏻 does not waste memory

## ✅ LinkedList의 시간 복잡도

- get with index: `O(n)`: node is not linear
- add, delete: `O(1)`, 추가/삭제하고 앞, 뒤만 참조값 바꾸면 끝
- search: `O(n)`

## ✅ 언제 ArrayList를 사용하고, 언제 LinkedList를 사용할까요?

- `ArrayList`: fast for get value with index
- `LinkedList`: add, delete data is important, make perfect size of list, when a lot of change is made to List

## ✅ add를 보면 시간복잡도가 똑같은데 왜 LinkedList가 효율적이나

- `ArrayList` has to change the whole list after adding/deleting
- `LinkedList` only has to change surrounding(before, next) nodes

## ✅ ArrayList와 Vector는 어떠한 차이가 있나요?

- Vector: all methods are synchronized, **multi thread safe**
- ArrayList: not synchronized, **single thread**

## ✅ Stack과 Queue가 무엇인가요?

- `Stack`: LIFO, `push()`, `pop()`
- `Queue`: FIFO, `offer()`, `poll()`
- `Deque`: double end Queue, has all methods of `Stack` and `Queue`
- `Deque` is faster than `Stack`

## ✅ Set이 무엇이고, 구현 클래스가 무엇이 있는지 설명해 주세요.

- no order
- no duplication
- used for search

- HashSet
- LinkedHashSet
- TreeSet

## ✅ Set에서 중복 요소를 어떻게 걸러내는지 설명해 주세요

- if do `equals()`, `hashCode()` is same, then considered as same

- before saving data, compare `hashCode` with `equals()`
- if `hashCode` is the same, does not add to set

- `hashCode()`: get the hashCode of object
- `equals()`: check if hashCode is same or not

## ✅ What is hash?

- use hash function to take an input, and **change** into **fixed-size** value(called `hash code`)
- `hash code` is used to decide **where** in memory the object should be saved

## 💥 What is hash collision?

- when hash code is same
- 💊 create another **new array** inside array

## ✅ What is Hash set?

- no duplication
- no order
- must override `equals()`, `hashCode()`
- 💥 Rehashing: if hash collision occurs frequently ➡️ create bigger array

- add, delete: `O(1)`
- search: `O(1)`
- get all hash set: return in random order

## ✅ What is Linked Hash set?

- `Hash set` ➕ `LinkedList`(order)
- has node, know reference of before, next node
- get all linked hash set: return in **input order**

## ✅ What is Tree set?

- binary tree
- can have order
- add, delete: `O(logN)`
- search: `O(logN)`
- get all: has ascending order, uses `Comparator`

## ✅ Map이 무엇이고, 구현 클래스가 무엇이 있는지 설명해 주세요.

- `key` ➕ `value`
- no order
- key cannot be duplicate
- value can be duplicate

- HashMap
- LinkedHashMap
- TreeMap

## ✅ HashMap은 어떻게 동작하나요?

- use `hash code()` as `key`
- must override `equals()`, `hashCode()`

- add, delete: `O(1)`
- search: `O(1)`
- get all: return in random order

## ✅ HashMap의 최악의 시간 복잡도를 설명해 주세요

- when **Hash Collision** occurs
- HashMap has `hash chaining`
- `hash chaining`: when hashCode is same, new array is created to save data
- when hash collision occurs, has to check all array ➡️ O(n)

```
Key 값은 다르지만 해시 함수에 의해 같은 출력 값을 갖는 현상을 해시 충돌이라고 하는데, HashMap은 이를 해시 체이닝을 통해 해결하고 있습니다. 만일, 한 개의 버킷에 대해 모두 해시 충돌이 발생하면 연결 리스트로 모두 탐색해야함으로 조회 시간 복잡도가 O(N)이 될 수 있습니다.
```

## ✅ Linked Hash Map

- HashMap ➕ LinkedList(order)
- add, delete: `O(1)`
- search: `O(1)`
- get all: input order

## ✅ Tree Map

- HashMap ➕ Tree
- add, delete: `O(logN)`
- search: `O(logN)`
- get all: key ascending order(SortedMap)

## ✅ iterable과 iterator의 차이

- `iterable interface`: collection implements `iterable`
- `for(int i=0; i<n; i++)`
- array: with index
- node: with reference
- tree: with parent, child node

- `iterator`: tool to iterate collection
- hasNext(): 다음 값이 있니?
- next(): 다음으로 간다

## ✅ Collection과 Collections의 차이는 무엇인가요?

- `Collection interface`: highest parent of JCF

- `Collections`: utility class to manipulate classes that implement `Collection interface`
- `max()`
- `shuffle()`
- `sort()`
- `reverse`

## ✅ Java에서 스레드를 만드는 방법을 설명해 주세요.

- 두 가지 방법이 있다
- 1️⃣ with thread class `class MyThread extends Thread`
- 2️⃣ with runnable interface `static class MyRunnable implements Runnable`

## Thread class 🆚 Runnable interface

- thread class: only can extend thread class
- runnable interface: can implement several interfaces

## ✅ 스레드를 생성하여 start 메소드를 호출했는데 왜 run 메소드가 호출되는지 이유

- `start()`: create new thread, and call `run()` method
- `run()`: new thread is not created, but run on thread that is running now

## ✅ 스레드 풀이란 무엇이고, 왜 사용할까요?

- limit the number thread
- prevent repreated thread creation/removal
- provide safe multi threading environment

## ✅ 스프링과 같은 프레임워크에서는 스레드 풀의 스레드 개수를 수백 개 이상으로 운영합니다. 이는 Context Switching이 일어남에도 불구하고도 이런 선택을 내린 것인데, 왜 그럴까요?

- in web applications network calls, database requests are handled in Blocking I/O method
- with many threads, even when one thread is blocked waiting would be minimized
- can respond several client requests at the same time
- make efficient use of CPU

## ✅ Context Switching란?

- CPU can only do one job at once
- context switching to look like it is doing many jobs at the same time

## ✅
