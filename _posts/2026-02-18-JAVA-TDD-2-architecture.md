---
title: Layered Architecutre and Integration Test in Spring and JPA
categories: [JAVA, TDD]
tags: [] # TAG names should always be lowercase
---

## ✅ Layered Architecutre in Spring

- ❓ why use layered architecture?
- separation of concerns
- to organize code by responsitbility

- Presentation Layer `Controller`: handles HTTP request & response
- Business Layer `Service` : business logic
- Persistence Layer `Repository, Data access`: access DB

- Controller 👉🏻 Service 👉🏻 Repository 👉🏻 Database

## ✅ Integration test

- 👎🏻 Unit test is limited to testing a single class in isolation
- In real life, several modules cooperate
- 👉🏻 check how multiple parts of the system interact together

## ✅ Spring basic concepts

#### ✔️ Spring Bean

- object that is created, managed, and stored inside the Spring IoC container

- ❌ **This is not a Spring bean**

```java
UserService service = new UserService();

// I created it
// I manage it
// I control the life cycle
```

- ⭕️ **Yes, this is a Spring bean**

```java
@Service
public class UserService {
}

// Spring creates it
// Spring injects it
// Spring controls its life cycle
```

- Beans are sotred in `Spring IoC Container`, called `Application Context`

- 🧰 **How to make a Spring bean**
- 1️⃣ with annotations

```java
@Component
@Service
@Repository
@Controller
@RestController
```

- 2️⃣ Using `@Bean` in configuration class

```java
@Configuration
public class AppConfig {

    @Bean
    public UserService userService() {
        return new UserService();
    }
}
```

- now `UserService` is also a bean

#### ✔️ Inversion of Control IoC

- **Spring control objects**
- control of creating and managing objects is transferred from your code to the Spring container
- Spring creates and manages the object for you

- 👀 Manager assign task instead of chef choosing work

- 👎🏻 **Before**

```java
public class UserController {
    private UserService service = new UserService();
}
```

- `UserController` controls the creation of the `UserService`
- 👎🏻 tight coupling

- 👍🏻 **After**

```java
//step 1. make UserService into a Spring Bean
@Service
public class UserService {
}

//step 2. Inject it using DI, constructor injection
@RestController
public class UserController {

    private final UserService service;

    public UserController(UserService service) {
        this.service = service;
    }
}
```

- Now, Spring creates object `UserService`
- Spring also creates `UserController`
- Then, Spring injects `UserService` into `UserController`

- Manages lifecycle
- Injects dependencies
- Handles configuration
- 👉🏻 Done by Spring IoC Container

#### ✔️ Dependency Injection DI

- mechanism Spring uses to implement IoC
- create dependency inside class ❌
- inject dependency from outside ⭕️
- 👍🏻 loose coupling

- 👀 Manager gives ingredients to chef, instead of the chef buying them

- **Types of DI**
- constructor injection
- setter injection
- field injection(not recommended)

- 👎🏻 **Before**

```java
public class OrderService {

    private PaymentService paymentService = new PaymentService();

    public void placeOrder() {
        paymentService.processPayment();
    }
}
```

- `OrderService` directly creates `PaymentService`
- have to change the whole code if `PaymentService` changes

- 👍🏻 **After**

```java
//step 1. create interface
public interface PaymentService {
    void processPayment();
}
//step 2. create implementations
@Service
public class CreditCardPaymentService implements PaymentService {

    @Override
    public void processPayment() {
        System.out.println("Processing credit card payment");
    }
}

@Service
public class PayPalPaymentService implements PaymentService {

    @Override
    public void processPayment() {
        System.out.println("Processing PayPal payment");
    }
}

//step 3. inject dependency via constructor
@Service
public class OrderService {

    private final PaymentService paymentService;

    public OrderService(PaymentService paymentService) {
        this.paymentService = paymentService;
    }

    public void placeOrder() {
        paymentService.processPayment();
    }
}
// what order service needs is paying
// does not have to know what kind of payment, paypal or credit card
```

- Spring creates all beans
- Finds a class that implements `PaymentService`
- Injects it into `OrderService`
- Manages lifecycle automatically

#### ✔️ Aspect Oriented Programming AOP

- add extra behavior without changing business logic
- separate cross-cutting concerns from business logic
- **cross-cutting concerns**

  - logging
  - security
  - transactions
  - caching
  - exception handling

- 👀 CCTV, billing, cleaning - applied everywhere automatically without changing cooking recipie

## ✅ Object Relational Mapping

- ORM allows you to **map** `Java objects ↔ Database tables`

- Object oriended(`objects`, `fields`, `methods`) and Relational DB(`tables`, `rows`, `columns`) are different paradigms
- 👎🏻 **Before**:
- after developing, the devloper had to map all OOP data into DB
- code using pure JDBC

```java
Connection conn = DriverManager.getConnection(...);
PreparedStatement ps = conn.prepareStatement(
    "SELECT * FROM users WHERE id = ?");
ps.setLong(1, 1L);

ResultSet rs = ps.executeQuery();

User user = new User();
user.setId(rs.getLong("id"));
user.setName(rs.getString("name"));
```

- 👍🏻 **After**:
- ORM acts as a bridge between them

```java
@Entity
public class User {

    @Id
    private Long id;

    private String name;
}
```

## ✅ Java Persistence API

- specification (rules/interface/standard) for ORM in Java
- **JPA defines**:

  - How Java objects should be mapped to database tables
  - How persistence should work
  - Standard APIs for CRUD operations

- **JPA**: rules(interface)
- **Hibernate**: implementation of the rules
- JPA can plug in other implementation(that are not Hibernate)and your JPA code still works
- normally JPA implements Hibernate

```java
//step 1. ORM mapping
@Entity
public class User {

    @Id
    @GeneratedValue
    private Long id;

    private String name;
}
//step 2. implement JPA
public interface UserRepository extends JpaRepository<User, Long> {
}
//step 3. use JPA APIs for CRUD operations
userRepository.save(user);
userRepository.findById(1L);
```

- Important JPA concepts

```java
@Entity
@Id
@Column

@ManyToOne, @OneToMany
@OneToOne, @ManyToMany
```
