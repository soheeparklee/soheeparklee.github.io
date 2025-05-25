---
title: Map
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ Map

- `key` ➕ `value`
- `key`: unique
- `value`: duplication possible
- no order

## ☑️ HashMap

- `key` ➕ `value`
- add, search value: `O(1)`
- no order
- get all: random
- `O(1)`
- must override `hashCode()` and `equals()` to use hash index

<img width="384" alt="Image" src="https://private-user-images.githubusercontent.com/97790983/443758429-059ea566-d04a-490b-87c0-aa47b7514fb8.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDc4NjA5OTYsIm5iZiI6MTc0Nzg2MDY5NiwicGF0aCI6Ii85Nzc5MDk4My80NDM3NTg0MjktMDU5ZWE1NjYtZDA0YS00OTBiLTg3YzAtYWE0N2I3NTE0ZmI4LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA1MjElMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwNTIxVDIwNTEzNlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWY0NjViODAxNzNlNjcyZDU0OTc2ZjhhNjZjYTk2N2Y2Mjk2MGZhZDRkZjczZjdjOWI3MDgwNWQzYjBkOGM2MjMmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.UJFcE7qgPEGOQR_6gAP0Xf-0CtXgv1ltFsj7xRokzwI" />

```java
Map<String, Integer> studentMap = new HashMap<>();
studentMap.put("student1", 90);

//get value
studentMap.get("student1");
//get keys
Set<String> keys = studentMap.keySet();
//get values
Collection<Integer> values = studentMap.values();
//get key ➕ value
Set<Map.Entry<String, Integer>> entries = studentMap.entrySet();
```

## ☑️ LinkedHashMap

- `HashMap` ➕ `linkedList(order)`
- add, search value: `O(1)`
- get all: input order
- `O(1)`

## ☑️ TreeMap

- `HashMap` ➕ `tree`
- get all: `key` ascending order
- `O(logN)`

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅
