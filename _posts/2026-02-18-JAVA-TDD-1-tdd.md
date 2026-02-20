---
title: TDD, Display Name, BDD
categories: [JAVA, TDD]
tags: [] # TAG names should always be lowercase
---

## ✅ TDD

- red
- blue
- green

## 🔴

- first create the test code

```java
//test code
    @DisplayName("Calculate the total price of beverages in order")
    @Test
    void getTotalPrice() {
        //given
        CafeKiosk cafeKiosk = new CafeKiosk();
        Americano americano = new Americano();
        Latte latte = new Latte();
        cafeKiosk.add(americano);
        cafeKiosk.add(latte);

        //when
        int toalPrice = cafeKiosk.calculateTotalPrice();
        //then
        assertThat(toalPrice).isEqualTo(9000);
    }
```

- the production code will be set to minimum
- this test will fail, as in production code, it `returns 0`

```java
//production code
public int calculateTotalPrice() {
        return 0;
    }
```

## 🔵

- in fast, minimum time,
- create the minimum production code to make the code pass

```java
//production code
public int calculateTotalPrice() {
        return 9000;
    }
```

## 🟢

- create the production code that works
- while keeping the test code without modification

```java
//production code
    public int calculateTotalPrice() {
        int total = 0;
        for (Beverage beverage : beverages) {
            total += beverage.getPrice();
        }
        return total;
    }
```

- and refactor

```java
    public int calculateTotalPrice() {
        return beverages.stream()
                .mapToInt(Beverage::getPrice)
                .sum();
    }
```

## ✅ DisplayName

- use `@DisplayName` annotation to describe the method
- `Test to...` ❌
- write in sentences ⭕️
- also write the results `added to Orders`

```java
    @Test
    @DisplayName("Add one beverage. Beverage is added to Orders")
    void add() {
        CafeKiosk cafeKiosk = new CafeKiosk();
        cafeKiosk.add(new Americano());
        assertThat(cafeKiosk.getBeverages().size()).isEqualTo(1);
        assertThat(cafeKiosk.getBeverages()).hasSize(1);
        assertThat(cafeKiosk.getBeverages().get(0).getName()).isEqualTo("Americano");
    }

    @Test
    @DisplayName("Add everal beverage to Orders")
    void addSeveral() {
        CafeKiosk cafeKiosk = new CafeKiosk();
        Americano americano = new Americano();
        cafeKiosk.add(americano, 10);

        assertThat(cafeKiosk.getBeverages()).hasSize(10);
        assertThat(cafeKiosk.getBeverages().get(0).getName()).isEqualTo("Americano");
        assertThat(cafeKiosk.getBeverages().get(0)).isEqualTo(americano);
        assertThat(cafeKiosk.getBeverages().get(1)).isEqualTo(americano);
    }
```

```java
    @Test
    @DisplayName("Cannot create order before CAFE_OPEN_TIME and after CAFE_CLOSE_TIME")
    void createOrderOutsideCurrentTime() {
        CafeKiosk cafeKiosk = new CafeKiosk();
        Americano americano = new Americano();
        cafeKiosk.add(americano);

        assertThatThrownBy(()->cafeKiosk.createOrder(LocalDateTime.of(2026, 2, 16, 9, 59)))
                .isInstanceOf(IllegalStateException.class)
                .hasMessage("This is not order time. Inquire to manager");
    }
```

## ✅ BDD

> Behavior Driven Development

- not focus on method
- but focus on `scenario`, `Test Case(TC)`

- Given: context, situation before the action happens, `어떤 환경에서`
- When: the action `어떤 행동을 진행했을 때`
- Then: check outcome of action `어떤 상태 변화가 일어난다`

- TDD 🆚 BDD: BDD is based on TDD, focuses more on scenarios
