---
title: Nested Class, Inner Class
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ Nested Class

- class with class inside

- ✔️ **Types of nested class**
- 1️⃣ Static nested class
- Non-static nested class
  - 2️⃣ Inner class
  - 3️⃣ Local class
  - 4️⃣ Anonymous class

<img width="552" alt="Image" src="https://github.com/user-attachments/assets/4f24cf5d-bfae-46d7-a700-29f11b7457e6" />

- 🆚 `Nested`: 내 안에 있지만 내것이 아닌 것(나무 상자 안에 작은 다른 나무 상자`nested`)
  - `Static nested class`는 `바깥 클래스`와 전혀 **다른** 클래스
  - 따라서 `바깥 클래스`의 instance에 소속되지 않는다 ❌
- 🆚 `Inner`: 내부에서 나를 구성하는 요소(내 안에 내 심장`inner`이 있다)

  - `Inner class`는 `바깥 클래스`를 구성하는 요소
  - 따라서 `바깥 클래스`의 instance에 소속된다 ⭕️

- 1️⃣ Static nested class ➡️ static variable(class variable)위치에 선언
- 2️⃣ Inner class ➡️ instance variable 위치에 선언
- 3️⃣ Local class ➡️ local variable 위치에 선언(inside code block)
- 4️⃣ Anonymous class

## 1️⃣ Static nested class

- static
- not instance of `outer class`
- `inner` and `outer` class DO NOT HAVE any relationship

- ✔️ **Example of static nested class**
- `NestedOuter` and `Nested` 는 아무 관계가 없는 서로 전혀 다른 클래스들이다
- `Nested` 는 `NestedOuter`안에서만 쓰이는 클래스

- 🟢 can access my `class field`
- 🔴 can NOT access `instance field` of `outer classs`
- 🟢 can access `class field` of `outer classs`
- 🟢 can access `private` of `outer classs`

```java
public class NestedOuter {
    private static int outClassValue = 3; //class field
    private int outInstanceValue  = 2; //instance field


    //static nested class
    static class Nested{
        private int nestedInstanceValue = 1;

        public void print(){
            nestedInstanceValue; // 🟢 can access my class field
            //outInstanceValue // 🔴 CAN NOT access instance field of outer class
            outClassValue; //🟢 CAN access class field of outer class
                           //🟢 CAN access private field of outer class
        }
    }
}
```

- ✔️ **Example of main class**
- to create `nested class`, DO NOT need to create `outer class`

```java
public class NestedOuterMain {
    public static void main(String[] args) {
        NestedOuter nestedOuter = new NestedOuter(); //create outer class
        NestedOuter.Nested nestedInner = new NestedOuter.Nested();
        //⭐️ create inner class
        //can be created without outer class

        nestedInner.print(); //call method in inner class

        nestedOuter.getClass(); //NestedOuter
        nestedInner.getClass(); //.NestedOuter$Nested
    }
}
```

- 👍🏻 encapsulation
- 👍🏻 can hide `inner class`

## 2️⃣ Inner class

- not static
- `inner class` is instance of `outer class`
- `inner` and `outer` class are linked(referenced)
- can access `outer class` isntance member

- ✔️ **Example of inner class**

- 🟢 can access my `class field`
- 🟢 can access `instance field` of `outer classs`
- 🟢 can access `class field` of `outer classs`

```java
public class InnerOuter {
    private static int outClassValue = 3;
    private int outInstanceValue = 2;

    class Inner{
        private int innerInstanceValue = 1;
        public void print(){
            innerInstanceValue; //🟢 can access my class field
            outInstanceValue; //🟢 can access instance field of outer class
            outClassValue; //🟢 can access class field of outer class
        }
    }
}
```

- ✔️ **Example of main class**
- create inner class: `InnerOuter.Inner inner = outer.new Inner();`
- to create inner class, MUST CREATE `outer class` first
  - first create `outside class`
  - then create `inner class`
  - `outer class` ref to `inner class`

```java
public class InnerOuterMain {
    public static void main(String[] args) {
        InnerOuter outer = new InnerOuter(); //outer class
        InnerOuter.Inner inner = outer.new Inner(); //⭐️ create inner class

        inner.print(); //call inner method

    }
}
```

### 💡 Inner class example

- 👎🏻 **Before**
- `Car` class, `Engine` class

<img width="1316" alt="Image" src="https://github.com/user-attachments/assets/5064358b-c108-48c0-a5ee-66798b432d2a" />

- 👍🏻 **After**
- `Engine` class **inner class** of `Car` class

```java
public class Car {
    private String model;
    private int chargeLevel;
    private Engine engine;

    public Car(String model, int chargeLevel) {
        this.model = model;
        this.chargeLevel = chargeLevel;
        this.engine = new Engine(); //👍🏻 dont need new Engine(this)
    }

    //👍🏻 no need for getChargeLevel()
    //👍🏻 no need for getCarModel()

    public void startCar(){
        engine.startEngine();
        System.out.println(model + "car started ready");
    }

    private class Engine { //⭐️ Engine is inner class of Car
        //👍🏻 dont need Car field
        //👍🏻 dont need constructor

        public void startEngine(){
            //👍🏻 can access Car field without method
            System.out.println("car chanrge level: " + chargeLevel);
            System.out.println(model + " is starting engine");
        }
    }
}
```

## ✅ Shadowing

