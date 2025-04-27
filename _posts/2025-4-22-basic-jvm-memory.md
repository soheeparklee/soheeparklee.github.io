---
title: Java memory, Static, psvm
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ Method, Stack, Heap

<img width="500" alt="Image" src="https://github.com/user-attachments/assets/e7385999-de78-4c12-8198-ac5d676642aa" />

✔️ **Method**

- class

✔️ **Stack**

- methods
- program is run

✔️ **Heap**

- Instance created
- `new`
- class instance, array

## 💡 Method

<img width="492" alt="Image" src="https://github.com/user-attachments/assets/ac5c4512-c9c3-4c62-80bc-767c1495508c" />

- **shared** data to run program
- `class`: field, method, constructor...
- `static`: shared among instances
- literal

## 💡 Stack

- `methods` run in main class
- `local variables`, `parameter`, method return values...

- LIFO
- `main() start` ➡️ `method1 start` ➡️ `method2 start`
- `method2 end` ➡️ `method1 end` ➡️ `main() end`

- method in class 🆚 method in main class
- method in class: `method` area, shared data for creating instances
- method in main class: `stack` area

## 💡 Heap

- `Instance`, `array`
- `new` instance
- GC is run in heap area
- if value is not referenced in `heap` area, GC would free address space

- student class 🆚 student 1 instnace
- `new` student 1 instance is made from student class

  - student class: method area
  - student 1 instance made from student class: heap area
  - student 2 instance made from student class: heap area
    - student 1, 2 instance will be each allocated address space in heap area
    - however, student class is used commonly for student 1, student 2

```java
public static void main(String[] args) {
        method1();
    }

    static void method1() {
        Data data1 = new Data(10);
        method2(data1);
    }

    static void method2(Data data) {
    }
```

- `main() start`
- ➡️ `method1 start`
- ➡️ `new data1` in heap allocated address space
- ➡️ `method2 start`
- ➡️ `method2 end`
- ➡️ `method1 end`
- ➡️ `new data1` in heap is not referenced anymore
- ➡️ GC clean
- ➡️ `main() end`

## ✅ Static

- `student class`로 `student 1, 2, 3...`등 만들건데, **인스턴스간에 공유**하는 변수를 지정할 수는 없을까?

- 1️⃣ `static` is to **share** among instances
- 2️⃣ `static` variables are saved in `method memory`, only once
  - normally, instance is created in `heap`
  - however, bc `static` is **shared** among instances, it is saved in `method memory`
  - only saved once(shared among instance)
- 3️⃣ `static` variables can be used _without_ creating instance

- 👎🏻 **Before(without static)**

```java
public class Data1 {
    public String name;
    public int count; //👎🏻 not static

    public Data1(String name){
        this.name = name;
        count++; //when data instance is created, ++
    }
}
```

```java
public class DataCountMain1 {
    public static void main(String[] args) {
        Data1 data1 = new Data1("A");
        System.out.println("data: " + data1.count);

        Data1 data2 = new Data1("B");
        System.out.println("data: " + data2.count);

        Data1 data3 = new Data1("C");
        System.out.println("data: " + data3.count);
    }
}
```

- ✔️ result

```
data: 1
data: 1
data: 1
```

- when instance is created, `count` is `0`
- thus, making `count++` will be `1`

- 👍🏻 **After(with static)**

```java
public class Data3 {
    public String name;
    public static int count; //👍🏻 implement static

    public Data3(String name){
        this.name = name;
        count++;
    }
}
```

```java
public class DataCountMain3 {
    public static void main(String[] args) {
        Data3 data1 = new Data3("A");
        System.out.println("data: " + Data3.count); //static

        Data3 data2 = new Data3("B");
        System.out.println("data: " + Data3.count); //static

        Data3 data3 = new Data3("C");
        System.out.println("data: " + Data3.count); //static
    }
}
```

- ✔️ result

```
data: 1
data: 2
data: 3
```

- `static` variables can be used without creating instance
- `Data3.count` ⭕️
- `data1.count` ❌

- `static int count` is **shared** among instance `data 1, 2, 3`
- thus every time instance is created, `기존 count++`
- because `static int count` is **shared** among instance, saved in `method` part of memory
  - only once saved in `method` memory
- 🆚 `String name`(not static) will be saved in `heap` part of memory
  - saved `3` times in `heap` memory
  - (created instance `3` times)

## Local variable 🆚 Instance variable 🆚 Class variable

```java
public class Data3 {
public String name; //class field, instance variable
public static int count; //class field, class variable, static
}
```

- Local variable: saved on memory `stack`, short life
- Instance variable: saved on memory `heap`, cleaned by GC
- Class variable: saved on memory `method`, longest life as variable

## ✅ Static Method

- 1️⃣ `static` method can be used without creating instance

- 👎🏻 **Before(without static)**

```java
public class DecoUtil1 {
    public String deco(String str){
        return  str;
    }
}
```

```java
public class DecoMain1 {
    public static void main(String[] args) {
        String s = "hello";

        DecoUtil1 utils = new DecoUtil1(); // 👎🏻 create instance
        utils.deco(s); // 👎🏻 then use method
    }
}
```

- 👍🏻 **After(with static)**

```java
public class DecoUtil2 {
    public static String deco(String str){ //static
        return  str;
    }
}
```

```java
public class DecoMain2 {
    public static void main(String[] args) {
        String s = "hello";

        DecoUtil2.deco(s); //call static method without creating instance
    }
}
```

- 2️⃣ `static` method can only use `static field` and `static method`
- 🆚 `instance` method can use both `static`, `instance`

```java
public class DecoData {
    private int instanceValue; //instance variable
    private static int staticValue; //static

    public static void staticCall(){ //static
        staticValue++; //static can use static
        //instanceValue++; //🔴compile error, static can only use static
        //instanceMethod(); //🔴static can only use static
    }

    public void instanceMethod(){
        staticValue++; //🟢instance can use both static and not static
        instanceValue++;
        staticCall();
    }
}
```

- 🤨 **Why `static` method can only use `static`?**
- `static` is created in `method`
- `static` can be used without creating instance
- thus, if `static` calls an `instance field or method`, the `instance` might not have been created yet!

```java
public class DecoDataMain {
    public static void main(String[] args) {
        DecoData.staticCall(); //static method is called from class, do not need instance to be created

        DecoData data = new DecoData();
        data.instanceMethod(); //instance method is called from instance, after creating instance
    }
}
```

## ✅ psvm Main()

- `main method` is also `static`

```java
public static void main(String[] args) {}
```

- 1️⃣ can use `main()` method without creating `main instance`
- `main()` is used to start the programs
- 2️⃣ methods called in `main()` should also be `static`

## ✅

## ✅
