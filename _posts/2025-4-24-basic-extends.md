---
title: Extends, Overriding
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ Extends

- if `extends`, extends the field and method of parent class

```java
public class Car {
    public void move(){}
}

public class GasCar extends Car{
    public void fillGas(){}

}

public class ElectricCar extends Car{
    public void charge(){}

}

public class CarMain {
    public static void main(String[] args) {
    ElectricCar electricCar = new ElectricCar()
    electricCar.charge();
    electricCar.move(); //electricCar can move(parent car class)
    }
}
```

- 👍🏻 if I want to add `openDoor()` to all cars, just add to `Car` class
  - as both `GasCar` and `ElectricCar` extends `Cars`, can easily add field, methods
- 👍🏻 save code repetition
  - `move()` can be called both in `GasCar`, `ElectricCar`

## ✅ Extends and memory

- 1️⃣ when `child class extending a parent class` is created, in memory, **both** child and parent class is made
- `Electric car` class `extends` the `Car class`
- when `ElectricCar electricCar = newElectricCar();`
- in memory, it looks like this

<img width="500" alt="Image" src="https://github.com/user-attachments/assets/38f89575-56f2-4528-b813-bae26a65c51c" />

- When `method` is called
- 2️⃣ first find in created `instance type`
  - if `ElectricCar electricCar = new ElectricCar();`, look in `ElectricCar`
- 3️⃣ if `method` does not exist,
- look in `extends parent type`, look in `Car`
- if `method` does not exist in any parent, compile error

```java
public class Car {
    public void move(){}
}

public class ElectricCar extends Car{
    public void charge(){}

}

public class CarMain {
    public static void main(String[] args) {
    ElectricCar electricCar = new ElectricCar();
    electricCar.charge();
    electricCar.move();
    }
}
```

- ✔️ call method `electricCar.charge();`
- in `ElectricCar electricCar = new ElectricCar();`, there is both `Car` and `Electric car`
- `ElectricCar`갔더니 `Car`도 있고 `Electric car`도 있음
- look in `ElectricCar` first
- bc `electricCar` type is `ElectricCar`, find `ElectricCar` first
- 아 나는 `electricCar` 타입이네. `electricCar` 먼저 찾음

- ✔️ call method `electricCar.move();`
- look in `ElectricCar` first
- 나는 `electricCar` type이니까 `electricCar`먼저 찾았는데, `move()`없음
- method `move()` does not exist
- look in `Car`(parent class) next
- 그러면 부모 클래스 `Car`찾음

## ✅ Extends and overriding

- child class can `override` parent class method and **recreate** a new method

```java
public class Car { //parent
    public void move(){}
}

public class ElectricCar extends Car { //child
    @Override
    public void move(){} //override
}
```

<img width="492" alt="Image" src="https://private-user-images.githubusercontent.com/97790983/437099195-62f80907-2970-4514-b466-d417cde63b0a.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDc4NjEzMDMsIm5iZiI6MTc0Nzg2MTAwMywicGF0aCI6Ii85Nzc5MDk4My80MzcwOTkxOTUtNjJmODA5MDctMjk3MC00NTE0LWI0NjYtZDQxN2NkZTYzYjBhLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA1MjElMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwNTIxVDIwNTY0M1omWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTZkMDZiODc5YjYzZGYyOTkyYWQyZTFlYWQ0N2Q0MjBkMzE3ZmExMDY4MjM0OWI2ZjZkNzk5ZDNmOGJjNWZmMGMmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.sLm8GMsvnn-VbnThA48MWmHEHlkfja7aVgyxGJ5vMqc" />

- ✔️ call method `electricCar.move();`
- `electricCar` type is `ElectricCar`, find `ElectricCar` first
- there is `move()` in `ElectricCar`
- does not find parent class for `move()`
- ⭐️ 자식 클래스에서 `field/method` 찾았으니까 부모 클래스까지 찾지 않음
- ❓ `field/method` 이름이 같아도 부모 클래스 참조하고 싶으면? ➡️ `super`

## Overriding 🆚 Overloading

- Overloading: create several method with **same method name, different parameter**
- Overriding: in `extends` relationship, child class **recreates** parent method

## ✅ Overriding conditions

- same method name
- same parameter
- same return value
- broader access modifier
- `static` ❌ : method overriding takes place in `heap` area of memory
  - `static` is in `method` area of memory
- `final` ❌ : final means method cannot be altered, thus cannot override
- `private` ❌ : private means only accessible in same class, cannot be accessed in child class
- constuctor is not overrideable

## ✅ Overriding and protected

- `public`
- `protected`: same package, allow `extends` in different package
- `default`: same package
- `private`: same class

- Parent `private field and method` can **NOT** be used by child
- Parent `defaut field and method` can be used only if parent and child are in **same** package
- Parent `protected field and method` can be used even if parent and child are in **different** package

- If `parent and child` are in different package...

```java
public class Parent {
    public int publicValue;
    protected int protectedValue;
    int defaultValue;
    private int privateValue;
}

public class Child extends Parent{
    publicValue = 1;
    protectedValue = 2; //even if different package, extends can use protected field
    //defaultValue //only same package
    //privateValue
}
```

## ✅ Super

- when child class `@Override` parent class, child `field/method` will be used
- however, if child class wants to use parent class `field/method`, use `super`
- **super**: in same `field/method` name of child/parent class, use parent class

```java
public class Parent {
    public String value = "parent"; //same field name

    public void hello(){} //same method name
}
```

```java
public class Child extends Parent{ //extends parent
    public String value = "child"; //same field name

    @Override
    public void hello(){} //same method name ➡️ override

    public void call(){
        System.out.println("this.value= " + this.value); //find in my class(child)
        System.out.println("super.value= " + super.value); //✔️ find in parent

        this.hello(); //find in my class(child)
        super.hello(); //✔️ find in parent
    }
}
```

## ✅ Super and Constructor

- when create `child instance`, both `child instance` and `parent instance` is created
- in `child constructor`, calls `parent constructor` with `super`
- ⭐️ order: `parent` ➡️ `child`
  - `classA`
  - `classB extends classA`
  - `classC extends classB`
  - order: `classA` ➡️ `classB` ➡️ `classC`
  - 결론: 상속 클래스의 경우 자식만 생성해도 항상 부모가 생성되는데, 순서는 **부모가 먼저** 생성이 되고, 자식이 생성된다.

```java
public class ClassA {
    public ClassA() { //classA constructor //3️⃣
        System.out.println("class A constructor"); //4️⃣
    }
}

public class ClassB extends ClassA{
    public ClassB(int a, int b){ //classB constructor
        super(); //call parent classA constructor //2️⃣
        System.out.println("Class B constructor a= " + a + " b= "+ b); //5️⃣
    }
}

public class ClassC extends ClassB{
    public ClassC(int a, int b) { //classC constructor
        super(a, b); //call parent classB constructor //1️⃣
        System.out.println("Class c constructor"); //6️⃣
    }
}
```

- ✔️ Result

```
class A constructor
Class B constructor a= 7 b= 1
Class c constructor
```

## ✅
