---
title: Dijkstra Algorithm
categories: [Coding Test, Algorithm]
tags: []
---

## ✅ Dijkstra Algorithm

> weighted graph
> find shorest path

## ⭐️ Keyword

weighed graph

## ✅ Time complexity

Adjacent Matrix: **O(N^2)** <br>
Adjacent List: **O(N\*logN)** <br>

## ✅ Code

1. array to save distance, if visited

```java
int[] distance;
boolean visited;
```

2. initialize distance to max

```java
for(int i = 1; i <= n; i++){
    distance[i] = Integer.MAX_VALUE;
}
```

3. initiate starting node distance, visited

```java
distance[start] = 0;
visited[start] = true;
```

4. check if visited, and set distance of the node

```java
for(int i = 1; i <= n; i++){
    if(!visited[i] && map[start][i] != 0) {
    	distance[i] = map[start][i];
    }
}
```

5. find the node that has not been visited, find min distance node

```java
int min = Integer.MAX_VALUE;
int midx = -1;

for(int i = 1; i <= n; i++){
    if(!visited[i] && distance[i] != Integer.MAX_VALUE) {
    	if(distance[i] < min) {
            min = distance[i];
            midx = i;
        }
    }
}
```

6. check visited array, reset minimum distance with root node

```java
visited[midx] = true;
for(int i = 1; i <= n; i++){
    if(!visited[i] && map[midx][i] != 0) {
    	if(distance[i] > distance[midx] + map[midx][i]) {
            distance[i] = distance[midx] + map[midx][i];
        }
    }
}
```

## 💡 Reference

<https://soheeparklee.github.io/posts/CT-67/>
