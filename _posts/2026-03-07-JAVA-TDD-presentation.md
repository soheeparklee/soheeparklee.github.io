---
title: Presentation layer- Mockito/MockMvc/Serialization/jakarta.validation
categories: [JAVA, TDD]
tags: [] # TAG names should always be lowercase
---

## ✅ Presentation Layer

- check parameter from front end

## ✅ MockMVC

- use Mock(fake data) to test MVC
- To test controller, make `service and repository` a mock data

- How to use?
- need two annotations
- `@WebMvcTest(controllers = ProductController.class)`
- `@Autowired private MockMvc mockMvc;`
- `@MockBean`
- 👉🏻 use `@MockitoBean`

```java
@WebMvcTest(controllers = ProductController.class)
class ProductControllerTest {
    @Autowired
    private MockMvc mockMvc;

    @Autowired
    private ObjectMapper objectMapper; //help Serialization, deserialization of objects

    @MockitoBean //make service mock
    private ProductService productService;


}
```

## 1️⃣ Post Mapping

## 📌 Production code: check request

```java
@RequiredArgsConstructor
@RestController
public class ProductController {
    private final ProductService productService;
    @PostMapping("/api/v1/products/new")
    public ProductResponse createProduct(@RequestBody ProductCreateRequest request){
        return productService.createProduct(request);
    }
}
```

- 🌙 For **serialization**
- In request class, need `@NoArgsConstructor`

```java
@Getter
@NoArgsConstructor //need for serialization, deserialization from ObjectMapper
public class ProductCreateRequest {

    private ProductType type;
    private ProductSellingStatus sellingStatus;
    private String name;
    private int price;
```

- For **base entity JPA auditing**
- create a distinct `JpaAuditingConfig` class
- and disable `@EnableJpaAuditing` in application

```java
@EnableJpaAuditing
@Configuration
public class JpaAuditingConfig {
}

//@EnableJpaAuditing //for base entity, disable and create distinct JpaAuditingConfig
@SpringBootApplication
public class CafeTddApplication {

    public static void main(String[] args) {
        SpringApplication.run(CafeTddApplication.class, args);
    }
}
```

## 📌 Test code: check request

- MockMVC
- Object Mapper
- test must include `@MockitoBean`
- should mock service to test controller

```java
@WebMvcTest(controllers = ProductController.class) // ⭐️ MockMVC
class ProductControllerTest {
    @Autowired
    private MockMvc mockMvc; //⭐️ MockMVC
    @Autowired
    private ObjectMapper objectMapper; //🌙 help Serialization, deserialization of objects
    @MockitoBean //test must include @MockitoBean
    private ProductService productService; //⭐️ MockMVC

    @DisplayName("Create product in controller")
    @Test
    void createProduct() throws Exception {
        //given
        ProductCreateRequest request = ProductCreateRequest.builder()
                .type(HANDMADE)
                .sellingStatus(SELLING)
                .name("americano")
                .price(4000)
                .build();
        //when //then
        mockMvc.perform(
                MockMvcRequestBuilders.post("/api/v1/products/new")
                    .content(objectMapper.writeValueAsString(request)) //🌙serliazize request
                    .contentType(MediaType.APPLICATION_JSON)
        )
                .andDo(MockMvcResultHandlers.print()) //see logs
                .andExpect(MockMvcResultMatchers.status().isOk());
    }

}
```

## ✅ Wrap Response in ApiResponse

#### ✔️ API response

```java
@Getter //can create json based on Getter
public class ApiResponse<T> {
    private int code;
    private HttpStatus status;
    private String message;
    private T data;

    public ApiResponse(HttpStatus status, String message, T data) {
        this.code = status.value();
        this.status = status;
        this.message = message;
        this.data = data;
    }

    public static <T> ApiResponse<T> of(HttpStatus httpStatus, String message, T data) {
        return new ApiResponse<T>(httpStatus, message, data);
    }

    public static <T> ApiResponse<T> of(HttpStatus httpStatus, T data) {
        return of(httpStatus, httpStatus.name(), data);
    }
    //response for creating OK
    public static <T> ApiResponse<T> ok(T data) {
        return ApiResponse.of(HttpStatus.OK, HttpStatus.OK.name(),  data);
    }
}

```

