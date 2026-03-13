---
title: Business layer-create products/readOnly, CQRS/concurrency
categories: [JAVA, TDD]
tags: [] # TAG names should always be lowercase
---

## ✅ Business Logic

- (1) As a cafe manager, create products
- (2) product number should be created automatically

## 📌 Business for Product Service

```java
@Transactional(readOnly = true)
@RequiredArgsConstructor
@Service
public class ProductService {
    private final ProductRepository productRepository;

    public List<ProductResponse> getSellingProducts(){
        //reading from DB ➡️ readOnly = true
    }

    //only for CUD methods
    //➡️ readOnly = false
    // add Transactional
    @Transactional
    public ProductResponse createProduct(ProductCreateRequest request) {
        //create product number (001, 002, 003...)
        //get the last product number from DB, and add one

        String nextProductNumber = createNextProductNumber();
        Product product = request.toEntity(nextProductNumber);
        Product savedProduct = productRepository.save(product);


        return ProductResponse.of(savedProduct);
    }

    private String createNextProductNumber() {
        String latestProductNumer = productRepository.findLatestProduct();
        //if product is created for the first time
        if(latestProductNumer == null){
            return "001";
        }
        return String.format("%03d", Integer.valueOf(latestProductNumer) + 1);
    }
}
```

## ✅ Transactional(readOnly=true), CQRS

- `readOnly=true`
- means check transaction for only Read
- so, in `CRUD`, CUD will not work ❌ only Read ⭕️
- in `JPA`, CUD snapshot will not be created, will not check if updated(improve performance)

- It is recommended method of **CQRS**
- **CQRS**: separate Command(CUD) and Query(Read)
- ❓ Why?
- As there are much more Read than Command, makes sense to separate command and read responsibilities
- ❓ How?
- 1️⃣ create a **different sevice** for CUD and another service for Read(Transactional readOnly = true)
- 2️⃣ create a **different DB** for writing and another for reading

## 📌 Test for Product Service

```java
@ActiveProfiles("test") //not to use sql data
@SpringBootTest
class ProductServiceTest {
    @Autowired
    private ProductService productService;
    @Autowired
    private ProductRepository productRepository;

    @AfterEach
    void tearDown(){
        productRepository.deleteAllInBatch(); //clean data after each test
    }

    //concurrency problem
    @DisplayName("Create new product to DB")
    @Test
    void createProduct(){
        Product product1 = createProduct("001", HANDMADE, SELLING, "americano", 4000);
        Product product2 = createProduct("002", HANDMADE, HOLD, "latte", 4500);
        Product product3 = createProduct("003", BAKERY, STOP_SELLING, "croissant", 4000);
        productRepository.saveAll(List.of(product1, product2, product3));

        ProductCreateRequest request = ProductCreateRequest.builder()
                .type(HANDMADE)
                .sellingStatus(SELLING)
                .name("icecream")
                .price(5000)
                .build();
        //when
        ProductResponse response = productService.createProduct(request);
        //then
        assertThat(response).extracting("productNumber", "type", "sellingStatus", "name", "price")
                .contains("004", HANDMADE, SELLING, "icecream", 5000);

        List<Product> products = productRepository.findAll();
        assertThat(products)
                .hasSize(4)
                .extracting("productNumber", "type", "sellingStatus", "name", "price")
                .containsExactlyInAnyOrder(
                        tuple("001", HANDMADE, SELLING, "americano", 4000),
                        tuple("002", HANDMADE, HOLD, "latte", 4500),
                        tuple("003", BAKERY, STOP_SELLING, "croissant", 4000),
                        tuple("004", HANDMADE, SELLING, "icecream", 5000)
                );

    }

    @DisplayName("When DB is empty, and the first product is created, the product numer should be 001")
    @Test
    void createProductFirstTime(){
        //given
        ProductCreateRequest request = ProductCreateRequest.builder()
                .type(HANDMADE)
                .sellingStatus(SELLING)
                .name("icecream")
                .price(5000)
                .build();
        //when
        ProductResponse response = productService.createProduct(request);
        //then
        assertThat(response).extracting("productNumber", "type", "sellingStatus", "name", "price")
                .contains("001", HANDMADE, SELLING, "icecream", 5000);
        List<Product> products = productRepository.findAll();
        assertThat(products)
                .hasSize(1)
                .extracting("productNumber", "type", "sellingStatus", "name", "price")
                .contains(
                        tuple("001", HANDMADE, SELLING, "icecream", 5000)
                );
    }

    private Product createProduct(String productNumber, ProductType productType, ProductSellingStatus sellingStatus, String name, int price) {
        return Product.builder()
                .productNumber(productNumber)
                .type(productType)
                .sellingStatus(sellingStatus)
                .name(name)
                .price(price)
                .build();
    }

}
```

## ✅ Concurrency

- if several managers create products at the same time,
- `product number` can suffer from concunrrency issues

- ❓ How to solve?
- 1️⃣ make productNumber `UNIQUE` in DB, if fail, make the system retry
- 2️⃣ make productNumber UUID, less conflicts

## Optimistic lock 🆚 Pessimistic lock

- 🆚 **Optimistic lock:** no lock during read
- allow transactions to proceed without locking the data
- assume conflict is NOT likely

```
1. transaction reads a record
2. changes locally
3. before saving, check whether the record has been modified by another transaction
4. if changed, conflict detected, update fails/retries
```

- 👍🏻 higher concurrency
- 👎🏻 update failure
- 💊 handle conflicts by `detect & retry`
- 🛠️ When `read >>>>> write`, Hibernate

- 🆚 **Pessimistic lock**: lock data immediately
- assume conflict is likely

```
1. transaction reads a record
2. database locks the record
3. other transactions must wait until the lock is released
```

- 👍🏻 prevent conflict entirely
- 👎🏻 lower concurrency
- 👎🏻 deadlock, waiting
- 💊 conflict is totally prevented
- 🛠️ MySQL, Banking systems, Financial
