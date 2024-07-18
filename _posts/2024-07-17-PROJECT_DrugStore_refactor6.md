---
title: TroubleShooting_Too long to get main page
categories: [Project, Drug Store Project]
tags: [project, trouble]
---

## ✅ Takes too long to get main page

- In developer tools takes 3.83 seconds
  <img width="1470" alt="Screenshot 2024-07-11 at 23 22 13" src="https://github.com/user-attachments/assets/18faa6e6-d8f0-477b-87f4-c170469b2c88">

- In HTTPS postman 4s 25ms
  <img width="1054" alt="Screenshot 2024-07-11 at 23 23 07" src="https://github.com/user-attachments/assets/96d35dc3-8346-4a0a-9ba0-9288c26fe230">

- In Localhost postman takes more than 9 minutes!!!
  ![Screenshot 2024-07-17 at 23 11 01](https://github.com/user-attachments/assets/bd90db96-ab3d-4a18-a147-02572e383757)

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

- Developer tools
  <img width="363" alt="image" src="https://github.com/user-attachments/assets/6eadeeeb-4387-40a3-bc49-09d48052ee2c">

- Localhost Postman

  - 9mins ➡️ 2seconds

  <img width="969" alt="Screenshot 2024-07-17 at 23 16 58" src="https://github.com/user-attachments/assets/ac6dddb2-18f6-4503-bbf0-b58288511b1b">

- HTTPS Postman 3.55 seconds
  <img width="964" alt="Screenshot 2024-07-17 at 23 21 00" src="https://github.com/user-attachments/assets/8a50620a-4733-4864-8f63-e6cabafe64d2">

- HTTPS Developer tools 28ms
  <img width="1412" alt="Screenshot 2024-07-17 at 23 22 09" src="https://github.com/user-attachments/assets/60678b05-9fc8-4626-ae55-d101836d0521">
