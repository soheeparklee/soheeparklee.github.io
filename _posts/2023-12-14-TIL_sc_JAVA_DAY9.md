---
title: 2023.DEC.14(THU) JAVA DAY 9_원, 사각형 넓이_extends
categories: [TIL(Today I Learned), SuperCoding_JAVA]
tags: [todayilearned, til, algorithm, extends]
---

## ✅ Daily Report

### 📌 **TO-DO LIST**

- [x] submit github blog post
- [x] lesson 34, 35
- [x] assigment: 원, 사각형 넓이\_extends
      <br>
      <br>

## ✅ 원과 사각형의 넓이 구하기

```java
public class Main {
    public static void main(String[] args) {
        Shape shape1 = new Circle("빨강", 4.0);
        Shape shape2 = new Rectangle("파랑", 3.0, 4.0);

        System.out.println("Shape1 면접 크키: " + shape1.getArea());
        System.out.println("Shape2 면접 크키: " + shape2.getArea());

        System.out.println("------------------------");

        if (shape1 instanceof Circle) {
            Circle circle = (Circle) shape1;
            circle.printCircleInfo();
        }

        System.out.println("------------------------");

        if (shape2 instanceof Rectangle) {
            Rectangle rectangle = (Rectangle) shape2;
            rectangle.printRectangleInfo();
        }
    }

}

//        Shape1 면접 크키: 50.24
//        Shape2 면접 크키: 12.0
//        ------------------------
//        도형의 색상: 빨강
//        도형의 면적: 50.24
//        원의 반지름: 4.0
//        ------------------------
//        도형의 색상: 파랑
//        도형의 면적: 12.0
//        사각형의 가로 길이: 3.0
//        사각형의 세로 길이: 4.0


public class Shape {
    protected String color;

    protected Shape(String color) {
        this.color = color;
    }

    public double getArea() {
        return 0.0;
    }

    protected void printInfo() {
        System.out.println("도형의 색상: " + color);
        System.out.println("도형의 면적: " + getArea());
    }
}

public class Circle extends Shape {
    private static final double PI = 3.14;
    private double radius;

    public Circle(String color, double radius) {
        super(color);
        this.radius = radius;
    }

    @Override
    public double getArea() {
        return radius * radius * PI;
    }

    public void printCircleInfo() {
        super.printInfo();
        System.out.println("원의 반지름: " + this.radius);
    }

}

public class Rectangle extends Shape{
    private double width;
    private double height;

    public Rectangle(String color, double width, double height) {
        super(color);
        this.width= width;
        this.height= height;
    }

    @Override
    public double getArea() {
        return width * height;
    }

    public void printRectangleInfo() {
        super.printInfo();
        System.out.println("사각형의 가로 길이: " + this.width);
        System.out.println("사각형의 세로 길이: " + this.height);
    }
}
```
