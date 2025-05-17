---
title: List, ArrayList, LinkedList BigO, DI
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ Array

- 👍🏻 use index and input, change, get value: `O(1)`
  - 배열에는 *index*가 있기 때문에
- 👎🏻 search, insert value: `O(n)`, need to search, compare the whole array,
- 👎🏻 array size is fixed, need to _fix_ array size when creating array

- input value `array[100] = 1;` : **O(1)**
- change value `array[100] = 10;` : **O(1)**
- get value `array[100]` : **O(1)**
- search value `if(array[i] == 10)` : **O(n)**
- insert certain value in the middle of array: **O(n)**, 옆으로 한 칸씩 다 밀어야 함

#### ❓ How does index help get/change value fast?

- in array, only one type of data is possible
  - `int[]`, `String[]`
- each dataset has same size
  - `int has 4 byte`
- so `memory 시작 위치 + index * 4byte`

<img width="509" alt="Image" src="https://github.com/user-attachments/assets/cc6c4395-3f7b-46bd-8758-1b644672685a" />

- `memory 시작 위치`: x100
- `int`: 4byte
- `index[2]의 위치`: x100 + 4byte \* 2

## 💡 BigO

> 알고리즘의 **데이터 크기 변화에 따른 성능 변화 경향**을 알려준다

<img width="511" alt="Image" src="https://github.com/user-attachments/assets/37f063e9-f98e-428a-bf59-1171021147df" />

- O(1): find with one operation, 한번만에 찾음
- O(n): `n` number of data, `n` operations
- O(n2): `n` number of data, much more `n*n` operations
- O(log n): more than `O(1)`, but less than `O(n)`
  - tree
- O(n log n): like ` O(log n)`, but multiplied by `n`

## ✅ List

- flexible size
- duplication allowed
- index

- List 🆚 Array: List has flexible size

## ✅ ArrayList

> use array <br>
> flexible size <br>

- 👍🏻 **flexible size**
  - if more space is needed, create a new arraylist with _more space_ and copy paste the existing old array
    - `default capacity`:10
    - if exceeds `default capacity`, increase capacity by `50%`
    - 기본 크기는 10, 11번째 데이터 추가 ➡️ 크기 15 ➡️ 22 ➡️ 33...
    - then copy old arraylist with `System.arraycopy()`
- 👎🏻 some space of arraylist might not be used ➡️ **waste memory**
  - 하지만 `arraylist`를 내가 필요한 데이터 크기에 딱 맞게 만드는 건 아니므로
  - `arraylist`에 남는 공간이 생길 수 있음
  - 데이터 `11`만 추가하면 `12~15`는 남는 공간
- 👍🏻 get value with **index**, add or delete **last** value is `O(1)`
- 👎🏻 search, add or delete in the **first or middle** of array is `O(n)`
- (옆으로 한 칸씩 다 밀어야 함)

- add/delete data _last_ of array: O(1)
- add/delete data _middle or front_: O(n)
- get value with index: O(1)
- search: O(n)

#### ❓ array 또는 array list에서 데이터 중간 삽입/삭제 연산이 끝 부분 삽입/삭제보다 왜 일반적으로 비효율적일까요?

- 중간에 삽입된/빠진 데이터 외에 나머지를 이동시켜야 해서

## ✅ ArrayList and generic

- use generic in array list to ensure type safety
- in one `array list`, only one type of data

```java
//👎🏻 Before
MyArrayList list = new MyArrayList();
list.add(1);
list.add("hello");
//list: [1, "hello"] //Integer, String이 혼합되어 있음

//👍🏻 After
MyArrayList<Inetger> list = new MyArrayList(); //use generic
list.add(1);
list.add("hello"); //🔴 compile error
//👍🏻 list에는 Integer만 들어갈 수 있게 됨
```

## 💡 Node

> node = value ➕ next node reference address <br>

- node끼리 연결
- 앞 node는 다음 node의 주소를 가지고 있음

- 👍🏻 필요한 크기만큼만 메모리 확보, no memory waste
- 👍🏻 add/delete middle/front data efficiently

<img width="510" alt="Image" src="https://github.com/user-attachments/assets/b1f8ce3e-e6d8-4137-a194-82d6db351b23" />

## ✅ Linked List

> has order, allow duplication <br>
> use node <br>
> reference before, next node <br>
> know first, last node <br>

- 👍🏻 linked list size is size of data, no memory waste
- 👍🏻 add/delete _front, middle, last_: `O(1)`, only has to change surrounding node references(address)
- 👎🏻 search data with specific index, has to search whole linked list ➡️ `O(n)`

## 💡 Dependency Injection

- `OCP`: client code should be **closed**, main code should be **open**
- `Dependency Injection`:
  - postpoone for dependency injection until main code is **RUN time**
  - open to _what specific class_ will be injected: `OCP`
  - client code does not change, postpone so that main code will decide: `OCP`
  - use interface

```java
//✔️ interface MyList
public interface MyList <E>{}

//✔️ MyList is implemented by MyArrayList and MyLinkedList
// ⭐️ depend on interface MyList
public class MyArrayList<E> implements MyList<E>{}

public class MyLinkedList<E> implements MyList<E> {}

//✔️ client code
public class BatchProcessor {
    //use interface, not specific class such as MyArrayList or MyLinkedList
    //DO NOT DEPEND on a specific class
    //POSTPONE
    // ⭐️ depend on interface MyList
    private final MyList<Integer> list;

      public BatchProcessor(MyList<Integer> list) {
        this.list = list;
    }
}

//✔️ main class to be run
main(){
    //decide here, in main code which class to run
    //dependency injection
    BatchProcessor arrayBatchProcessor = new BatchProcessor(new MyArrayList<Integer>());

}
```

- `BatchProcessor(client code)` DOES NOT depend on a specific class
- `BatchProcessor(client code)` depends on interface, `MyList`
- specific class `MyArrayList`, `MyLinkedList` depends on interface, `MyList`
- `main class(class to be run)` decides which specific class will be run
  - specific class: `MyArrayList`, `MyLinkedList`
- **POSTPONE** deciding specific class ➡️ **dependency injection**
- `OCP`: client code does not change, main class is modified
- `polymorphism`: several classes could be injected to main class
- application is loosely coupled, extendable, maintainable

- 메인 클라스가 어떤 구체 클래스를 실행할지 런타임까지 결정을 미룸, 지연
- 클라이언트 클라스는 인터페이스를 사용, 인터페이스에 의존 ➡️ 의존성 주입
- 구체 클래스는 인터페이스를 구현(의존) ➡️ 의존성 주입
- 어떤 클래스를 실행할지 메인클래스에게 알려줘야 함

#### ✔️ compile time dependency

- dependency injection between class
- `BatchProcessor(client code)` depends on `MyList(interface)`
- specific class `MyArrayList`, `MyLinkedList` depends on `MyList(interface)`
  - implements interface

#### ✔️ runtime dependency

- dependency injection between instance

```java
MyLinkedList<Integer> list = new MyLinkedList(); //x002
BatchProcessor processor = new BatchProcessor(list); //reference x002
```

## ✅

## ✅

## ✅

## ✅

## ✅
