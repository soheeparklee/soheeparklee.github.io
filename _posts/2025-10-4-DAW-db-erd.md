---
title: 2. Data Modeling
categories: [DAW bilingual, Database]
tags: [] # TAG names should always be lowercase
---

## ✅ Data Modeling

- Conceptual data model ➡️ ERD
- ERD ➡️ Logical data model
- Physical data model: implemented in DBMS using SQL

## ✅ ERD

> Diagram of relationship of entity sets

✔️ **Three components of ERD**

- 1️⃣ Entity
- 2️⃣ Attribute
- 3️⃣ Relationship

## ✅ Entity

> Object or concept about which you want to store information

- distinguishable from other objects
- 💡 rectangle ◼️
- 💡 consise singular noun

✔️ **Entity xxx**

- 1️⃣ Entity type: collection of entities that have same attribute `Student`
- 2️⃣ Entity instance: one item in entity `So Hee`
- 3️⃣ Entity set: set of entity instances `So Hee, Alan, Pepe...`

✔️ **Type of Entity**

- 1️⃣ Strong
- 2️⃣ Weak
  - existance entity
  - identification entity

## ✅ Attribute

> property/feature/characteristic of entity

- 💡 ovals 🔵
- 💡 start with uppercase letter `Name, Address`
- if more than two words, first letter of each subsequent word also in uppercase `Student ID`

✔️ **Atrribute type: how many**

- 1️⃣ Single: single value for each entity instance
- 2️⃣ Multivalued: can have more than one, `languages a student speaks`

✔️ **Atrribute type: can be divided**

- 1️⃣ Single or atomic: cannot be divided `City`
- 2️⃣ Composite: `Address ➡️ City, State, Zip, Street`

✔️ **more Atrribute types:**

- 3️⃣ Derived or stored: can be caculated `Age = year - birthday`
- 4️⃣ Mandatory
- 5️⃣ Optional

## ✅ Key

> identifier

- can uniquely identify an individual instance of an entity
- 💡 underline primary key, or use ⚫️

- 0️⃣ Composite key: several attributes together uniquely identify an instance
- 1️⃣ Natural key
- 2️⃣ Surrogate key
- 3️⃣ Candidate key
- 4️⃣ Primary key: represented with `underline` or ⚫️, `(1)` each row should have unique primary key `(2)` primary key cannot be null
- 5️⃣ Alternate key
- 6️⃣ Foreign key

## ✅ Domain

> restraints/allowed value of an attribute

## ✅ Relationship

> how entityes connect/associate with each other

- 💡 diamon shape 🔷
- 💡 present tense verb

✔️ **Relationship xxx**

- 1️⃣ Relationship set: grouping of all matching relationship instances
- 2️⃣ Relationship type: relationship between entity types

📌 **Relationship attribute**

> Relationship can have attributes

- If `Student` enrolls in a `Module`
- entity: `Student`, `Module`
- relationship: `ENROLL`
- relationship attribute: `grade`

## ✅ Grade

> number of entities that participate in this relationship

✔️ **Type of Grade**

- 1️⃣ Unary/self-linked/reflexive/recursive
- 2️⃣ Binary, degree 2: DB will only seek grade 2 relationship
- 3️⃣ N-ary or defree n: should be simplified
- 4️⃣ Double grade: two entity with two relationship

## ✅ Cardinality

✔️ **Type of cardinality**

- 1️⃣ Relationship cardinality `X : X`
  - max number of isntances that can participate in one relationship instnace
  - `1:1`, `1:N`, `N:M`
- 2️⃣ Entity cardinality `X, X`
  - min and max number of instances that may relate to an instance of another entity
  - `0, 1`, `1, 1`, `1, N`, `N, M`
  - 💡 indicated on both sides of the relation

## ✅ Redundancy control

> remove redundant element from schema

- schema is redundant if no information is lost even when removed from schema
- redundant schema contains a loop

## ✅ Extended Entity Relationship Model

- 1️⃣ Superclass
- 2️⃣ Subclass
- 3️⃣ Hierarchical relationship: `IS-A`
- 4️⃣ Aggregation: combining instances of several entities to represent the parts of a whole represented in the instances of another entity

## ✅ Hierarchical relationship `IS-A`

> when one entity can be **subdivided** into other entities

✔️ **Type of Hierarchical relationship: exclusive⭕️❌**

- 1️⃣ Elclusive: instance of supertype can only be one subtype, `Ｕ`
- 2️⃣ Overlapping: can appear in several subtype

```
          Person
        /       \
    Student    Teacher

1️⃣ Elclusive: you can be either student or teacher
2️⃣ Overlapping: you can be both student and teacher
```

✔️ **Type of Hierarchical relationship: total⭕️❌**

- 1️⃣ Total: all instances of superclass must be represented by one of subtypes `⚫️`
- 2️⃣ Partial: not all supertype will be part of subclass

```
          Person
        /       \
    Student    Teacher
1️⃣ Total: all people in this school will either be student or teacher
2️⃣ Partial: person can be technician
```

## ✅ Exclusive OR(XOR)

- existence or a relationship prevents the existence of another

## ✅ Heritage

- entity is composed of one or more entities

**✔️ Types of Heritage**

- 1️⃣ Composite/Component: entity is obtained by union of several entities, can be different objects and play different roles
- 2️⃣ Member/Collection: entity obtained by same type of entity, that plays same role

## ✅ Aggregation

- in ERD, it is NOT possible to represent relationship between relationship
- 👉🏻 Thus, use **aggregation** and treat relationship as higher level entity
- max, min cardinality of aggregated entity will always be `(1, 1)`
