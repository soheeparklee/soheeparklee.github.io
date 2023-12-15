---
title: 2023.DEC.15(FRI) JAVA DAY 10_원, 사각형 넓이, 둘레_abstract
categories: [TIL(Today I Learned), SuperCoding_JAVA]
tags: [todayilearned, til, algorithm, abstract]
---

## ✅ Daily Report

### 📌 **TO-DO LIST**

- [x] submit github blog post
- [x] lesson 36, 37, 38
- [x] assigment:
      <br>
      <br>

## ✅ 원과 사각형의 abstract 사용해 넓이 구하기

```java

public class Main {
    public static void main(String[] args) {
        // Circle 객체 생성
        Circle circle = new Circle(5.0);
        System.out.println("기본 원 색상: " + circle.getColor());
        System.out.println("기본 원 차원: " + circle.getDimension());
        circle.setColor("빨강");  // 도형의 색상 설정

        // Circle 객체 정보 출력
        System.out.println("원 반지름: " + circle.getRadius());
        System.out.println("원 지름: " + circle.calculateDiameter());
        System.out.println("원 둘레: " + circle.calculatePerimeter());
        System.out.println("원 면적: " + circle.calculateArea());
        System.out.println("원 색상: " + circle.getColor());

        System.out.println("---------------------------------------------");

        // Rectangle 객체 생성
        Rectangle rectangle = new Rectangle(4.0, 6.0);
        System.out.println("기본 직사각형 색상: " + rectangle.getColor());
        System.out.println("기본 직사각형 차원: " + rectangle.getDimension());

        rectangle.setColor("파랑");  // 도형의 색상 설정


        // Rectangle 객체 정보 출력
        System.out.println("직사각형 가로 길이: " + rectangle.getWidth());
        System.out.println("직사각형 세로 길이: " + rectangle.getHeight());
        System.out.println("직사각형 대각선 길이: " + rectangle.calculateDiagonal());
        System.out.println("직사각형 면적: " + rectangle.calculateArea());
        System.out.println("직사각형 둘레길이: " + rectangle.calculatePerimeter());
        System.out.println("직사각형 색상: " + rectangle.getColor());
    }

//[예상 출력]
//
//    기본 원 색상: 기본색
//    기본 원 차원: 2
//    원 반지름: 5.0
//    원 지름: 10.0
//    원 둘레: 31.41592653589793
//    원 면적: 78.53981633974483
//    원 색상: 빨강
//---------------------------------------------
//    기본 직사각형 색상: 기본색
//    기본 직사각형 차원: 2
//    직사각형 가로 길이: 4.0
//    직사각형 세로 길이: 6.0
//    직사각형 대각선 길이: 7.211102550927978
//    직사각형 면적: 24.0
//    직사각형 둘레길이: 20.0
//    직사각형 색상: 파랑
}
//abstact class Shape
public abstract class Shape {
      //💡 static 아니라는 것 확인
    protected int dimension;
    protected String color;

    public abstract double calculateArea();
    public abstract double  calculatePerimeter();

    public  String getColor() {
        return color;
    }

    public void setColor(String color) {
        this.color = color;
    }

    public int getDimension() {
        return dimension;
    }

    public Shape(int dimension, String color) {
        this.dimension = dimension;
        this.color = color;
    }
}


public class Circle extends Shape{

    private double radius;
    private static double PI= 3.14;
//⭐️ override 할 때는 public, parameter 모두 부모랑 똑같아야 한다
    @Override
    public double calculateArea() {
        return radius * radius * PI;
    }

    @Override
    public double calculatePerimeter() {
        return radius * 2 * PI;
    }

    public double calculateDiameter(){
        return radius *2;
    }

    public double getRadius() {
        return radius;
    }

//부모의 field받아올 때는 super
    public Circle(double radius) {
        super(2, "기본색");
        this.radius = radius;
    }

}

public class Rectangle extends Shape{

    private double width;
    private double height;


    @Override
    public double calculateArea() {

        return width * height;
    }

    @Override
    public double calculatePerimeter() {
        return (width + height)*2;
    }

    public double getWidth() {
        return width;
    }

    public double getHeight() {
        return height;
    }
//pow: 제곱 sqrt: 제곱근
    public double calculateDiagonal(){
        double heightPow=Math.pow(height, 2);
        double widthPow= Math.pow(width,2);
        return Math.sqrt(heightPow + widthPow);
    }

    public Rectangle(double width, double height) {
        super(2, "기본색");
        this.width = width;
        this.height = height;
    }
}


```
