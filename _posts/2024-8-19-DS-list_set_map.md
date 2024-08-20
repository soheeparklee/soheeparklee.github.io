---
title: List/ Set/ Map
categories: [Computer Science, DataStructure]
tags: [] # TAG names should always be lowercase
---

## ✅ List

- has `index`
- can `get()` element by `index`
- 👍🏻 search, regularly access the element
- duplicate element possible ⭕️
- insertion order ⭕️
- store null ⭕️

## ✅ Set

- 👍🏻 build collection of distinct items
- duplicate items impossible ❌
- insertion order ❌
- only one null value

> **When to use set, instead of list?** <br>
>
> > when all items need to be unique <br>

## ✅ Map

- key ➕ value are mapped
- hold pairs of keys and values
- 👍🏻 store data in `key-value` form
- duplicate `key` impossible ❌
- duplicate `value` possible ⭕️
- insertion order ❌
- allow single null key at most
- allow null value ⭕️

```java
        // Creating object for a Map.
        Map<String, Integer> map
            = new HashMap< String, Integer>();

        // Adding Elements using Map.
        map.put( "Rajat", 101);
        map.put("Shyam", 102);
        map.put("Rahul", 103);
        map.put("Krishna", 104);
```

## ☑️ ArrayList

<img width="329" alt="Screenshot 2024-08-20 at 01 15 45" src="https://github.com/user-attachments/assets/8e988992-e921-4322-bc3e-59083d1031b5">

- one direction pointer
- 👍🏻 fast in search

## ☑️ LinkedList

<img width="465" alt="Screenshot 2024-08-20 at 01 32 20" src="https://github.com/user-attachments/assets/542999a7-92c4-4d1b-9298-18ed386b05eb">

- double direction pointer
- 👍🏻 fast in insertion, deletion

ArrayList 🆚 LinkedList <https://soheeparklee.github.io/posts/DB-3array-list-linked/>

## ☑️ HashSet

```java
// Instantiate an object of HashSet
HashSet<ArrayList> set = new HashSet<>();

// create ArrayList list1
ArrayList<Integer> list1 = new ArrayList<>();

// create ArrayList list2
ArrayList<Integer> list2 = new ArrayList<>();

// Add elements using add method
list1.add(1);
list1.add(2);
list2.add(1);
list2.add(2);
set.add(list1);
set.add(list2);

// print the set size to understand the
// internal storage of ArrayList in Set
System.out.println(set.size());

//result = 1
//two lists are considered equal if they have the same elements in the same order
```

- creates collection that stores elements in a hash table
- hash code, to function as object identifier
- insertion order not guaranteed ❌
- data duplication ❌

## ☑️ LinkedHashSet

- Linked list ➕ Hash Table
- insertion order guaranteed ⭕️(list의 특징)
- data duplication ❌(set의 특징)

## ☑️ TreeSet

- (default) if data can be compared, ordered in ascending otder
- data duplication ❌
- can implement `comparable`

## ☑️ HashMap

<img width="375" alt="Screenshot 2024-08-20 at 12 47 18" src="https://github.com/user-attachments/assets/a1ba205d-2d27-4e2d-9723-d578ff303f6d">

- insertion order not guaranteed ❌
- key duplication imossible ❌

## ☑️ LinkedHashMap

- insertion order guaranteed ⭕️
- key duplication imossible ❌

## ☑️ TreeMap

- save `key-value` on `red-black tree`
- (default) if data can be compared, ordered in ascending otder
- can implement `comparable`
