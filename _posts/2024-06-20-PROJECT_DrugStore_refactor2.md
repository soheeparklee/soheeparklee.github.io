---
title: Refactoring_Restful API URI
categories: [Project, Drug Store Project]
tags: [project, rest]
---

## ✅ Mid Feedback

In order for the API to be Representational of the State, it should follow some conditions. <br>
It should have a uniform interface. <br>
Thus, the URIs have to explain the resource. <br>

## 👎🏻 Before to 👍🏻 After

### ✔️ Auth

| 👎🏻 URI Before        | Method | 👍🏻 URI After     |
| -------------------- | ------ | ---------------- |
| auth/sign-up         | POST   | /auth/sign-up    |
| auth/login           | POST   | /auth/login      |
| auth/nickname-check  | GET    | /auth/nickname   |
| auth/email-check     | GET    | /auth/email      |
| auth/findEmail       | GET    | /auth/find-email |
| auth/change-password | PUT    | /auth/password   |
| email/send           | GET    | /email/send      |
| email/auth-num-check | GET    | /email/auth-num  |

### ✔️ Cart

| 👎🏻 URI Before | Method | 👍🏻 URI After |
| ------------- | ------ | ------------ |
| cart/myCart   | GET    | /cart        |
| cart/add      | POST   | /cart        |
| cart/update   | PUT    | /cart        |
| cart/delete   | DELETE | /cart        |
| cart/empty    | DELETE | /cart/empty  |

### ✔️ Likes

| 👎🏻 URI Before | Method | 👍🏻 URI After |
| ------------- | ------ | ------------ |
| likes         | POST   | /likes       |
| likes/deelte  | DELETE | /likes       |
| likes/mylikes | GET    | /likes       |

### ✔️ Main Page

| 👎🏻 URI Before | Method | 👍🏻 URI After   |
| ------------- | ------ | -------------- |
| /main         | GET    | /main          |
| main/category | GET    | /main/category |
| main/find     | GET    | /main/find     |

### ✔️ Detail

| 👎🏻 URI Before              | Method | 👍🏻 URI After                |
| -------------------------- | ------ | --------------------------- |
| product/detail             | GET    | /product                    |
| product/review/{productId} | POST   | /product/review/{productId} |
| product/question/list      | GET    | /product/question           |
| product/question           | POST   | /product/question           |
| product/answer             | POST   | product/answer              |
| product/question/del       | DELETE | /product/question           |
| product/question/update    | PUT    | /product/question           |

### ✔️ MyPage

| 👎🏻 URI Before        | Method | 👍🏻 URI After              |
| -------------------- | ------ | ------------------------- |
| mypage/review/add    | POST   | /mypage/review/{ordersId} |
| mypage/review/update | PUT    | /mypage/review/{ordersId} |
| mypage/review/delete | DELETE | /mypage/review/{ordersId} |
| mypage/product       | GET    | /mypage/order             |
| mypage/userInfo      | GET    | /mypage/userInfo          |
| mypage/question/get  | GET    | /mypage/question          |
| mypage/reviews       | GET    | /mypage/reviews           |
| mypage/coupon/get    | GET    | /mypage/coupon            |

### ✔️ Order

| 👎🏻 URI Before     | Method | 👍🏻 URI After         |
| ----------------- | ------ | -------------------- |
| order/cartToOrder | GET    | /order/cart-to-order |
| order/pay         | PUT    | /order/order-to-pay  |
| admin/addProduct  | POST   | /admin/product       |
