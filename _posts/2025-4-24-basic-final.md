---
title: Final, Constant
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ Final

- `final`: **can not** change after initialization
- final value can not be altered after initializatoin
- 처음 값 할당 후에는 변수의 값을 변경하지 못하게 막아버린다

- 👎🏻 **without final**

```java
int data0;
data0 = 10;
data0 = 20; //change value possible
```

- 👍🏻 **with final**
- 처음 한번만 값 할당 가능
- `final`이 붙으면 바꿀 수 없음

```java
final int data1;
data1 = 10; //can set value once
//data1 = 20; //🔴compile error
```

## ✅ static final

- `static`: 인스턴스끼리 공유
- `final`: 한번 생성 후에는 바꿀 수 없다

```java
public class Student{
    static final int STUDENT_AGE = 15; //STATIC FINAL write in CAPITAL LETTERS
    final int grade;

    public Student(int grade){
        this.grade = grade; //initiate student with grade, grade will never change
    }
}

public class StudentMain{
    public static void main(String[] args){
        Student student1 = new Student(100);
        Student student2 = new Student(90);
        Student student3 = new Student(80);
    }
}
```

- ✔️ 이렇게 생성하면 all `student 1, 2, 3` will have `age = 15`
  - `static STUDENT_AGE` will be shared among all `student instance`
  - `static STUDENT_AGE` is saved only once in `method memory`
  - since `final STUDENT_AGE`, age can not be altered
- ✔️ each student will have `grade` `100`, `90`, `80`
  - since `final int grade`, `grade` can not be altered

## ✅ Constant

- 하나만 존재하고 : `static`
- 변하지 않는 값: `final`
- constant is used to `make a fixed value` to use the value itself
- constant is normally written in CAPITAL_LETTERS

```java
public class Constant {

    public static final int HOURS_IN_DAY = 24;
    public static final int MINUTES_IN_HOUR = 60;
    public static final int SECONDS_IN_MINUTE = 60;

    public static final int MAX_USERS = 1000;
}
```

```java
public class ConstantMain {
    public static void main(String[] args){
        Constant.HOURS_IN_DAY;
        Constant.MAX_USERS;
    }
}
```

- 👍🏻 유지보수가 쉽다.
- `MAX_USERS`를 바꾸고 싶으면 `Constant`클래스에 가서 한번만 바꾸면 됨

## ✅ Final reference value can be altered

```java
public class Data {
    public int value;
}
```

- `public int value` is not final

```java
public class FinalRefMain {
    public static void main(String[] args) {
        final Data data = new Data(); //data instance is final
        //data = new Data(); //🔴final value can not be altered after initialization

        data.value = 10;
        data.value = 20; //🟢even when instance final, reference value can be altered
        //value is not final
    }
}
```

- `final Data data = new Data()` is final
- however, `value` field in `Data class` is not final
- so `value` field can be altered as many times

## ✅

## ✅

## ✅

## ✅
