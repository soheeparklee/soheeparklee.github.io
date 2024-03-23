---
title: Entity 🆚 Repository 🆚 JPA
categories: [JAVA, Spring]
tags: [entity, repository, jpa] # TAG names should always be lowercase
---

## ✅ JPA

> JAVA **persistence** API
> <br>

> 💡 여기서 persistence의 뜻은?<br>
> persistence는 고집, 즉 **영속성**, 따라서 프로그램이 종료되더라도 사라지지 않는 데이터의 특성을 의미한다. <br>
> persistence는 파일 시스템, RDB 혹은 객체 데이터베이스 등을 활용하여 구현한다. <br>
> 데이터에 persistence한 특징이 없다면 단지 메모리에서만 존재하기 때문에 프로그램을 종료하면 모두 잃어버리게 될 것이다! <br>

> ☑️ "persistence" in the context of JPA<br>
> "persistence" refers to the ability of Java objects to be stored, retrieved, and managed in a long-term storage medium, typically a relational database

- store objects
- retrieve objects
- manage object lifecycle
- mapping java objects to database tables
- transaction management: data consistency and integrity

## ✅ Entity

> corresponds to a database table

- Represent domain object
- each instance in entity is a row in a table
  ✔️ example: userId, name, email, gender

## ✅ Repository

> design pattern
> provides abstraction layer for storing and retrieving data

- provide CRUD along with query methods for interacting with entities
- custom queries on **entities**
  ✔️ example: save, findById, findAll

## ✅ DTO

> Data Transfer Object

- object for data encapsulation and transfer between presentation layer and business layer
