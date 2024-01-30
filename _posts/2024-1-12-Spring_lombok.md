---
title: Lombok Utility Library, Logback
categories: [JAVA, Spring]
tags: [
    lombok,
    getter,
    setter,
    noargsconstructor,
    allargsconstructor,
    equalandhashcode,
    builder,
    rowmapper
  ] # TAG names should always be lowercase
---

### 👎🏻 기존 코드 한계:

getter 생성자, bean 주입 생성자, Entity Equals, setter, hash...매번 생성하다보니 코드가 길어지고 반복됨 <br>
<br>

👌🏻 **Lombok**으로 해결!<br>
🕵🏻‍♂️ Lombok **runtime meta programming** <br>
annotation 프로세서가 컴파일 이후 자동으로 코드를 생성해준다. <br>

## 🌶️ Lombok

> 목적: 반복되는 코드 줄이기 <br>
> how to use: annotation <br>

```java
@Getter, @Setter
@NoArgsConstructor
@AllArgsConstructor
@EqualAndHashCode
@Builder
```

➡️ Lombok annotation이 자동으로 getter, setter, Constructor 만들어 준다, <br>

#### 🌶️ Lombok사용해 빈 생성자, 게터 생략하기 @Getter, @NoArgsConstructor

```java
//🌶️ Lombok사용해 빈 생성자, 게터 생략하기
import lombok.Getter;
import lombok.NoArgsConstructor;

@Getter
@NoArgsConstructor
public class ItemBody {
    private String name;
    private String type;
    private int price;
    private Spec spec;

//    public ItemBody(){} //🌶️Lombok 덕에 빈 생성자 생략해도 됨
//
//    public String getName() { //🌶️Lombok 덕에 게터 생략해도 됨
//        return name;
//    }
//
//    public String getType() {
//        return type;
//    }
//
//    public int getPrice() {
//        return price;
//    }
//
//    public Spec getSpec() {
//        return spec;
//    }
}
```

#### 🌶️ Lombok사용해 Bean 생성자 생략하기

❓ 언제 Bean 생성자 만들었더라?<br>
<br>

- Controller에서 Repository가져올 때<br>
- Service 가져올 때
- Dao에서 Jdbc Template 가져올 때 등등<br>
  따라서 Lombok을 Bean에도 적용 가능하다.<br>

💡 보통 Bean을 주입할 때는 final을 붙인다.<br>

> final: 상수로, 바꿀 수 없게 <br>

한 번 Service, Repository, JdbcTemplate 가져오면 안 바뀌니까<br>

```java
//🌶️ Controller에서 Repository가져올 때 Lombok사용해 Bean 생성자 생략하기
@RequiredArgsConstructor
@RestController
@RequestMapping("/api")
public class ElectronicStoreControllerLombok {
    //🌶️Lombok 덕에 bean 생성자 생략가능
    private final ElectronicStoreItemService electronicStoreItemService;
//    public ElectronicStoreControllerLombok(ElectronicStoreItemService electronicStoreItemService) {
//        this.electronicStoreItemService = electronicStoreItemService;
//    }
```

```java
//🌶️  Dao에서 Jdbc Template 가져올 때Lombok사용해 Bean 생성자 생략하기
//🚫🚫🚫 하지만 이 코드는 lombok 사용 불가 🚫🚫🚫
// @RequiredArgsConstructor ❌
@Repository
public class AirlineTicketJdbcDao implements AirlineTicketRepository{

    private final JdbcTemplate jdbcTemplate;
//🌶️으로 bean 생성자 생략하려고 하였으나, 현재 jdbcTemplate이 2개인 상황
//그래서 어떤 jdbcTemplate인지 명시해 주어야 하므로 constructor 생략 불가
//어떤 jdbcTemplate인지 명시하기 위해 @Qualifier("jdbcTemplate2")
//만약 jdbcTemplate하나면 lombok으로 bean 생성자 생략 가능⭕️
   public AirlineTicketJdbcDao(@Qualifier("jdbcTemplate2") JdbcTemplate jdbcTemplate) {
       this.jdbcTemplate = jdbcTemplate;
   }
```

#### 🌶️ Lombok사용해 Entity @AllArgsConstructor, @EqualsAndHashCode

