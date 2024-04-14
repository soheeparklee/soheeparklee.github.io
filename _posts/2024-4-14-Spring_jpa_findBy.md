---
title: JPA_findByCategory/keyword
categories: [JAVA, Spring]
tags: [jpa] # TAG names should always be lowercase
---

## ✅ 조건(카테고리, 키워드)이 있도록 JPA에서 찾아올 떄

![코딩공책-32](https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/5b36c3c9-5de6-4a67-b225-c07347114723)

### 1. 먼저, 내가 가져오려는 값이 1개의 테이블에서 가져오는지, 여러개의 테이블에서 필요한지 파악하기

1. 1개의 테이블에서만 정보 가져오기 필요하다면: `findBy`하고 끝 <br>
2. 여러개의 테이블에서 정보 조금씩 필요: <br>
   1. JPQL에서 `JOIN TABLE`하거나 <br>
   2. service에서 각 테이블에서 각 JPA로 받아온 다음 합친다. 💡 4번 예시 참고 <br>

### 2. 조건이 있는가? 특정 카테고리를 찾고 싶다거나, 특정 키워드를 찾고 싶다거나

1. JPQL에서 WHERE문으로 조건 처리 <br>
2. 일단 JPA에서 findAll로 모든 아이템들을 받아온 후, `stream().filter()`로 조건을 찾는다. <br>

### 3. JPA에서 받아온 response와 내가 return하고 싶은 response가 DTO가 같은가?

1. 같다면 바로 위에서 조건 찾은 다음 `toList()` 하고 `return` <br>
2. 다르면`map(()-> new 내가 만들고 싶은 DTO)` <br>

### 💡 결론

- 여러개의 테이블에서 조인해야하는데, 찾고 싶은 조건들도 있다면 그냥 편하게 JPA로 처리한다.<br>
- 이미 `findAll`이 있고, 조건 하나만 간단히 추가하고 `return`하는 형식이 같다면 그냥 `findAll`쓰고 `service`에서 조건만 처리한다.

## ✔️ 1. Post Board 예시

![코딩공책-29](https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/3ff8290a-f241-463e-a1ee-81891aaec4b5)

1. post 테이블에서 `findAll`해서 모든 post를 찾아온다. 별도의 테이블 `join`은 필요가 없다. <br>
   우리가 원하는 정보가 모두 post 테이블에 있기 떄문이다. <br>
2. 조건: 키워드를 포함하는<br>
   이를 위해서 `postService`에서: JPA에서 찾아온 모든 post중에, `stream().filter()`을 활용하여 키워드를 포함하는 post만 찾는다. <br>
3. 내가 JPA에서 받아온건 post인데, 내보내고 싶은 DTO는 postResponse이다. 따라서 `map(()-> new postResponse)`<br>

## ✔️ 2. ShoppingMall-verSoh 예시

![코딩공책-30](https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/48c1daf2-1cdd-4162-bbd6-d9104c5945e5)

1. 원하는 정보가 여러게 테이블에 흩어져 있다. 여러게 테이블을 `join`해서 정보 모아모아<br>
2. 조건: 키워드를 포함하는<br>
   이를 위해서 `productService`에서: JPA에서 찾아온 모든 products 중에, `stream().filter()`을 활용하여 키워드를 포함하는 products만 찾는다. <br>
3. 내가 JPA에서 받아온건 productMainResponse이고, 내보내고 싶은 DTO도 productMainResponse이다. 두 DTO가 일치하므로 별 문제없이 바로 내보낸다. <br>

## ✔️ 3. ShoppingMall-Mar2024 예시 ⭐️ 제일 깥끔

![코딩공책-31](https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/c23bf2a6-1a78-4295-84aa-4a8293a7e38b)

1. 원하는 정보가 여러게 테이블에 흩어져 있다. 키워드를 포함하는 조건도 있다. <br>
2. JPA에서 JPQL로 모든 로직(테이블 합치기 + 키워드 찾기)을 다 처리해버린다!<br>
3. JPA에서 받아온 응답과 내보내고 싶은 응답 또한 같으므로 바로 내보낸다. <br>

## ✔️ 4. service에서 각 테이블에서 각 JPA로 받아온 다음 합치기 예시

```java
 public ResponseDTO findProductDetail(Integer productId) {
        Product product = productJpa.findById(productId)
                .orElseThrow(() -> new NotFoundException("해당 아이디" + productId + "상품을 찾을 수 없습니다."));

        if(product.getProductStatus().equals("soldOut")) throw new SoldOutException("판매 종료된 상품입니다.");

        List<Review> reviews = reviewJpa.findByProduct(product);
        Double reviewAvg = reviews.stream().collect(Collectors.averagingDouble(Review::getScore));

        List<ProductPhoto> productPhotos = productPhotoJpa.findByProduct(product);
        List<PhotoRequestDto> photoRequestDtoList = productPhotos
                .stream()
                .map((p) -> new PhotoRequestDto(p.getPhotoUrl(), p.getPhotoType()))
                .collect(Collectors.toList());

        List<ProductOption> productOption = productOptionJpa.findByProduct(product);
        List<ProductOptionRequestDto> productOptionRequestDtoList = productOption
                .stream()
                .map((p) -> new ProductOptionRequestDto(p.getProductOptionId(), p.getColor(), p.getProductSize(), p.getStock()))
                .collect(Collectors.toList());

        List<ReviewUserDto> reviewUserDtoList = reviews
                .stream()
                .map((r) -> new ReviewUserDto(r.getUser().getUserId(), r.getReviewId(), r.getReviewContents(), r.getScore(), r.getCreatedAt()))
                .collect(Collectors.toList());


        ProductDetailResponse productDetailResponse = ProductDetailResponse.builder()
                .productId(product.getProductId())
                .productName(product.getProductName())
                .productPrice(product.getProductPrice())
                .category(product.getCategory())
                .productStatus(product.getProductStatus())
                .createAt(product.getCreatedAt())
                .finishAt(product.getFinishedAt())
                .scoreAvg(reviewAvg)
                .photoRequestDtoList(photoRequestDtoList)
                .productOptionRequestList(productOptionRequestDtoList)
                .reviewUserDtoList(reviewUserDtoList)
                .build();

        return new ResponseDTO(200, "제품 상세 조회 성공", productDetailResponse);

    }
```
