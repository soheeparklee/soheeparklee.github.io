---
title: Anomaly, Normalization
categories: [Database, DB]
tags: [] # TAG names should always be lowercase
---

## ✅ Anomaly

> 이상 현상 <br>
> 테이블을 잘못 설계하여 데이터 삽입, 삭제, 수정할 때 오류 발생 <br> > <br>

**1. Insertion Anomaly**

> need to add unnecessary data to instert

- when {student ID, course ID} is primary key,
- if need to save students who did not take a course
- these students' course ID would be null
- primary key cannot be null
- thus, cannot insert students who did not take a course, unless adding unnecessary data

<br>

**2. Update Anomaly**

> updating a part of data, so that data is not consistent

- update student deparement from music to computer
- need to update all deparetments
- update anomality happends when update miss to update ome departments

<br>

**3. Deletion Anomaly**

> deleting even the necessary data

- when student withdraw from a course
- delete student information as well

## ✅ Normalization

> 정규화 <br>
> 중복을 최대한 줄여 데이터 구조화 <br>
> 불필요한 데이터 제거, 논리적으로 데이터 저장 <br>
> goal: data integrity <br>
> reduce data **repetition**, increase data integrity <br>

- 👍🏻 data integrity
- 👍🏻 save DB resource

**✔️ 1NF(First Normal Form)**

> table column to have **one atomic value** <br>
> Don't use multiple fields in a single table to store similar data <br>

- one phone number per user
- one feature per user

<img width="442" alt="Screenshot 2024-09-19 at 11 40 43" src="https://github.com/user-attachments/assets/d8a9258d-b0d9-40d6-8c04-958b9d3904a7">

**✔️ 2NF**

> Create separate tables for sets of values that apply to multiple records. <br>
> Relate these tables with a foreign key <br>

- 제 1 정규화를 진행한 테이블에 대해 완전 함수 종속 만족시키기
- 완전 함수 종속: 기본키의 부분집합이 결정자가 되어선 안된다.

- user address is used in customer table, orders, shipping, invoices table.
- do not repeat this field as a seperate entry in all tables, but place it on customer table and set foreign key

<img width="601" alt="Screenshot 2024-09-19 at 11 43 04" src="https://github.com/user-attachments/assets/7ac00686-4b4c-49a5-ad88-475c27cb05e1">

**✔️ 3NF**

> Elimiate fields that don't depend on key

- 제 2 정규화를 진행한 테이블에 대해 이행적 종속 없애기
- **이행적 종속**: `A -> B`, `B -> C`가 성립할 때, `A -> C`가 성립하는 것

<img width="597" alt="Screenshot 2024-09-19 at 11 45 25" src="https://github.com/user-attachments/assets/0d2abc45-bd04-4b83-b066-6c9d7d308dcc">

**✔️ BCNF 정규화**

- 제 3 정규화를 진행한 테이블에 대해 모든 결정자가 후보키가 되도록 테이블 분해
