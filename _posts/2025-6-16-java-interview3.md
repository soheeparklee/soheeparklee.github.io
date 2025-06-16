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

## ✅ ArrayList에 대해 설명해주세요

List ➕ **Array**

- list that uses array, but flexible in size
- default size: 10
- if bigger size `ArrayList` is needed, increase capacity by 50%
- 👎🏻 some space might not be used ➡️ waste memory

## ✅ ArrayList의 시간 복잡도

- get with index: `O(1)`
- add, delete: `O(n)`, 추가/삭제하고 나머지 다 이동시켜야 함
- search: `O(n)`

## ✅ ArrayList는 어떻게 동적으로 사이즈가 늘어나나요?

- if bigger size `ArrayList` is needed, increase capacity by 50%
- 👎🏻 some space might not be used ➡️ waste memory

## ✅ LinkedList에 대해 설명해주세요

- List ➕ **Node**
- reference before, next node
- 👍🏻 does not waste memory

## ✅ LinkedList의 시간 복잡도

- get with index: `O(n)`
- add, delete: `O(1)`, 추가/삭제하고 앞, 뒤만 참조값 바꾸면 끝
- search: `O(n)`

## ✅ 언제 ArrayList를 사용하고, 언제 LinkedList를 사용할까요?

- `ArrayList`: get value with index
- `LinkedList`: add, delete data is important, make perfect size of list

## ✅ add를 보면 시간복잡도가 똑같은데 왜 LinkedList가 효율적이나

- `ArrayList` has to change the whole list after adding/deleting
- `LinkedList` only has to change surrounding(before, next) nodes

## ✅ ArrayList와 Vector는 어떠한 차이가 있나요?

-

## ✅ Stack과 Queue가 무엇인가요?

- `Stack`: LIFO, push(), pop()
- `Queue`: FIFO,
- `Deque`: has all methods of `Stack` and `Queue`

## ✅ Set이 무엇이고, 구현 클래스가 무엇이 있는지 설명해 주세요.

- no order
- no duplication
- used for search

- HashSet
- LinkedHashSet
- TreeSet

## ✅ Set에서 중복 요소를 어떻게 걸러내는지 설명해 주세요

- if do `equals()`, `hashCode()` is same, then considered as same

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
- get all linked hash set: return in input order

## ✅ What is Tree set?

- binary tree
- can have order
- add, delete: `O(logN)`
- search: `O(logN)`

## ✅ Map이 무엇이고, 구현 클래스가 무엇이 있는지 설명해 주세요.

## ✅ HashMap은 어떻게 동작하나요?

## ✅ HashMap의 최악의 시간 복잡도를 설명해 주세요

## ✅ iterable과 iterator의 차이

## ✅ Collection과 Collections의 차이는 무엇인가요?

-

## ✅ Java에서 스레드를 만드는 방법을 설명해 주세요.

## ✅ Thread 클래스와 Runnable 인터페이스의 차이

## ✅ 스레드를 생성하여 start 메소드를 호출했는데 왜 run 메소드가 호출되는지 이유

## ✅ 스레드 풀이란 무엇이고, 왜 사용할까요?

## ✅ 스프링과 같은 프레임워크에서는 스레드 풀의 스레드 개수를 수백 개 이상으로 운영합니다. 이는 Context Switching이 일어남에도 불구하고도 이런 선택을 내린 것인데, 왜 그럴까요?

## ✅ Context Switching란?

## ✅
