---
title: Constructor, this
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ this

- `this` refers to the field of the **current** class
- `this` is to distinguish which is `field` and which is `paramter` when the variable names are the same

- `this.name`: the `name` field of this class
- `name`: the `name`parameter for method `initMember`

```java
public class MemberInit {
    String name; //🔴
    int age;
    int grade;

    void initMember(String name //🔵, int age, int grade){
        this.name//🔴 = name; //🔵
        this.age = age;
        this.grade = grade;
    }

}
```

- in `Main class` to create a new member
- this code will create a new `member`, with name of `member1`

```java
MemberInit member1 = new MemberInit2();
member1.initMember("member1", 15, 90);
```

- ⭐️ so if `field name` and `parameter` is different, **no need** for `this`

```java
public class MemberThis {
    String nameField;

    void initMember(String nameParameter){
        nameField = nameParameter;
        //this.nameField = nameParameter; // this is also possible
    }
}
```

- ⭐️ `this` is to distinguish which is `field` and which is `paramter`
- ⭐️ if variable names were same in `MemberThis` the same code would look like this

```java
public class MemberThis {
    String name;

    void initMember(String name){
        this.name = name;
    }
}
```

## ✅ Constructor

- 👍🏻 allows to create instance and set the fields at the same time
- 👍🏻 if instance is created and fields are not set, compile error
- (prevent ghost member with no fields being created)

- constuctor name == class name
- no return value

```java
public class MemberConstruct {
    String name;
    int age;
    int grade;

    MemberConstruct(String name, int age, int grade){ //constuctor name == class name
        this.name = name;
        this.age = age;
        this.grade = grade;
    }
}
```

- 👎🏻 before

```java
    MemberConstruct member1 = new MemberConstruct();
    member2.name = "member1";
```

- 👍🏻 after

```java
    MemberConstruct member1 = new MemberConstruct("member1", 15, 90);
    //use constructor, 그러면
    //한번에 create class and field 가능
```

## ✅ Default contructor

- we need a constructor to create an instance

```java
MemberDefault member = new MemberDefault();
```

- basic default constructor is automatically created by Java
- has no field

```java
public class MemberDefault {
    String name;

    MemberDefault(){} //basic default constructor
}
```

- if there is any other constructor, basic constuctor will not be made

```java
public class MemberDefault {
    String name;

    MemberDefault(String name){ //other constructor
        this.name = name;
    }
}
```

```java
//now this is impossible
MemberDefault member = new MemberDefault(); //🔴compile error

//only this is possible
MemberDefault member = new MemberDefault("memberName"); //use other constructor
```

## ✅ constructor overloading

- not all fields in class has to be in constuctor

```java
    MemberConstruct(String name, int age, int grade){
        this.name = name;
        this.age = age;
        this.grade = grade;
    }

    MemberConstruct(String name, int age){ //no grade, grade will be 0
        this.name = name;
        this.age = age;
    }
```

```java
MemberConstruct member1 = new MemberConstruct("member1", 15, 90); //member1 15 90
MemberConstruct member2 = new MemberConstruct("member2", 16); //member2 16 0
```

## ✅ This and Constructor

- also can call constuctor in constuctor
- ⭐️ `this()` always has to come first line

```java
    MemberConstruct(String name, int age, int grade){
        this.name = name;
        this.age = age;
        this.grade = grade;
    }

    MemberConstruct(String name, int age){ //call constructor in constructor
        this(name, age, 0); //⭐️first line
    }
```

- `this` always has to come first in a constructor
- You can only call one other constructor

```java
    public Student(int age) {
        this.age = age;
    }

    public Student(int age, int grade) {
        this(0); // call the other constructor with a default age
        this.grade = grade;
    }
```

## ✅ Copy Constructor

- constructor that creates a **new object** by copying data from another object of the same class

```java
public class Student {
    int age;

    public Student(int age) {
        this.age = age;
    }

    public Student(Student student){ //create deep copy
        this.age = student.age;
    }
}

public class Main {
    public static void main(String[] args) {
        Student studentA = new Student(10);
        Student studentB = studentA; //just point to same reference
        Student studentC = new Student(studentA); //using copy constructor

        studentA.setAge(20); //change original
        System.out.println(studentA.getAge()); //20
        System.out.println(studentB.getAge()); //20
        System.out.println(studentC.getAge()); //10, does not change

    }
}
```

- `studentA` and `studentC` are **different** object
- initially `studentC` fields were copied from `studentA`

- ❓ **Why Use a Copy Constructor?**
- To create `deep copies` of objects safely (avoiding unwanted shared references).
- To duplicate complex objects easily.

## Shallow copy 🆚 Deep copy

- Shallow copy: Copies field values **as-is**, including **references** to other objects.
- Deep copy: Creates **new objects** for any referenced fields too.

- ✔️ **Example of shallow copy**

```java
class Department {
    String name;
}

class Employee {
    String name;
    Department dept;

    // Copy constructor (shallow copy)
    Employee(Employee e) {
        this.name = e.name;
        this.dept = e.dept; // same reference!
    }
}
```

- Both Employee objects share the **same Department instance**.

- ✔️ **Example of deep copy**

```java
Employee(Employee e) {
    this.name = e.name;
    this.dept = new Department(); //new Deparment!
    this.dept.name = e.dept.name;
}
```