#### ✔️ ApiControllerAdvice

- use `@RestControllerAdvice`

```java
@RestControllerAdvice
public class ApiControllerAdvice {

    @ResponseStatus(HttpStatus.BAD_REQUEST)
    @ExceptionHandler(BindException.class)
    public ApiResponse<Object> bindException(BindException e){
        return ApiResponse.of(
                HttpStatus.BAD_REQUEST,
                e.getBindingResult().getAllErrors().get(0).getDefaultMessage(),
                null);
    }
}
```

#### ✔️ Product controller

- add `@Valid` to `@RequestBody`

```java
@PostMapping("/api/v1/products/new")
    //add @Valid to @RequestBody
    public ApiResponse<ProductResponse> createProduct(@Valid @RequestBody ProductCreateRequest request){
       return ApiResponse.ok(productService.createProduct(request));
    }
```

## 📌 Production code for validating parameter

- use **jakarta.validation**
- add dependencies

```gradle
    implementation 'org.springframework.boot:spring-boot-starter-validation'
```

#### ✔️ Request DTO

- In request class, add `@NotNull`, `@NotBlank`, `@Positive`

```java
@Getter
@NoArgsConstructor //need for serialization, deserialization from ObjectMapper
public class ProductCreateRequest {

    @NotNull(message = "Product type cannot be null")
    private ProductType type;

    @NotNull(message = "Product status cannot be null")
    private ProductSellingStatus sellingStatus;

    @NotBlank(message = "Product name cannot be blank")
    private String name;

    @Positive(message = "Product price should be positive")
    private int price;
}
```

- 🆚 Difference between `@NotNull`, `@NotBlank`, `@NotEmpty`
- `@NotNull`: cannot be null 👀 `""`, `"   "` will pass
- `@NotEmpty`: cannot be empty 👀 `"   "` will pass
- `@NotBlank`: if you do not want `""` nor `"   "`, use `@NotBlank`
- recommended for String validation

#### ❓ What if I want name to be length max 20?

- this specific validation should not be done in controller
- but should be dont in service layer
- or in constructor, when creating the product

- 👉🏻 controller should have the responsibility of http requests, responses

## 📌 Test code for validating the parameters

```java
    @DisplayName("When creating product, product type cannot be null")
    @Test
    void createProductWithoutType() throws Exception {
        //given
        ProductCreateRequest request = ProductCreateRequest.builder()
                .sellingStatus(SELLING)
                .name("americano")
                .price(4000)
                .build();
        //when //then
        mockMvc.perform(
                        post("/api/v1/products/new")
                                .content(objectMapper.writeValueAsString(request))
                                .contentType(MediaType.APPLICATION_JSON)
                )
                .andDo(print()) //see logs
                .andExpect(status().isBadRequest()) //check status, code, message...
                .andExpect(jsonPath("$.code").value(400))
                .andExpect(jsonPath("$.status").value("400 BAD_REQUEST"))
                .andExpect(jsonPath("$.message").value("Product type cannot be null"))
                .andExpect(jsonPath("$.data").isEmpty());

    }
```

- can also validate for the rest of attributes
- `@NotNull sellingStatus`
- `@NotBlank name`
- `@Positive price`

## 2️⃣ Get Mapping

## 📌 Production code for GET

```java
@RequiredArgsConstructor
@RestController
public class ProductController {
    private final ProductService productService;

    @GetMapping("/api/v1/products/selling")
    public ApiResponse<List<ProductResponse>> getSellingProducts(){
        return ApiResponse.ok(productService.getSellingProducts());
    }

```

## 📌 Test code for GET

