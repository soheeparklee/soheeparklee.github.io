---
title: Class
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ Why do we need class?

- collect each student's charecteristics in one class
- create one student class
- and save one student's name, age, grade in one class

- there is `int type`, `String type` in Java
- we save numbers in `int type` and letters, words in `String type`
- why not create `Student type` when we need, and save students in `Student type` class?

#### 👎🏻 before

- student1, student2 contents are distributed into arrays
- more difficult to know about student1

```java
String[] studentNames = {"학생1, 학생2"}
int[] studentAges = {15, 16};
int[] studentGrades = {90, 80};
```

#### 👍🏻 after

- create student class

```java
public class Student {

    String name;
    int age;
    int grage;
}
```

- create student in Main class
- save one student fields in one class

```java
public class studentMain {
    public static void main(String[] args) {
        Student student1 = new Student(); //create student
        student1.name = "student1"; //save student fields
        student1.age = 15;
        student1.grage = 90;
    }
}
```

#### ✔️ class is like a blueprint

- create `types` that developer needs
- create `student` blueprint
- and save student1, student2...

## ✅ Class, Object, Instance

- `student class` : class
- `student1`, `student2`... : instance
- `student1` and `student2` are different objects
- `student1` **object** is an **instance** of `student` **class**

- **class** is a blueprint of an instance
- defines field and method of instance
- **instance** is created based on **class**
- object and instance are used interchangeably
