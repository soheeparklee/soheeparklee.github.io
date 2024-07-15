---
title: TroubleShooting_Too long to get main page
categories: [Project, Drug Store Project]
tags: [project, trouble]
---

## ✅ Takes too long to get main page

- In developer tools takes more than 3 seconds
  <img width="1470" alt="Screenshot 2024-07-11 at 23 22 13" src="https://github.com/user-attachments/assets/18faa6e6-d8f0-477b-87f4-c170469b2c88">

- In postman takes more than 4 seconds
  <img width="1054" alt="Screenshot 2024-07-11 at 23 23 07" src="https://github.com/user-attachments/assets/49a17198-51df-4094-9357-3486416bec70">

## 🔵 Tryout 1. Move update code to each service.

First, the `update` code was inside the `for loop`.
Thus, making the update for each product each time calling a product.
This was considered to be so inefficient.
Moved the update code outside the `for loop`.

### 👎🏻 Before

```java
  public List<productListQueryDto> getProductListQueryDto(List<Product> productList) {
        List<productListQueryDto> plqdList = new ArrayList<>();

        for (Product product : productList) {

            productRepository.updateProductSales(); //🔴
            productRepository.updateReviewAvg(); //🔴
            int productLike=productRepository.countLikesByProductId(product.getProductId());
            productListQueryDto plqd = productListQueryDto.builder()
                    .product_id(product.getProductId())
        }
```

### 👍🏻 After

```java
 public List<productListQueryDto> getProductListQueryDto(List<Product> productList) {
        List<productListQueryDto> plqdList = new ArrayList<>();
        productRepository.updateProductSales(); //🔵outside for loop
        productRepository.updateReviewAvg();

        for (Product product : productList) {
            int productLike=productRepository.countLikesByProductId(product.getProductId());
            productListQueryDto plqd = productListQueryDto.builder()
                    .product_id(product.getProductId())

        }
      }
```

### 🟢 Result

Just by doing this, the time for loading main page reduced from 3 seconds to 1.

<img width="363" alt="image" src="https://github.com/user-attachments/assets/6eadeeeb-4387-40a3-bc49-09d48052ee2c">
