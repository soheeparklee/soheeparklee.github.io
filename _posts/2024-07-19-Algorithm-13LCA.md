---
title: Lowest Common Ancestor
categories: [Coding Test, Algorithm]
tags: []
---

## ✅ Lowest Common Ancestor

> longest subsequence which is common in input sequences

Example:

```java
//input
S1= "ABC"
S2= "ACD"
//output
2
//explanation
"AC"
```

![Screenshot 2024-07-19 at 19 15 17](https://github.com/user-attachments/assets/59f6dd19-4901-4ae1-a5ec-e8e423192172)

## ✅ Code

```java
//depth
0 -> 1 (root)
1 -> 2, 3
2 -> 4, 5, 6, 7
```

```java
//root node(1) has no parent -> 0
//node 2 parent: 1
//node 6 parent: 3
int parent= {0, 1, 1, 2, 2, 3, 3}
```

```java
//check two nodes
while(true){
    if(if the depth of two nodes ==){
        if(two node parent ==) return LCA
        else change two nodes parent into current node parent
        //for node 4 and 6, depth==, however parent would be each 2, 3.
        //Thus, change parent to 1
    }else{ //depth of two nodes does not match
        change parent of deeper node into current node parent
        //for node 2 and 6, depth would be each 1, 2
        //Thus change node parent for 6(deeper), into node 2 parent, which is 1.
        //LCA(2, 6) = 1
    }
}
```

## ✅ Time complexity

**O(2^m+n)**

## ✅ Space complexity

**O(1)**

## 👍🏻 Pros

## 👎🏻 Cons

## 💡 Reference
