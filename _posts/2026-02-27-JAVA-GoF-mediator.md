---
title: Behavioral_Mediator
categories: [JAVA, GoF]
tags: [] # TAG names should always be lowercase
---

## ✅ Mediator

- mediator object control how the objects interact
- objects communicate through mediator
- 👎🏻 before: objects communicate directly with each other, tight coupling

- 👍🏻 after
- components only know the mediator, not each other

```
Component A \
Component B ---> Mediator ---> Other components
Component C /
```

## ✅ Diagram

[![image.png](https://i.postimg.cc/fW6k8Rd4/image.png)](https://postimg.cc/Yjzp9k88)

## 👀 Send message

[![Screenshot-2026-03-08-at-20-47-40.png](https://i.postimg.cc/Dw4gtZjQ/Screenshot-2026-03-08-at-20-47-40.png)](https://postimg.cc/68wnZ9NT)

#### ✔️ Mediator Interface

```java
interface Mediator {
    void sendMessage(String message, Colleague colleague);
}
```

#### ✔️ Concrete Mediator

```java
class ChatMediator implements Mediator {

    private User1 user1; //should have concrete colleague as field
    private User2 user2;

    public void setUser1(User1 user1) {
        this.user1 = user1;
    }

    public void setUser2(User2 user2) {
        this.user2 = user2;
    }

    @Override
    public void sendMessage(String message, Colleague colleague) {
        if (colleague == user1) {
            user2.receive(message);
        } else {
            user1.receive(message);
        }
    }
}
```

#### ✔️ Abstract Colleague class(component)

- colleague does not have to know other colleagues
- only need to know the mediator

```java
abstract class Colleague {
    protected Mediator mediator; //now colleague knows only mediator

    public Colleague(Mediator mediator) {
        this.mediator = mediator;
    }
}
```

- objects that communicate through the mediator

#### ✔️ Concrete Colleage

```java
class User1 extends Colleague {

    public User1(Mediator mediator) {
        super(mediator);
    }

    public void send(String message) {
        mediator.sendMessage(message, this);
    }

    public void receive(String message) {
        System.out.println("User1 received: " + message);
    }
}

//also user2, user3, user4...
//they all communicate via Mediator
```

#### ✔️ Client

```java
public class Main {
    public static void main(String[] args) {

        ChatMediator mediator = new ChatMediator();

        User1 u1 = new User1(mediator);
        User2 u2 = new User2(mediator);

        mediator.setUser1(u1);
        mediator.setUser2(u2);

        u1.send("Hello from User1");
        u2.send("Hello from User2");
    }
}

//User2 received: Hello from User1
//User1 received: Hello from User2
```

## 👀 Air Traffic control

- flights do not communicate with each other directly
- they talk to the control tower
- control tower mediates the communicatation among flights

#### ✔️ Mediator Interface

- define how to communicate

```java
interface AirportMediator {
    boolean isRunwayAvailable(); //check if runway is available
    void setRunwayAvailability(boolean status); //change runway availability
}
```

#### ✔️ Concrete Mediator

- implement the coordination logic

```java
class AirportControlTower implements AirportMediator {
    private boolean isRunwayAvailable = true;

    //override
    public boolean isRunwayAvailable() {
        return isRunwayAvailable;
    }
    //override
    public void setRunwayAvailability(boolean status) {
        isRunwayAvailable = status;
    }
}
```

#### ✔️ Concrete Colleage

- objects that communicate through the mediator
- actual components

```java
class Flight {
    private AirportMediator mediator;
    private String flightNumber;

    public void land() {
        //check if runway is available and land
    }
}

class Runway {
    private AirportMediator mediator;

    public void clear() {
        //make runway available again
    }
}
```

#### ✔️ Client

```java
public class AirportSystem {
    public static void main(String[] args) {
        AirportMediator controlTower = new AirportControlTower(); //use airportControlerMediator

        Flight flight1 = new Flight(controlTower, "KE123");
        Flight flight2 = new Flight(controlTower, "OZ456");
        Runway runway = new Runway(controlTower);

        flight1.land();
        flight2.land();
        runway.clear();
        flight2.land();
    }
}
```

## 🛠️

- when order is created, talk to email, inventory, analytics

```
OrderService  ----> EventPublisher (Mediator)  ----> EmailService
                                               ----> InventoryService
                                               ----> AnalyticsService
```

## 👍🏻

- lose coupling
- easier maintenance
