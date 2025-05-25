---
title: Iterable, Comparable, Collection
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ Iterable, Iterator

- 처음부터 끝까지 **순회**하기
- `array`: iterate with index
- `node`: iterate with node reference(before and after node)
- `tree`: iterate with parent node, child node
- ➡️ Java provides iterator for all data architecture type

## ✅ Java Iterator

- `hasNext()`: 다음 값이 있니?
- `next()`: 다음으로 간다

```java
 ArrayList<Integer> arrayList = new ArrayList<>();
arrayList.add(1);
arrayList.add(2);
arrayList.add(3);

Iterator<Integer> iterator = arrayList.iterator(); //get iterator
while(iterator.hasNext()){ //hasNext(): 다음이 있어?
    Integer next = iterator.next(); //next(): 있으면 다음꺼 반환해
}
```

## ✅ Comparable, Comparator

- 데이터를 **정렬**하기

- `Arrays.sort()`

```java
Integer[] array = {3, 2, 1};
Arrays.sort(array); //정렬 {1, 2, 3};
```

- 내가 정렬 기준을 만들고 싶다면?
- create class that `implement Comparator`
- override `compare()`

```java
  static class AscComparator implements Comparator<Integer>{ //implement Comparator
        @Override
        public int compare(Integer o1, Integer o2) {
            System.out.println("o1: " + o1 +" o2 = " + o2);
            return (o1 < o2) ? -1 : (o1 == o2) ? 0 : 1 ; //ascending
        }
    }
```

```java
Arrays.sort(array, new AscComparator());  //array, my order class
Arrays.sort(array, new AscComparator().reversed()); //reverse 3->2->1
```

## ✅ Comparator to make my own compare()

- ✔️ I want to compare based on `user age`
- in `MyUser class`
- `implement comparable`

```java
public class MyUser implements Comparable<MyUser> { //implement comparable

    @Override
    public int compareTo(MyUser o) { //age ascending order
        return age > o.getAge() ? 1 : (age == o.getAge()) ? 0 : -1;
    }
}
```

- ✔️ I want to create another sort, sort with `Id`
- create new class `IdComparator`
- `implements Comparator`

```java
public class IdComparator implements Comparator<MyUser> { //implements Comparator
    @Override
    public int compare(MyUser o1, MyUser o2) {
        return o1.getId().compareTo(o2.getId()); //compare ascending Id
    }

}
```

- ✔️ Main class

```java
//use compareTo in MyUser class
Arrays.sort(array); //order in age 10 -> 20 -> 30

//use IdComparator class
Arrays.sort(array, new IdComparator()); //order in iD A->B->c
Arrays.sort(array, new IdComparator().reversed()); //order in ID C->B->A
```

### ☑️ Comparator in linkedList

- ✔️ Main class

```java
//use compareTo in MyUser class
linkedList.sort(null); //order in age 10 -> 20 -> 30

//use IdComparator class
linkedList.sort(new IdComparator()); //order in iD A->B->c
```

### ☑️ Comparator in tree

- in `tree`, `order & input value` is done at the **same time**
- 트리에서는 자료를 넣을 때부터 정렬해서 넣기 때문에 따로 정렬이 필요가 없음

```java
TreeSet<MyUser> treeSet = new TreeSet<>();
//이미 treeSet은 myUser을 age순서로 정렬해 저장해 둠

//use IdComparator class
//I want to order user with Id
//input in tree constructor
TreeSet<MyUser> treeSet = new TreeSet<>(new IdComparator()); //use IdComparator compare()

```

## ✅ Collection

```java
//max
Integer max = Collections.max(list);

//shuffle
Collections.shuffle(list);

//sort
Collections.sort(list);

//reverse
Collections.reverse(list);

//create immutable list
List<Integer> list = List.of(1, 2, 3);

//make list multi-thread safe
Collections.synchronizedList(arrayList);
```

## ✅

## ✅

## ✅

## ✅
