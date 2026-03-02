---
title: Business layer production code
categories: [JAVA, TDD]
tags: [] # TAG names should always be lowercase
---

## ✅ Business Layer

- `transaction` and `rollback`
- test code will be an integrated test
- as it will test how `business layer` and `persistence layer` interacts

## ✅ Business Logic

- (1) We add products to order
- (2) Need order entity
- (3) As product and order has `many to many` relationship, need orderProduct entity
- (4) We will create order with product numbers
- So we need `OrderCreateRequest` with productNumbers as List
- (5) When we create an order, we will return `OrderResponse`
- with `ProductResponse` as a List

- (6) Order controller
- (7) Order service
- to be able to write test code for `registeredDateTime`,
- it should be passed on as parameter when creating order
- we will recieve `OrderCreateRequest` and return `OrderResponse`

- when we find products from productRepository to create orders
- if product number is the same, we will only find one product
- but we can have several same products in one order
- like several latte in one order

- (8) order repository

## 📌 Test code for Service

- we are using `@SpringBootTest`
- this is NOT `transactional` ❌
- does not rollback
- so we need `tearDown()` method to clean the data after each test

```java
@ActiveProfiles("test")
@SpringBootTest
class OrderServiceTest {
    //all @Autowired

    //After each test, clean data
    //so that one test does not affect another
    @AfterEach
    void tearDown() {
        //productRepository.deleteAll();
        orderProductRepository.deleteAllInBatch();
        productRepository.deleteAllInBatch();
        orderRepository.deleteAllInBatch();
    }
```

- 🆚 In `@DataJpaTest`
- it has `@Transactional` ⭕️
- does rollback after each testt
- so no need for `tearDown()` method

```java
@DataJpaTest //faster than spring, only brings JPA libraries
@ActiveProfiles("test") //do not use data.sql for test

class ProductRepositoryTest {
    @Autowired
    private ProductRepository productRepository;
}
```

## 📌 Test code for order class

- this will be unit test, as we are testing for each method

## ☑️ Testing with HTTP

- to test GET, we used `h2-console` and the `api`
- to test POST, we can use `.http`

- run the application
- then run `.http` file

- `order.http`

```http
### create new order
POST localhost:8080/api/v1/orders/new
Content-Type: application/json

{
  "productNumbers": [
    "001", "002"
  ]
}
```

- `product.http`

```java
### get products with status
GET localhost:8080/api/v1/products/selling

```

#### 🔴 InvalidDefinitionException: Cannot construct instance of...

- this is because there is no constructor for request
- when making a POST request

- 🟢 Add constructor

```java
@Getter
@NoArgsConstructor
public class OrderCreateRequest {
    private List<String> productNumbers;

    @Builder
    public OrderCreateRequest(List<String> productNumbers) {
        this.productNumbers = productNumbers;
    }
}
```