```java
@Getter
@Setter
@AllArgsConstructor
@EqualsAndHashCode(of= "id") //어떤 것을 기준으로 equals 할 것인가? 꼭 조건을 알려 줘야 한다.
public class ItemEntity {
    private Integer id;
    private String name;
    private String type;
    private Integer price;
    private Integer storeId;
    private Integer stock;
    private String cpu;
    private String capacity;
//🌶️Lombok 덕에 equals, hash 생략가능
//    @Override
//    public boolean equals(Object o) {
//        if (this == o) return true;
//        if (!(o instanceof ItemEntity that)) return false;
//        return Objects.equals(id, that.id);
//    }
//
//    @Override
//    public int hashCode() {
//        return Objects.hash(id);
//    }
// 🌶️Lombok 덕에 constructor 생략가능
    // public ItemEntity(Integer id, String name, String type, Integer price, Integer storeId, Integer stock, String cpu, String capacity) {
    //     this.id = id;
    //     this.name = name;
    //     this.type = type;
    //     this.price = price;
    //     this.storeId = null;
    //     this.stock = 0;
    //     this.cpu = cpu;
    //     this.capacity = capacity;
    // }
// 🌶️Lombok 덕에 getter, setter 생략가능
//    public Integer getId() {
//        return id;
//    }
//
//    public void setId(Integer id) {
//        this.id = id;
//    }
//
//    public String getName() {
//        return name;
//    }
//
//    public void setName(String name) {
//        this.name = name;
//    }
//
//    public String getType() {
//        return type;
//    }
//
//    public void setType(String type) {
//        this.type = type;
//    }
//
//    public Integer getPrice() {
//        return price;
//    }
//
//    public void setPrice(Integer price) {
//        this.price = price;
//    }
//
//    public String getCpu() {
//        return cpu;
//    }
//
//    public void setCpu(String cpu) {
//        this.cpu = cpu;
//    }
//
//    public String getCapacity() {
//        return capacity;
//    }
//
//    public void setCapacity(String capacity) {
//        this.capacity = capacity;
//    }
//
//
//    public Integer getStoreId() {
//        return storeId;
//    }
//
//    public void setStoreId(Integer storeId) {
//        this.storeId = storeId;
//    }
//
//    public Integer getStock() {
//        return stock;
//    }
//
//    public void setStock(Integer stock) {
//        this.stock = stock;
//    }
}

```

#### 🌶️ Lombok사용해 DAO의 RowMapper 개선 @Builder

RowMapper는 DAO에 있음, <br>
❗️ 그러나 @Build는 Entity에 추가 <br>
Lombok @Builder을 사용하면 순서를 바꿔도 상관 업음!

```java
//🌶️ Lombok사용해 DAO의 RowMapper 개선하기
@Repository
public class ElectronicStoreItemJdbcDao implements ElectronicStoreItemRepository{

    private JdbcTemplate jdbcTemplate;
    public ElectronicStoreItemJdbcDao(@Qualifier("jdbcTemplate1") JdbcTemplate jdbcTemplate) {
        this.jdbcTemplate = jdbcTemplate;
    }
    //기존 코드 RowMapper는 순서를 맞춰야 하므로 헷갈릴 수 있음
    //이를 lombok builder로 개선
//    static RowMapper<ItemEntity> itemEntityRowMapper= (((rs, rowNum)->
//            new ItemEntity(
//                    rs.getInt("id"),
//                    rs.getNString("name"),
//                    rs.getNString("type"),
//                    rs.getInt("price"),
//                    rs.getInt("store_id"),
//                    rs.getInt("stock"),
//                    rs.getNString("cpu"),
//                    rs.getNString("capacity")
//            )));
//🌶️ Lombok사용해 build하면 명시를 해주어 순서 헷갈려도 괜찮음.
    static RowMapper<ItemEntity> itemEntityRowMapper= (((rs, rowNum)->
            new ItemEntity.ItemEntityBuilder()
                    .id(rs.getInt("id"))
                    .name(rs.getNString("name"))
                    .type(rs.getNString("type"))
                    .price(rs.getInt("price"))
                    .storeId(rs.getInt("store_id"))
                    .stock(rs.getInt("stock"))
                    .cpu(rs.getNString("cpu"))
                    .capacity(rs.getNString("capacity"))
                    .build()));

//⭐️ @ Build는 Entity에 추가
@Getter
@Setter
@AllArgsConstructor
@EqualsAndHashCode(of= "id")
@Builder //⭐️
public class ItemEntity {
    private Integer id;
    private String name;
    private String type;
    private Integer price;
    private Integer storeId;
    private Integer stock;

    private String cpu;
    private String capacity;
>
```
