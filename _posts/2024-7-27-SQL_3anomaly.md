---
title: Anomaly 정규화
categories: [Database, DB]
tags: [] # TAG names should always be lowercase
---

## ✅ Anomaly

> 정규화 <br>
> 중복을 최대한 줄여 데이터 구조화 <br>
> 불필요한 데이터 제거, 논리적으로 데이터 저장 <br>
> 목표: 이상현상이 일어나지 않도록! <br>

<br>

1. Insertion Anomaly
   > need to add unnecessary data to instert

- when {{student ID, course ID}} is primary key,
- if need to save students who did not take a course
- these students' course ID would be null
- primary key cannot be null
- thus, cannot insert students who did not take a course, unless adding unnecessary data

<br>

2. Update Anomaly
   > updating a part of data, so that data is not consistent

- update student deparement from music to computer
- need to update all deparetments
- update anomality happends when update miss to update ome departments

<br>

3. Deletion Anomaly
   > deleting even the necessary data

- when student withdraw from a course
- delete student information as well