- 이름이 같은 변수가 `outside class`, `inner class` 모두에 있어
- `inner class`에 있는 변수가 우선순위를 가짐
- `outside class`에 있는 같은 이름 변수는 가려짐 ➡️ shadowing

```java
public class ShadowingMain {

    public int value = 1; //outer class field

    class Inner{
        public int value = 2; //inner class field

        void innerMethod(){
            int value = 3; //local variable

            this.value; //acess inner class field
            ShadowingMain.this.value; //access outer class field
        }
    }
}
```

- in this case, `int value = 3; //local variable` will have higest priority
- `outer class field` and `inner class field` are shadowed
- 👍🏻 better to use variables with different names

- ❓ How to access `inner class field`?
- `this.value;`

- ❓ How to access `outer class field`?
- `ShadowingMain.this.value;`

## 3️⃣ Local class

- not static
- `inner class` is instance of `outer class`
- `Inner class` ➕ **can access local variable**
- create class inside a `method` of `outer class`

- ✔️ **Example of local class**

- local class `LocalPrinter` is created inside `method process()` of `outer class`
- 🟢 can access `local class field`
- 🟢 can access `local variable` in `outer class method`
- 🟢 can access `parameter` in `outer class method`
- 🟢 can access `outer class` `instance field`

- create `local class instance` outside `outer class method`

```java
public class LocalOuterV1 {
    private int outInstanceValue = 3; //outer class instance field

    public void process(int parameter){ //outer class method process()

        int localValue = 1; //local variable

        class LocalPrinter{  //local class inside method process()
            int localClassValue = 0;

            public void printData(){
                localClassValue; //🟢 can access local class variable
                localValue; //🟢 can acess local variable in outer class method
                parameter; //🟢 can access parameter in outer class method
                outInstanceValue; // 🟢 can access outer class instance field
            }
        }

        LocalPrinter printer = new LocalPrinter(); //create local class instance
        printer.printData(); //call local class method
    }
}
```

## ✅ Local variable capture

- Life cycle of variable depends on the type of variable

- ✔️ **Types of variables**

|   Variable types    | Memory space |                     life cycle                      |
| :-----------------: | :----------: | :-------------------------------------------------: |
|  `Class variable`   |    method    |             longest, until program ends             |
| `Instance variable` |     heap     | until instance is not referennced and cleaned by GC |
|  `Local variable`   |    stack     |             shortest, when method ends              |

- `Local variable` life cycle is shorter than `Instance variable`
- However, `Instance` that was created by `local class` might have to access `Local variable`
- Thus, when `local class` creates `Instance`,
- ⭐️ JAVA makes a copy of `Local variable`
- ➡️ **Local variable capture**
- even if `Local variable` is removed from memory, `local class instance` can run its code

- `Local variable` is **copied** in the `local class instance`
- 🔴 thus, if the `local class instance` changes the value of `Local variable`, compile error
- ⭐️ `Local variable` that `local class` uses **SHOULD NOT BE** modified
- thus, `Local variable` should be **final**

```java
public class LocalOuterV1 {
    private int outInstanceValue = 3; //class variable

    public void process(int parameter){ //⚠️ local variable should be final

        final int localValue = 1; //⚠️ local variable, should be final

        class LocalPrinter{
            int localClassValue = 0;

            public void printData(){
                localClassValue;
                localValue; //🔴 cannot change value
                parameter; //🔴 cannot change value
                outInstanceValue;
            }
        }

        LocalPrinter printer = new LocalPrinter();
        printer.printData();
    }
}
```

## 4️⃣ Anonymous class

- type of `local class`
- `Inner class` ➕ class with no name
- 👍🏻 can **define and create** class at the same time
- ⭐️ must `extend` or `implement` a `class/interface`
- can be created ONLY ONCE

```java
// ✔️ local class
//declare class
    class LocalPrinter implements Printer{
        //body
    }
//create instance
    Printer printer = new LocalPrinter();

// ✔️ anonymous class
// declare and create class at the same time
    Printer printer = new Printer(){ //create class that implements Printer
        //body
    }
```

- ✔️ **before: static nested class**

```java
public class Ex1MainRef1 {

    static class Dice implements Process{ //static nested class
        @Override
        public void run() {
            Random random = new Random();
            int randomValue = random.nextInt(6) +1;
            System.out.println("randomValue = " + randomValue);
        }
    }

    static class Sum implements Process{ //static nested class
        @Override
        public void run() {
            for(int i = 0; i<3; i++){
                System.out.println("i = " + i);
            }
        }
    }

    public static void hello(Process process){ //method
        System.out.println("program start");
        process.run();
        System.out.println("program end");
    }

    public static void main(String[] args) { //main class
        hello(new Dice()); //call method
        hello(new Sum());
    }
}
```

- ✔️ **after: anonymous class**

```java
public class Ex1MainAnonymous {
    public static void hello(Process process){ //method
        System.out.println("program start");
        process.run();
        System.out.println("program end");
    }


    public static void main(String[] args) { //main class
        Process dice = new Process(){ //anonymous class
            @Override
            public void run() {
                Random random = new Random();
                int randomValue = random.nextInt(6) +1;
                System.out.println("randomValue = " + randomValue);
            }
        };


        Process sum = new Process(){ //anonymous class
            @Override
            public void run() {
                for(int i = 0; i<3; i++){
                    System.out.println("i = " + i);
                }
            }
        };

        hello(dice); //call method
        hello(sum);
    }
}
```

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅
