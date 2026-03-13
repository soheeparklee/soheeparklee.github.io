---
title: Behavioral_Strategy Pattern
categories: [JAVA, GoF]
tags: [] # TAG names should always be lowercase
---

## ✅ Strategy Pattern

- make a lot of algorithms
- encapsulate them
- and make them interchangeable at runtime, 갈아끼우기
- client will use the common interface only
- actual behavior can vary according to the selected strategy
- 👍🏻 algorithm is independent from the client that uses it
- 👍🏻 no need to use `if/else`, `switch`

## ✅ Diagram

[![Screenshot-2026-03-06-at-17-52-06.png](https://i.postimg.cc/yxc91pt2/Screenshot-2026-03-06-at-17-52-06.png)](https://postimg.cc/8fksw41b)

## 👀

#### 👎🏻 before

```java
if(paymentType.equals("PAYPAL")) { ... }
else if(paymentType.equals("CARD")) { ... }
else if(paymentType.equals("CRYPTO")) { ... }
```

#### ✔️ Strategy interface

```java
public interface PaymentStrategy {
    void pay(double amount);
}
```

#### ✔️ Concrete strategies

- card payment method
- paypal payment method

```java
public class CreditCardPayment implements PaymentStrategy {

    @Override
    public void pay(double amount) {
        //pay w credit card
    }
}

public class PaypalPayment implements PaymentStrategy {

    @Override
    public void pay(double amount) {
        //pay w paypal
    }
}
```

#### ✔️ Context

- has `strategy interface` as field

```java
public class PaymentService {

    private PaymentStrategy paymentStrategy;

    public PaymentService(PaymentStrategy paymentStrategy) { //interchange, 갈아끼우기 method
        this.paymentStrategy = paymentStrategy;
    }

    public void processPayment(double amount) {
        paymentStrategy.pay(amount);
    }
}
```

#### ✔️ Client

```java
public class Main {

    public static void main(String[] args) {

        PaymentService service1 = new PaymentService( new CreditCardPayment()); //use card payment method
        service1.processPayment(100);

        PaymentService service2 = new PaymentService( new PaypalPayment()); //use paypal method
        service2.processPayment(100);
    }
}
```

## 🛠️

- used for Dependency injections
