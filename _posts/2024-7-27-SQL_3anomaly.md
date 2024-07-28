---
title: Anomaly
categories: [Database, DB]
tags: [] # TAG names should always be lowercase
---

## ✅ Anomaly

> 정규화를 해야 하는 이유, 이상현상

1. Insertion Anomaly
   > need to add unnecessary data to instert

- when {{student ID, course ID}} is primary key,
- if need to save students who did not take a course
- these students' course ID would be null
- primary key cannot be null
- thus, cannot insert students who did not take a course, unless adding unnecessary data

2. Update Anomaly
   > updating a part of data, so that data is not consistent

- update student deparement from music to computer
- need to update all deparetments
- update anomality happends when update miss to update ome departments

3. Deletion Anomaly
   > deleting even the necessary data

- when student withdraw from a course
- delete student information as well
