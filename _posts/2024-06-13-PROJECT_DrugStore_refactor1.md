---
title: Refactoring_UUID to make unique order number
categories: [Project, Drug Store Project]
tags: [project, unique]
---

## ✅ Mid Feedback

Instead of using `Random` to make unique order number, why not use `UUID`?

## ✅ UUID

> Universally Unique Identifier <br>
> 128-bit long number in hex characters separated by “-“<br>

<br>
example: e58ed763-928c-4155-bee9-fdbaaadc15f3

## ✔️ Before

Cart to Order service<br>

```java

@Transactional
public ResponseDto cartToOrder(CustomUserDetails customUserDetails) {
            //...make order code

            //before implementing UUID
            LocalDate orderAt = LocalDate.now();
            Random random = new Random();
            Integer randomNumber = random.nextInt(10000);

            String ordersNumber = user.getUserId().toString() + orderAt.getYear() + ":" + randomNumber.toString();

            OrderResponseDto orderResponseDto = OrderResponseDto.builder()
                    .userName(user.getName())
                    .phoneNumber(user.getPhoneNumber())
                    .address(user.getAddress())
                    .ordersNumber(ordersNumber) //save here
                    .ordersAt(orderAt)
                    .orderCouponList(makeOrderCouponsList(user))
                    .orderProductList(makeOrderProductsList(cartList))
                    .build();

            return new ResponseDto(HttpStatus.OK.value(), "order page show success", orderResponseDto);
```

## 🔴 UUID was too long for my datatype

After changing the code as such, I got an 🔴Error🔴 saying <br>
`Data too long for column 'orders_number' at row 1`<br>

```java
            //UUID사용해서 고유한 주문번호 만들기
            String ordersNumber = UUID.randomUUID().toString();

```

## 👍🏻 After implementing shortened UUID

🔵 Used `substring` to make the UUID shorter <br>
👍🏻 No worries that the order numbers will not be unique<br>

```java
         //UUID사용해서 고유한 주문번호 만들기
            String ordersNumber = UUID.randomUUID().toString().replace("-", "").substring(0, 16);

```

<img width="415" alt="image" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/65bacfcb-5b33-407b-97de-621f61564aa3">
