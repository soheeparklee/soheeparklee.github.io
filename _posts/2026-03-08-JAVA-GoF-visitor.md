---
title: Behavioral_Visitor
categories: [JAVA, GoF]
tags: [] # TAG names should always be lowercase
---

## ✅ Visitor Pattern

- add new operations to existing object structures
- without modifying those classes
- 👉🏻 separate algorithms(operations) from the objects on which they operate

- 👀 Shapes such as `circle` and `rectangle` has `calculatePermiteter()` method
- I want to add `calculateArea()` without chaning `circle` and `rectangle`

## ✅ Diagram

[![Screenshot-2026-03-08-at-23-11-15.png](https://i.postimg.cc/fbJ6qX1w/Screenshot-2026-03-08-at-23-11-15.png)](https://postimg.cc/xkVxck07)

## 👎🏻 before

- `circle` and `rectangle` has their own operations

```java
class Circle{
  calculatePermiteter();
}

class Rectangle{
  calculatePermiteter();
}
```

- 👎🏻 If I want to add `calculateArea()`, I need to change the code for both classes
- 👎🏻 violate open/closed principle

## 👍🏻 after

- `calculatePermiteter()` is not inside `Circle` nor `Rectangle`
- objects only accept visitors
- and the visitors will perform the operation

#### ✔️ Element

- now elements only accept visitor

```java
interface Shape {
    void accept(Visitor visitor);
}
```

#### ✔️ Concrete Element

- `circle` and `rectangle` do NOT how to `calculateParameter()` ❌
- only knows how to accept visitor

```java
class Circle implements Shape {

    double radius;

    @Override
    public void accept(Visitor visitor) {
        visitor.visit(this);
    }
}

class Rectangle implements Shape {
    double width, height;

    @Override
    public void accept(Visitor visitor) {
        visitor.visit(this);
    }
}
```

#### ✔️ Visitor

```java
// Visitor interface
interface Visitor {
    void visit(Circle circle);
    void visit(Rectangle rectangle);
}
```

#### ✔️ Concrete visitor

- visitor will do all the work of `calculateParameter()`
- as `PerimeterVisitor`

```java
class PerimeterVisitor implements Visitor {
    @Override
    public void visit(Circle circle) {
        //define how to get perimeter for circle
    }

    @Override
    public void visit(Rectangle rectangle) {
        //define how to get perimeter for rectangle
    }
}
```

#### 💡 Add more functions

- now if I want to **add operation** `calculateArea()`
- I can just create a new visitor
- 👍🏻 do not have to change `circle` code

```java
class AreaVisitor implements Visitor {
    @Override
    public void visit(Circle circle) {
        //calculate circle area
    }

    @Override
    public void visit(Rectangle rectangle) {
        //calculate rectangle area
    }
}
```

#### 💡 Add more shapes

- now if I want to **add Element** like `triangle`,
- create `triangle` class and make it accept() visitor
- and create visitor for triangle

```java
class Triangle implements Shape {
    @Override
    public void accept(Visitor visitor) {
        visitor.visit(this);
    }
}
```

```java
class PerimeterVisitor implements Visitor {
    @Override
    public void visit(Circle circle) {}
    @Override
    public void visit(Rectangle rectangle) {}
    @Override
    public void visit(Triangle triangle) {
      //define how to calculate perimeter for triangle
    }
}
```

#### ✔️ Client

```java
public class Main {
    public static void main(String[] args) {
        Shape circle = new Circle(5);
        Shape rectangle = new Rectangle(4, 6);

        Visitor areaVisitor = new AreaVisitor();
        Visitor perimeterVisitor = new PerimeterVisitor();

        circle.accept(areaVisitor); //calculate circle area
        rectangle.accept(areaVisitor);

        circle.accept(perimeterVisitor); //calculate circle perimeter
        rectangle.accept(perimeterVisitor);
    }
}
```

## 🛠️
- class structure은 stable하게 잡혔는데
- 계속 새로운 operation을 추가하고 싶을 때
- used for file system
- for calculating file size, compression