```java
    @DisplayName("Get selling products")
    @Test
    void getSellingProducts() throws Exception {
    //given
        List<ProductResponse> result = List.of();
        when(productService.getSellingProducts()).thenReturn(result);

    //when //then
        mockMvc.perform(
                get("/api/v1/products/selling")
        )
                .andDo(print())
                .andExpect(status().isOk())
                .andExpect(jsonPath("$.code").value(200))
                .andExpect(jsonPath("$.status").value("200 OK"))
                .andExpect(jsonPath("$.message").value("OK"))
                .andExpect(jsonPath("$.data").isArray()); //just check if result is Array
    }

```

## ✅ Refactoring: create separate DTO for service

- now, service and controller is using the same DTO `CreateOrderRequest`
- however, service should not know what controller has

#### 👎🏻 before

```java
//controller
@RequiredArgsConstructor
@RestController
public class OrderController {
    private final OrderService orderService;
    @PostMapping("/api/v1/orders/new")
    public ApiResponse<OrderResponse> createOrder(@Valid @RequestBody OrderCreateRequest request ){ //controller recieve request
        LocalDateTime registerDateTime = LocalDateTime.now();
        return ApiResponse.ok( orderService.createOrder(request, registerDateTime)); //services uses the same request
    }
}

//service
//recieves the same request DTO as param
    public OrderResponse createOrder(OrderCreateRequest request, LocalDateTime registeredDateTime){
        List<String> productNumbers = request.getProductNumbers();
        List<Product> duplicateProducts = findProductsBy(productNumbers);

        deductStockQuantities(duplicateProducts);


        Order order = Order.create(duplicateProducts, registeredDateTime);
        Order savedOrder = orderRepository.save(order);
        return OrderResponse.of(savedOrder);
    }
```

#### 👍🏻 after

- create a separate DTO for service code,
- called `CreateOrderServiceRequest`

- `CreateOrderServiceRequest` looks identical to `CreateOrderRequest`
- In `CreateOrderRequest`, add `toServiceRequest()` method
- so controller can convert `CreateOrderRequest` into `CreateOrderServiceRequest`

```java
//CreateOrderRequest
@Getter
@NoArgsConstructor
public class OrderCreateRequest {
    @NotEmpty(message = "ProductNumberList cannot be empty")
    private List<String> productNumbers;

    @Builder
    public OrderCreateRequest(List<String> productNumbers) {
        this.productNumbers = productNumbers;
    }
    //method toServiceRequest()
    public OrderCreateServiceRequest toServiceRequest() {
        return OrderCreateServiceRequest.builder()
                .productNumbers(productNumbers)
                .build();
    }
}

//CreateOrderServiceRequest
@Getter
@NoArgsConstructor
public class OrderCreateServiceRequest {
    private List<String> productNumbers;

    @Builder
    public OrderCreateServiceRequest(List<String> productNumbers) {
        this.productNumbers = productNumbers;
    }
}
```

- now in controller,
- when calling service, hand over the `CreateOrderServiceRequest`

```java
//controller
@RequiredArgsConstructor
@RestController
public class OrderController {
    private final OrderService orderService;
    @PostMapping("/api/v1/orders/new")
    public ApiResponse<OrderResponse> createOrder(@Valid @RequestBody OrderCreateRequest request ){
        LocalDateTime registerDateTime = LocalDateTime.now();
        //convert to CreateOrderServiceRequest
        return ApiResponse.ok( orderService.createOrder(request.toServiceRequest(), registerDateTime));
    }
}

//service
//recieve OrderCreateServiceRequest as parameter
    public OrderResponse createOrder(OrderCreateServiceRequest request, LocalDateTime registeredDateTime){
        List<String> productNumbers = request.getProductNumbers();
        List<Product> duplicateProducts = findProductsBy(productNumbers);

        //filter, check stock for BAKERY or BOTTLE, and decrease stock quantity
        deductStockQuantities(duplicateProducts);


        Order order = Order.create(duplicateProducts, registeredDateTime);
        Order savedOrder = orderRepository.save(order);
        return OrderResponse.of(savedOrder);
    }
```
