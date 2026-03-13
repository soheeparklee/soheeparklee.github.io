---
title: Creational_Factory
categories: [JAVA, GoF]
tags: [] # TAG names should always be lowercase
---

- Loose coupling
- OC principle
- `default` in interface

## 🛠️ When to use factory

- When you want to create several **types** of smth with different values
- give the creation role to a factory
- 👀 You have class `Circle` and `Square` extending `Interface Shape`
- you want to create `Circle` or `Square` using one constructor
- 👀 You have class `WhiteShip` and `BlackShip` extending `Ship`
- you want to create `WhiteShip` and `BlackShip` just with one method, without using `else-if` for checking the names and settings colors...

## ✅ Factory Pattern

- factory안에서 구체적인 클래스를 만들어낸다
- ⭐️ **Loosely coupled: make coupling between class and constructor loose**
- `<<Interface>>` will be responsible for constructing a class
- delegate object creation to a factory
- ⭐️ **Open/Closed principle**: open to extension, closed to modification

## 👎🏻 If there was no factory pattern

- ✔️ **Class `Ship`**

```java
public class Ship {
    private String name;
    private String color;
    private String logo;

  //getters
  //setters
}
```

- ✔️ **Class `ShipFactory`**
- 👎🏻 need to check name and set logo and color accordingly

```java
        // Customizing for specific name
        if (name.equalsIgnoreCase("whiteship")) {
            ship.setLogo("\uD83D\uDEE5️");
        } else if (name.equalsIgnoreCase("blackship")) {
            ship.setLogo("⚓");
        }

        // coloring
        if (name.equalsIgnoreCase("whiteship")) {
            ship.setColor("whiteship");
        } else if (name.equalsIgnoreCase("blackship")) {
            ship.setColor("black");
        }
```

## ✅ After factory pattern

[![Screenshot-2026-02-19-at-15-45-43.png](https://i.postimg.cc/fWjdk0d4/Screenshot-2026-02-19-at-15-45-43.png)](https://postimg.cc/5jyyRypp)

- ✔️ **Class `Ship`**

```java
public class Ship {
    private String name;
    private String color;
    private String logo;

  //getters
  //setters
}
```

- ✔️ **Class `WhiteShip` and `BlackShip`**
- ⭐️ How to set attributes of parent without using constructor

```java
public class WhiteShip extends Ship {
    public WhiteShip() {
        setName("White Ship");
        setLogo("aaa");
        setColor("white");
    }
}
```

```java
public class BlackShip extends Ship{
    public BlackShip() {
        setName("BlackShip");
        setLogo("bbbb");
        setColor("black");
    }
}
```

- ✔️ **Interface ShipFactory**

```java
public interface ShipFactory {
  //default, could/could not be overrided
    default Ship orderShip(String name, String email){
        validate(name, email);
        Ship ship = createShip(); //use createShip();
        sendEmailTo(email, ship);
        return ship;
    }

    Ship createShip(); //not defined, must be overrided

}
```

- `validate()`, `sendEmailTo()` are methods I want to run as soon as I create Ship

- ✔️ **Class WhiteShipFactory and BlackShipFactory**

```java
public class WhiteShipFactory implements ShipFactory{
    @Override
    public Ship createShip() {
        return new WhiteShip();
    }
}
```

```java
public class BlackShipFactory implements ShipFactory{
    @Override
    public Ship createShip() {
        return new BlackShip();
    }
}
```

- ✔️ **CLient code**

```java
public class Client {
    public static void main(String[] args) {
        Ship whiteShip = new WhiteShipFactory().orderShip("WhiteShip", "aaa@gmail.com");
        Ship blackShip = new BlackShipFactory().orderShip("BlackShip", "bbb@gmail.com");
    }
}
```

## 👍🏻 Advantages 👎🏻 Disadvantages

- 👍🏻 do not need to use else-if
- 👍🏻 open/closed principle: open for extension, closed for modification
  - can create another function/interface without modifying the old code
  - this is bc of coupling between class and constructor is loose
- 👍🏻 can use `default` to write a default method in `interface`

- 👎🏻 need to create more classes

## default and private in interface

- can use `default` to define a method in `interface`
- and the helper methods for the `default method` should be `private`
- as it would be used only inside the interface

```java
public interface ShipFactory {
    default Ship orderShip(String name, String email){
        validate(name, email);
        prepareFor(name);
        Ship ship = createShip();
        sendEmailTo(email, ship);
        return ship;
    }

  //helper methods inside default method
  //access modifier: private
  private void validate(String name, String email){

    }

    private void prepareFor(String name) {

    }


```

## 👀

[![Screenshot-2026-03-08-at-10-04-25.png](https://i.postimg.cc/0NrGb6kh/Screenshot-2026-03-08-at-10-04-25.png)](https://postimg.cc/d7PZfVT9)

#### ✔️ Product interface

```java
public interface Car {
    //method that car can perform
    drive();
}
```

#### ✔️ Abstract product

```java
public abstract class AbstractCar implements Car {
    protected String color;
    protected double price;

    //constructor to use in concrete products
    public AbstractCar(String color, double price) {
        this.color = color;
        this.price = price;
    }
}
```

#### ✔️ Concete products

```java
public class Mercedes extends AbstractCar {

    public Mercedes(String color) {
        super(color, 55000);
    }

    @Override
    public void drive() {
    }
}

public class Kia extends AbstractCar {

    public Kia(String color) {
        super(color, 30000);
    }

    @Override
    public void drive() {
    }
}
```

#### ✔️ Factory Interface

```java
public interface CarFactory {

    Car createCar(String color);

}
```

#### ✔️ Conrete Factory

```java
public class MercedesFactory implements CarFactory {

    @Override
    public Car createCar(String color) {
        return new Mercedes(color);
    }
}

public class KiaFactory implements CarFactory {

    @Override
    public Car createCar(String color) {
        return new Kia(color);
    }
}
```

#### ✔️ Client

```java
Car blackMercedes = new MercedesFactory.createCar("black");

Car whiteKia = new KiaFactory.createCar("white");
```
