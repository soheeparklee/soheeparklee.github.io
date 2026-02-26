---
title: Persistence layer test
categories: [JAVA, TDD]
tags: [] # TAG names should always be lowercase
---

## ✅ Production code

```java
@Repository
public interface ProductRepository extends JpaRepository<Product, Long> {
    /**
     * select *
     * from product
     * where selling_status IN ('SELLING', 'HOLD');
     */
    List<Product> findAllBySellingStatusIn(List<ProductSellingStatus> sellingStatuses);
}
```

## ✅ Test code

- can choose between `@SpringBootTest` and `@DataJpaTest`
- `@DataJpaTest` is faster, as it only loads JPA libraries
- `@ActiveProfiles` is for using only test code data

```java
//@SpringBootTest
@DataJpaTest //faster than spring, only brings JPA libraries
@ActiveProfiles("test") //do not use data.sql for test

class ProductRepositoryTest {
    @Autowired
    private ProductRepository productRepository;

    @DisplayName("Get products according to their selling status")
    @Test
    void findAllBySellingStatusIn(){
    //given
        Product product1 = Product.builder()
                .productNumber("001")
                .type(HANDMADE)
                .sellingStatus(SELLING)
                .name("americano")
                .price(4000)
                .build();
        Product product2 = Product.builder()
                .productNumber("002")
                .type(HANDMADE)
                .sellingStatus(HOLD)
                .name("latte")
                .price(4500)
                .build();
        Product product3 = Product.builder()
                .productNumber("003")
                .type(BAKERY)
                .sellingStatus(STOP_SELLING)
                .name("croissant")
                .price(3500)
                .build();
        productRepository.saveAll(List.of(product1, product2, product3));
    //when
        List<Product> products = productRepository.findAllBySellingStatusIn(List.of(SELLING, HOLD));
    //then
        assertThat(products).hasSize(2)
                .extracting("productNumber", "name", "sellingStatus")
                .containsExactlyInAnyOrder(
                        tuple("001", "americano", SELLING),
                        tuple("002", "latte", HOLD)

                );

    }

}
```

- when testing a list
- 1️⃣ check size
- 2️⃣ use `extracting()` and `contains()` to see if it has the value you expect

## ✅

## ✅

## ✅
