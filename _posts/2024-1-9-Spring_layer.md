---
title: Spring boot Layer
categories: [JAVA, Spring]
tags: [] # TAG names should always be lowercase
---

![코딩공책-23](https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/b8bdaefc-1d7b-4289-82c1-268beaa4fa2c)

## ✅ Web Layer

### ✔️ Web Layer Class

#### ☑️ Controller

#### ☑️ DTO: Data Transfer Object

> 계층 간 데이터 교환을 위한 Java Beans <br>
> 데이터를 **전달**하기 위한 객체 <br>
> 데이터베이스 레코드의 데이터를 매핑하기 위한 데이터 객체 <br>
> 보통 로직을 가지고 있지 않고 data와 그 data에 접근하기 위한 getter, setter를 가지고 있다. <br> > <br>

이번 실습에서는 **빈 생성자**와 **getter**을 추가했음 <br>

#### 🆚 DAO: Data Access Object

> database의 data에 **접근**하기 위한 객체 <br>
> 데이터베이스 접근을 하기 위한 로직과 비즈니스 로직을 **분리**하기 위해 사용 <br> > <br>
> 데이터의 CRUD작업을 실행하는 클래스<br><br>

#### 🆚 VO: Value Object

> 값 자체를 표현하는 객체<br>

VO는 getter를 포함한 다른 비즈니스 로직도 가질 수 있다.<br>
그러나 setter은 가지지 않음, 사용하는 도중에 값 변경이 불가능하므로<br>

#### 🆚 Entity

> 실제 DB와 매핑이 되는 클래스<br>

DTO와 반드시 분리되어야 한다.<br>

#### ☑️ exception handlers

#### ☑️ Filters

### ✔️ Rest Controller and Dispatcher Servlet

> HTTP method ➕ URI로 Controller 매핑 후 해당 method 실행<br>

### 💡 Web Layer CRUD 구현 예시

1️⃣ 모든 아이템 조회 GET <br>
2️⃣ 새로운 아이템 등록 POST <br>
3️⃣ Path ID로 아이템 조회 GET <br>
4️⃣ 쿼리 파라미터로 ID 조회 <br>
5️⃣ 여러 ID 쿼리 파라미터로 조회 GET <br>
6️⃣ Path ID로 아이템 삭제 DELETE <br>
7️⃣ Path ID와 Body로 업데이트 UPDATE <br>

#### 1️⃣ 모든 아이템 조회 GET & 2️⃣ 새로운 아이템 등록 POST

1️⃣ 모든 아이템 조회 GET
<img width="890" alt="스크린샷 2024-01-09 오후 9 22 23" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/f3a2484e-6bde-4333-82ea-842b3d23efd9">

```java
//1️⃣ 모든 아이템 조회 GET
//get할 때 가져오는 itemBody

public class ItemBody {
    private String name;
    private String type;
    private int price;
    private Spec spec;

    public ItemBody(){}

    public String getName() {
        return name;
    }

    public String getType() {
        return type;
    }

    public int getPrice() {
        return price;
    }

    public Spec getSpec() {
        return spec;
    }
}

//spec은 또 따른 클래스로 정의해줘야 함
public class Spec {
    private String cpu;
    private String capacity;

    public Spec(){
    }

    public Spec(String cpu, String capacity) {
        this.cpu = cpu;
        this.capacity = capacity;
    }

    public String getCpu() {
        return cpu;
    }

    public String getCapacity() {
        return capacity;
    }
}
```

2️⃣ 새로운 아이템 등록 POST
<img width="886" alt="스크린샷 2024-01-09 오후 9 25 48" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/343271b2-75f7-47f2-a60c-25a91b7f0d8c">

```java
//2️⃣ 새로운 아이템 등록 POST
//post 할 때 보내는 item
public class Item {
    private String id;
    private String name;
    private String type;
    private int price;
    private Spec spec;

    public Item() {
    }
    //2️⃣새로운 아이템 등록 POST
    //post할 때 가져올 item을 constructor로 선언
    //⭐️ ItemBody는 get하기 위해 선언했었음
    public Item(Integer id, ItemBody itemBody) {
        this.id = String.valueOf(id);
        this.name= itemBody.getName();
        this.type= itemBody.getType();
        this.price= itemBody.getPrice();
        this.spec= itemBody.getSpec();
    }

    public String getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public String getType() {
        return type;
    }

    public int getPrice() {
        return price;
    }

    public Spec getSpec() {
        return spec;
    }
}

```

```java
//💡 실행클래스 💡
//1️⃣ 모든 아이템 조회 GET
@RestController
@RequestMapping("/api")
public class ElectronicStoreController {

    //1️⃣ 모든 아이템 조회 GET 위해 list
    private List<Item> items= new ArrayList<>();
    //2️⃣새로운 아이템 등록 POST 위해 필요한 serialID
    //get할 때마다 아이디 새롭게 지정하도록
    private static int serialItemId= 1;
    @GetMapping("/items")
    public List<Item> findAllItem(){
        return items;
    }
    //2️⃣ 새로운 아이템 등록 POST
    @PostMapping("/items")
    public String registerItem(@RequestBody ItemBody itemBody){
        //json값이 들어왔을 때 여기서 받을 것이다.
        //Item에서 itemBody constructor로 받아올 것임
        //get할 때마다 아이디 ++
        Item newItem= new Item(serialItemId++, itemBody);
        items.add(newItem);
        return "ID:"+ newItem.getId();
    }
}

```

#### ⭐️ 만약 item 미리 post 해두려면

```java
//2️⃣새로운 아이템 등록 POST
//post 할 때 보내는 item
public class Item {
    private String id;
    private String name;
    private String type;
    private int price;
    private Spec spec;

    public Item() {
    }
    //2️⃣새로운 아이템 등록 POST
    //post할 때 가져올 item을 constructor로 선언
    // ⭐️ item 미리 post 해두고 각각 가져오기
    public Item(String id, String name, String type, Integer price, String cpu, String capacity) {
        this.id = id;
        this.name= name;
        this.type= type;
        this.price= price;
        this.spec= new Spec(cpu, capacity);
    }

    public String getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public String getType() {
        return type;
    }

    public int getPrice() {
        return price;
    }

    public Spec getSpec() {
        return spec;
    }
}

public class ElectronicStoreController {
    //2️⃣새로운 아이템 등록 POST 위해 필요한 serialID
    private static int serialItemId= 1;

    //1️⃣ 모든 아이템 조회 GET 위해 list
    private List<Item> items= new ArrayList<>(Arrays.asList(
        //미리 arrayList에 넣어두기도 가능함
            new Item(String.valueOf(serialItemId++), "Iphone", "Electronics", 1000, "IntelCore", "128GB"),
            new Item(String.valueOf(serialItemId++), "BeamProjector", "Gadget", 2000, "ChinaCPU", "5GB"),
            new Item(String.valueOf(serialItemId++), "Laptop", "Apple", 3000, "M2chip", "512GB")
    ));

    @GetMapping("/items")
    public List<Item> findAllItem(){
        return items;
    }
    //2️⃣새로운 아이템 등록 POST
    @PostMapping("/items")
    public String registerItem(@RequestBody ItemBody itemBody){
        //json값이 들어왔을 때 여기서 받을 것이다.
        //Item에서 itemBody constructor로 받아올 것임
        Item newItem= new Item(serialItemId++, itemBody);
        items.add(newItem);
        return "ID:"+ newItem.getId();
    }
}

```

#### 3️⃣ Path ID로 아이템 조회 GET

```java
    //실행클래스
    // 3️⃣ Path ID로 아이템 조회 GET
    //id값으로 path 설정
    //id를 parameter로 받도록 설정
    @GetMapping("/items/{id}")
    public Item findItemByPathID(@PathVariable String id){
        //item찾는 stream
        //못 찾으면 Throw
        Item itemFound= items.stream()
                                .filter(item-> item.getId().equals(id))
                                .findFirst().orElseThrow(()->new RuntimeException());
        return itemFound;
    }
```

#### 4️⃣ 쿼리 파라미터로 ID 조회

```java
    //4️⃣ 쿼리 파라미터로 ID 조회
    @GetMapping("/items-query") //GET api/items-query?id=1
    public Item findItemByQueryID(@RequestParam("id") String id){ //여기에 받을 id를 parameter로 받는다.
        //찻는거니까 3️⃣ Path ID로 아이템 조회랑 비슷
        Item itemFound= items.stream()
                .filter(item-> item.getId().equals(id))
                .findFirst()
                .orElseThrow(()->new RuntimeException());
        return itemFound;

    }
```

#### 5️⃣ 여러 ID 쿼리 파라미터로 조회 GET

여러개의 ID가 들어오면 어떻게?

```java
    @GetMapping("/items-queries")
    public List<Item> findItemByManyQueryIDs(@RequestParam("id") List<String> ids){ //id몇 개가 parameter로 들어올지 모르니 list로
        //id를 비교하기 위해서 set으로 바꿨다가
        Set<String> idSet= ids.stream().collect(Collectors.toSet());
        List<Item> itemsFound= items.stream()
                .filter(item -> idSet.contains(item.getId()))
                .collect(Collectors.toList());
        return itemsFound;
    }
```

#### 6️⃣ Path ID로 아이템 삭제 DELETE

```java
    // 6️⃣ Path ID로 아이템 삭제 DELETE
    @DeleteMapping("/items/{id}")
    public String deleteItemByPathID(@PathVariable String id){
        //일단 items가 없다면 error throw
        Item itemFound= items.stream()
                .filter(item-> item.getId().equals(id))
                .findFirst()
                .orElseThrow(()->new RuntimeException());
        //item찾아서 delete
        items.remove(itemFound);
        return "Item with ID " + itemFound.getId() + "Deleted";
    }

    //⭐️ Item에다가 equals, hash해 주어야 한다.
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof Item item)) return false;
        return Objects.equals(id, item.id);
    }

    @Override
    public int hashCode() {
        return Objects.hash(id);
    }
```

#### 7️⃣ Path ID와 Body로 업데이트 UPDATE

```java
    @PutMapping("/items/{id}")
    //어떤 item바꿀지 알기 위해 id받고(@PathVariable), 어떻게 바꿀지 받기 위해 itemBody도 받는다.(@RequestBody)
    public String updateItem(@PathVariable String id, @RequestBody ItemBody itemBody){
        //일단 items찾아서 만약 없다면 error throw
        Item itemFound= items.stream()
                .filter(item-> item.getId().equals(id))
                .findFirst()
                .orElseThrow(()->new RuntimeException());
        //그리고 찾은 기존의 아이템 지워버림
        items.remove(itemFound);
        //item새로 만들기
        Item itemUpdated= new Item(Integer.valueOf(id), itemBody);
        items.add(itemUpdated);
        return itemUpdated;
    }
```

## ✅ Data Access Layer(🟰Repository Layer)

### ☑️ Entity(🟰model)

> 데이터 베이스 테이블과 1대 1 매핑되는 자바 객체<br>
> DB와 JAVA 애플리케이션 간에 소통을 담당<br>
> <br>

⭐️ Entity와 DTO는 무조건 다른 클래스로 구현되어야, **꼭 분리되어야 한다**<br>
<br>

- 역할 분리 위하여<br>
- 보안 및 노출 제어 위해서<br>
- 의존성 분리 위해서<br>

### ☑️ Repository 구현체: JDBC template

> JDBC template: Spring에서 제공하는 JDBC 사용해 DB와 상호작용<br>

<br>

> RowMapper: DB와 JAVA를 각각 매핑해 주는 역할<br>

<br>

> DataSource: Spring에서 데이터베이스와의 커넥션을 관리하고 제공하는 **빈**

### 💡 Data Access Layer 구현 예시

#### ✔️ sql 구현

```sql
CREATE TABLE item(
	id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50) NOT NULL UNIQUE,
    type VARCHAR(50) NOT NULL,
    price INT,
    cpu VARCHAR(30),
    capacity VARCHAR(30)
);

INSERT INTO item(name, type, price, cpu, capacity)
VALUES
	('Iphone', 'Phone' , 1000, 'M2chip', '512GB'),
    ('Laptop', 'computer' , 12000, 'Apple', '218GB'),
    ('Ipad', 'Pad' , 10000, 'Samsung', '200GB'),
    ('Chair', 'Brown' , 3000, 'Wood', 'Chedar'),
    ('Vaccum', 'Cleaner' , 18000, 'Red', '100L');
```

#### 1️⃣ config, dataSource 추가, bean 등록

config 추가해서 dataSource 추가 <br>
여기에 JDBC관련된 bean들을 추가하는 곳이다. <br>
bean을 등록한다. <br>
그리고 만약 드라이버 없으면 build.gradle에 드라이버도 설치해야 한다. <br>
`implementation 'org.springframework.boot:spring-boot-starter-data-jdbc'` <br>
`runtimeOnly 'mysql:mysql-connector-java:8.0.26'` <br>

#### 2️⃣ config에 JDBC template을 등록한다.

❓ 어디에: config<br>
JDBC template안에 dataSource를 넣는다.<br>
그리고 JDBC template도 bean이다!<br>

```java
//🐬mySql이랑 연결
//jdbc관련 build를 하는 파일
@Configuration
public class JdbcConfig {
    //JAVA와 데이터베이스 연결
    //1️⃣ config, dataSource 추가, bean 등록
    @Bean
    public DataSource dataSource(){
        DriverManagerDataSource dataSource= new DriverManagerDataSource();
        //set을 통해서 실제로 어떤 user인지, 어디에 있는지 설정해서 알려주어야 한다.
        //각각 setUsername, setPassword, setDriverClassName도 알려주어여 한다.
        dataSource.setUsername("root");
        dataSource.setPassword("12341234");
        dataSource.setDriverClassName("com.mysql.cj.jdbc.Driver"); //mySql이랑 연결할꺼니까 driver도 mySql
        dataSource.setUrl("jdbc:mysql://localhost:3306/chap_95?useUnicode= true&characterEncoding=UTF-8"); //어디로 접근할 것인가?
        //여기에 DB서버를 쓰는 것
        //우리는 localhost:3306에서 진핼할 것
         //schema: chap_95
        return dataSource;
    }
    //2️⃣ config에 JDBC template을 등록
    @Bean
    public JdbcTemplate jdbcTemplate(){return new JdbcTemplate(dataSource());}
}
```

#### 3️⃣ Repository Interface 구현

```java
public interface ElectronicStoreItemRepository {
        List<Item> findAllItems();
}
```

#### 4️⃣ Controller에 Repository Interface 추가

```java
//🐬mySql이랑 연결
    private ElectronicStoreItemRepository electronicStoreItemRepository;
    //생성자
    public ElectronicStoreController(ElectronicStoreItemRepository electronicStoreItemRepository) {
        this.electronicStoreItemRepository = electronicStoreItemRepository;
    }
```

#### ☑️ 이제 Repository Interface사용해서 GET 바꿔줘야지

🚫 하지만 이 코드는 틀린 코드 <br>
DTO, Entity를 나눠주지 않았기 때문 <br>
나중에 아래에서 수정할 예정 <br>

```java
   @GetMapping("/items")
    public List<Item> findAllItem(){
        //return items;
        //🐬mySql이랑 연결
        return electronicStoreItemRepository.findAllItems();
    }
```

#### 5️⃣ `findAllItems()`라는 함수를 Repository Interface 에 추가해줘야지

#### 6️⃣ Repository Interface를 구현한 구현체가 필요하다 ➡️ ElectronicStoreItemJdbcDao

controller는 interface 사용하고 <br>
interface를 구현하는 클래스가 필요하다. <br>
이렇게 interface를 구현하는 클래스를 사용하는 이유는 ➡️ **느슨한 결합**을 위해서이다. <br>
느슨한 결합을 사용해 DB의 버전이 바꾸더라도 내부에는 문제 없이 실행되도록 <br>

```java
@Repository
 //Repository를 넣어주면 bean 등록
public class ElectronicStoreItemJdbcDao implements ElectronicStoreItemRepository{

    //db에 접근
    private JdbcTemplate jdbcTemplate;
    // jdbcTemplate도 bean이니까 생성자 만들어주어야 한다
    // JdbcTemplate는 JdbcConfig에서 정의했음
    public ElectronicStoreItemJdbcDao(JdbcTemplate jdbcTemplate) {
        this.jdbcTemplate = jdbcTemplate;
    }
}
```

#### 7️⃣ ⭐️ItemEntity⭐️ 만들어야지

ItemEntity는 sql에서 create한 테이블과 **1대1 매핑**되어야 한다. <br>
복잡해보이지만 사실 각 필드에 대한 constructor, getter, setter 정의한 것이다. <br>
⭐️ 중요한 건 아이디로 equals, hash해야 한다는 것! <br>

```java
public class ItemEntity {
    //db의 sql에서 작성한 테이블과 1대1 매핑이 된다.
    private Integer id;
    private String name;
    private String type;
    private Integer price;
    private String cpu;
    private String capacity;

    //⭐️ id를 기준으로 equals, hashCode구현
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof ItemEntity that)) return false;
        return Objects.equals(id, that.id);
    }

    @Override
    public int hashCode() {
        return Objects.hash(id);
    }

    public ItemEntity(Integer id, String name, String type, Integer price, String cpu, String capacity) {
        this.id = id;
        this.name = name;
        this.type = type;
        this.price = price;
        this.cpu = cpu;
        this.capacity = capacity;
    }


    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getType() {
        return type;
    }

    public void setType(String type) {
        this.type = type;
    }

    public Integer getPrice() {
        return price;
    }

    public void setPrice(Integer price) {
        this.price = price;
    }

    public String getCpu() {
        return cpu;
    }

    public void setCpu(String cpu) {
        this.cpu = cpu;
    }

    public String getCapacity() {
        return capacity;
    }

    public void setCapacity(String capacity) {
        this.capacity = capacity;
    }


}

```

#### 8️⃣ RowMapper, findAllItems() override

```java
@Repository
 //Repository를 넣어주면 bean 등록
public class ElectronicStoreItemJdbcDao implements ElectronicStoreItemRepository{

    //RowMapper는 JDBC를 쉽게 사용해 field를 ⭐️매핑⭐️시키기 위해 필요하다.
    //⭐️ DTO와 Entity는 분리해야
    //Item: DTO, ItemEntity: Entity로 따로 만들어야
    //RowMapper는 Functional Interface
    //➖ rs: 각각의 필드에 접근
    //➖ rowNum: 한 줄씩 한 줄씩 읽는다
    static RowMapper<ItemEntity> itemEntityRowMapper= (((rs, rowNum)->
            //db에서 데이터 받아와 어떤 객체를 만들지 알려준다.
            new ItemEntity(
                    rs.getInt("id"),
                    rs.getNString("name"),
                    rs.getNString("type"),
                    rs.getInt("price"),
                    rs.getNString("cpu"),
                    rs.getNString("capacity")
            )));

    //db에 접근
    // private JdbcTemplate jdbcTemplate;
    // // jdbcTemplate도 bean이니까 생성자 만들어주어야 한다
    // // JdbcTemplate는 JdbcConfig에서 정의했음
    // public ElectronicStoreItemJdbcDao(JdbcTemplate jdbcTemplate) {
    //     this.jdbcTemplate = jdbcTemplate;
    // }


    //🚫이 코드도 추후에 수정할 예정
    @Override
    public List<Item> findAllItems() {
        //여기에 sql query를 넣는다.
        //그리고 itemEntityRowMapper를 넣어서 1대1 매핑
        List<ItemEntity> itemEntities= jdbcTemplate.query("SELECT * FROM item", itemEntityRowMapper);
        //⭐️ 생성자로 db에서 들어온 데이터 JAVA에서 원하는 형식으로 만들기
        //🔟 이를 위해 Item.java에 ItemEntity받는 Item생성자 추가
        return itemEntities.stream().map(Item::new).collect(Collectors.toList());
    }
}
```

#### 9️⃣ Item.java에 ItemEntity받는 Item생성자 추가

```java
public class Item {
    //⭐️ 생성자로 db에서 들어온 데이터 JAVA에서 원하는 형식으로 만들기
    public Item (ItemEntity itemEntity){
        this.id= itemEntity.getCapacity();
        this.type= itemEntity.getType();
        this.price= itemEntity.getPrice();
        this.name= itemEntity.getName();
        //spec은 하나로 합쳐줘야 함
        this.spec= new Spec(itemEntity.getCpu(), itemEntity.getCapacity());
    }
}
```

#### 1️⃣ GET 바꾸기

itemEntity받도록 다시 구현한다. <br>
위에서처럼 구현하면 안 된다. <br>
DTO와 Entity를 각각 구현해야 하기 떄문 <br>

```java
//controller
    @GetMapping("/items")
    public List<Item> findAllItem(){
        List<ItemEntity> itemEntities= electronicStoreItemRepository.findAllItems();
        return itemEntities.stream().map(Item::new).collect(Collectors.toList());
    }
//dao
    @Override
    public List<Item> findAllItems() {
        return jdbcTemplate.query("SELECT * FROM item", itemEntityRowMapper);
    }

```

#### 2️⃣ 새로운 아이템 등록 POST

☝🏻 ElectronicStoreController에서 POST할 때 electronicStoreItemRepository사용 <br>
✌🏻 ElectronicStoreItemRepository에서 `saveItem()` 구현 <br>
🤙🏻 ElectronicStoreItemJdbcDao에서 `saveItem()` Override <br>

```java
//☝🏻ElectronicStoreController에서 POST할 때 electronicStoreItemRepository사용
public class ElectronicStoreController {
    @PostMapping("/items")
    public String registerItem(@RequestBody ItemBody itemBody){
//        Item newItem= new Item(serialItemId++, itemBody);
//        items.add(newItem);
//        return "ID:"+ newItem.getId();
        //🐬mySql이랑 연결
        Integer itemID= electronicStoreItemRepository.saveItem(itemBody);
        return "ID:"+ itemID;
    }
}

//✌🏻 ElectronicStoreItemRepository에서 `saveItem()` 구현
public interface ElectronicStoreItemRepository {
    List<Item> findAllItems();

    Integer saveItem(ItemBody itemBody);
}

//🤙🏻 ElectronicStoreItemJdbcDao에서 `saveItem()` Override
@Repository
public class ElectronicStoreItemJdbcDao implements ElectronicStoreItemRepository{
    @Override
    public Integer saveItem(ItemBody itemBody) {
        //테이블에 데이터 넣을때는 ⭐️update⭐️
        //가져올 때는 query
        jdbcTemplate.update("INSERT INTO item(name, type, price, cpu, capacity) VALUES(?, ?, ?, ?, ?)"
                            itemBody.getName(),
                            itemBody.getType(),
                            itemBody.getPrice(),
                            itemBody.getSpec().getCpu(),
                            itemBody.getSpec().getCapacity());

        //한 개만 불러올 때는 queryForObject
        //어떤 Item만들어졌는지 확인하기 위해서 가져오기
        ItemEntity itemEntity= jdbcTemplate.queryForObject("SELECT * FROM item WHERE name=?", itemEntityRowMapper, itemBody.getName());
        return itemEntity.getId();
    }
}
```

#### 2️⃣ POST 새로운 아이템 등록할 때 itemEntity받도록 수정

itemEntity를 사용하도록 수정한다.<br>

```java
//controller
    @PostMapping("/items")
    public String registerItem(@RequestBody ItemBody itemBody){
    ItemEntity itemEntity = new ItemEntity(null,
            itemBody.getName(),
            itemBody.getType(),
            itemBody.getPrice(),
            itemBody.getSpec().getCpu(),
            itemBody.getSpec().getCapacity());
        Integer itemID= electronicStoreItemRepository.saveItem(itemEntity);
        return "ID:"+ itemID;
    }

//repository
public interface ElectronicStoreItemRepository {
    List<Item> findAllItems();

    Integer saveItem(ItemEntity itemEntity);
}

//dao
    @Override
    public Integer saveItem(ItemEntity itemEntity) {
        jdbcTemplate.update("INSERT INTO item(name, type, price, cpu, capacity) VALUES(?, ?, ?, ?, ?)"
                            itemEntity.getName(),
                            itemEntity.getType(),
                            itemEntity.getPrice(),
                            itemEntity.getCpu(),
                            itemEntity.getCapacity());

        ItemEntity itemEntityFound= jdbcTemplate.queryForObject("SELECT * FROM item WHERE name=?", itemEntityRowMapper, itemBody.getName());
        return itemEntityFound.getId();
    }
```

#### 3️⃣ Path ID로 아이템 조회 GET

```java
    @GetMapping("/items/{id}")
    public Item findItemByPathID(@PathVariable String id){
        Integer idInt= Integer.parseInt(id);
        ItemEntity itemEntity= electronicStoreItemRepository.findItemById(idInt);
        Item item= new Item(itemEntity);
        return item;
    }
```

#### 5️⃣ 여러 ID 쿼리 파라미터로 조회 GET

```java
    @GetMapping("/items-queries")
    public List<Item> findItemByManyQueryIDs(@RequestParam("id") List<String> ids){
        List<ItemEntity> itemEntities = electronicStoreItemRepository.findAllItems();
        List<Item> items= itemEntities.stream()
                .map(Item::new)
                .filter((item)->ids.contains(item.getId()))
                .collect(Collectors.toList());
        return electronicStoreItemService.findAllItemsByIds(ids);
    }
```

#### ☑️ Path ID와 Body로 업데이트 UPDATE

//☝🏻 ElectronicStoreController에서 UPDATE할 때 electronicStoreItemRepository사용<br>
//✌🏻 ElectronicStoreItemRepository에서 `updateItemEntity()` 구현<br>
//🤙🏻 ElectronicStoreItemJdbcDao에서 `updateItemEntity()` Override<br>

```java
//☝🏻 ElectronicStoreController에서  UPDATE할 때 electronicStoreItemRepository사용
    @PutMapping("/items/{id}")
    public String updateItem(@PathVariable String id, @RequestBody ItemBody itemBody){
 Integer idInt= Integer.valueOf(id);
        ItemEntity itemEntity = new ItemEntity(idInt,
                itemBody.getName(),
                itemBody.getType(),
                itemBody.getPrice(),
                itemBody.getSpec().getCpu(),
                itemBody.getSpec().getCapacity());

        ItemEntity itemEntityUpdated= electronicStoreItemRepository.updateItemEntity(idInt, itemEntity);

        Item itemUpdated= new Item(itemEntityUpdated);
        return itemUpdated;
    }
//✌🏻 ElectronicStoreItemRepository에서 `updateItemEntity()` 구현
public interface ElectronicStoreItemRepository {
    List<Item> findAllItems();

    Integer saveItem(ItemBody itemBody);

    ItemEntity updateItemEntity(Integer idInt, ItemEntity itemEntity);
}
//🤙🏻 ElectronicStoreItemJdbcDao에서 `updateItemEntity()` Override
    @Override
    public ItemEntity updateItemEntity(Integer idInt, ItemEntity itemEntity) {
        jdbcTemplate.update("UPDATE item"+
                "SET name= ? , + type= ?, price = ?, cpu= ?, capacity = ?" +
                "WHERE id= ?",
                itemEntity.getName(),
                itemEntity.getType(),
                itemEntity.getPrice(),
                itemEntity.getCpu(),
                itemEntity.getCapacity(),
                idInt);

        ItemEntity itemEntityUpdate= jdbcTemplate.queryForObject("SELECT * FROM item WHERE id= ? ", itemEntityRowMapper, idInt);
        return itemEntityUpdate;
```

## ✅ Service Layer

controller layer는 최소한의 작업만 가지고 있어야 한다. <br>
Service Layer로 작업 옮기기 <br>
기존 controller에 있던 비즈니스 로직의 책임을 Service Layer에 위임 <br>
특히 controller에 있는 DAO를 없애서 service에 넣어야 한다. <br>
`DAO: ElectronicStoreItemJdbcDao.java file` <br>

### ☑️ Service 객체

### ☑️ 트랜잭션 개념

> 작업 처리 원자성: 작업들이 아예 몽땅 성공하거나, 하나라도 실패하면 다시 롤백(원상태)되도록 작업들을 하나의 단위로 묶는 것<br>

예를 들어, A계좌에서 B계좌로 돈을 보냈을 때, A계좌는 -10이 되면 B계좌는 +10이 되어야 함. <br>
A계좌만 성공하면 안 됨! <br>
따라서 A, B모두 성공하도록, 하나라도 실패하면 둘 다 실패하는 것임. <br>
따라서 A, B는 **원자성을 띄고**, A, B는 **하나의 작업 단위**이다. <br>

> 트랜잭션: 데이터 처리 원자성을 보장하기 위해 여러 작업들을 하나의 단위로 묶는 것<br>

bean을 통해서 "나 이제 이 작업들 하나의 단위로 묶을건데, 묶어서 관리해줬으면 좋겠어" <br>
`Transaction Manager`이라는 것을 하나 만들어서 관리 <br>

### ✔️ service class 구현 예시

controller에 있는 DAO지우고, service에 구현하기<br>

```java
@Service //service도 bean이다.
public class ElectronicStoreItemService {
    //여기에 DAO를 구현해야 한다.
}
```

```java
//1️⃣ 모든 아이템 조회 GET 위해 list
//controller
    @GetMapping("/items")
    public List<Item> findAllItem(){
        return electronicStoreItemService.findAllItem();
    }

//service
@Service //service도 bean이다.
public class ElectronicStoreItemService {
    //여기에 DAO를 구현해야 한다.
    private ElectronicStoreItemRepository electronicStoreItemRepository;

    //DAO의 생성자
    public ElectronicStoreItemService(ElectronicStoreItemRepository electronicStoreItemRepository) {
        this.electronicStoreItemRepository = electronicStoreItemRepository;
    }

    public List<Item> findAllItem() {
        List<ItemEntity> itemEntities= electronicStoreItemRepository.findAllItems();
        return itemEntities.stream().map(Item::new).collect(Collectors.toList());
    }
}
```

```java
//2️⃣새로운 아이템 등록 POST
//controller
    @PostMapping("/items")
    public String registerItem(@RequestBody ItemBody itemBody){
        Integer itemID= electronicStoreItemService.saveItem(itemBody);
        return "ID:"+ itemID;
    }
//service
    public Integer saveItem(ItemBody itemBody) {
        ItemEntity itemEntity = new ItemEntity(null,
                itemBody.getName(),
                itemBody.getType(),
                itemBody.getPrice(),
                itemBody.getSpec().getCpu(),
                itemBody.getSpec().getCapacity());
        Integer itemID= electronicStoreItemRepository.saveItem(itemEntity);
        return itemID;
    }

```

```java
//3️⃣ Path ID로 아이템 조회 GET

//controller에서는 최소한의 역할만
    @GetMapping("/items/{id}")
    public Item findItemByPathID(@PathVariable String id){
        return electronicStoreItemService.findItemById(id);
    }
//service에서 dao
    public ItemEntity findItemById(String id) {
        Integer idInt= Integer.parseInt(id);
        ItemEntity itemEntity= electronicStoreItemRepository.findItemById(idInt);
        Item item= new Item(itemEntity);
        return item;
    }

//4️⃣ 쿼리 파라미터로 ID 조회, 3️⃣번이랑 service에서 같은 함수 사용
    @GetMapping("/items-query") //GET api/items-query?id=1
    public Item findItemByQueryID(@RequestParam("id") String id){
        return electronicStoreItemService.findItemById(id);
    }
```

```java
// 5️⃣ 여러 ID 쿼리 파라미터로 조회 GET
//controller
    @GetMapping("/items-queries")
    public List<Item> findItemByQueryIds(@RequestParam("id") List<String> ids){
        return electronicStoreItemService.findItemsByIds(ids);
    }
//service
    public List<Item> findItemsByIds(List<String> ids) {
        List<ItemEntity> itemEntities = electronicStoreItemRepository.findAllItems();
        return itemEntities.stream()
                                       .map(Item::new)
                                       .filter((item -> ids.contains(item.getId())))
                                       .collect(Collectors.toList());
    }
```

```java
// 6️⃣ Path ID로 아이템 삭제 DELETE
//controller
        @DeleteMapping("/items/{id}")
        public String deleteItemByPathId(@PathVariable String id){
        electronicStoreItemService.deleteItem(id);
        return "Object with id =" + id + "has been deleted";
    }
//service
    public void deleteItem(String id) {
        Integer idInt = Integer.parseInt(id);
        electronicStoreItemRepository.deleteItem(idInt);
    }
```

```java
//7️⃣ Path ID와 Body로 업데이트 UPDATE
//controller
    @PutMapping("/items/{id}")
    public Item updateItem(@PathVariable String id, @RequestBody ItemBody itemBody){
        return electronicStoreItemService.updateItem(id, itemBody);
    }
//service
    public Item updateItem(String id, ItemBody itemBody) {
        Integer idInt = Integer.valueOf(id);
        ItemEntity itemEntity = new ItemEntity(idInt, itemBody.getName(),
                                               itemBody.getType(), itemBody.getPrice(),
                                               itemBody.getSpec().getCpu(), itemBody.getSpec().getCapacity());

        ItemEntity itemEntityUpdated = electronicStoreItemRepository.updateItemEntity(idInt, itemEntity);

        return new Item(itemEntityUpdated);
    }
```

### ✔️ 트랜잭션 구현 예시

```java
//config파일에 transaction 추가
//transaction할거라고 알려줘야 함
    @Bean
    public PlatformTransactionManager transactionManager() {return new DataSourceTransactionManager(dataSource());
    }
```

```java
//controller
    //💡트랜잭션
    @PostMapping("/items/buy")
    public String buyItem(@RequestBody BuyOrder buyOrder){
        Integer orderItemNums= electronicStoreItemService.buyItems(buyOrder);
        return "This Item was bought " + orderItemNums+ " times.";
    }
```

```java
//우선 store Entity, item Entity 만들어주고
public class StoreSales {
    private Integer id;
    private String storeName;
    private Integer amount;

    public StoreSales(Integer id, String storeName, Integer amount) {
        this.id = id;
        this.storeName = storeName;
        this.amount = amount;
    }

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getStoreName() {
        return storeName;
    }

    public void setStoreName(String storeName) {
        this.storeName = storeName;
    }

    public Integer getAmount() {
        return amount;
    }

    public void setAmount(Integer amount) {
        this.amount = amount;
    }
}

public class ItemEntity {
    //db의 테이블과 1대1 매핑이 된다.
    private Integer id;
    private String name;
    private String type;
    private Integer price;
    private Integer storeId;
    private Integer stock;

    private String cpu;
    private String capacity;

    //id를 기준으로 equals, hashCode구현
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof ItemEntity that)) return false;
        return Objects.equals(id, that.id);
    }

    @Override
    public int hashCode() {
        return Objects.hash(id);
    }

    public ItemEntity(Integer id, String name, String type, Integer price, Integer storeId, Integer stock, String cpu, String capacity) {
        this.id = id;
        this.name = name;
        this.type = type;
        this.price = price;
        this.storeId = null;
        this.stock = 0;
        this.cpu = cpu;
        this.capacity = capacity;
    }

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getType() {
        return type;
    }

    public void setType(String type) {
        this.type = type;
    }

    public Integer getPrice() {
        return price;
    }

    public void setPrice(Integer price) {
        this.price = price;
    }

    public String getCpu() {
        return cpu;
    }

    public void setCpu(String cpu) {
        this.cpu = cpu;
    }

    public String getCapacity() {
        return capacity;
    }

    public void setCapacity(String capacity) {
        this.capacity = capacity;
    }


    public Integer getStoreId() {
        return storeId;
    }

    public void setStoreId(Integer storeId) {
        this.storeId = storeId;
    }

    public Integer getStock() {
        return stock;
    }

    public void setStock(Integer stock) {
        this.stock = stock;
    }
}

```

```java
public class ElectronicStoreItemService {
@Transactional
    public Integer buyItems(BuyOrder buyOrder) {
        // 1. BuyOrder 에서 상품 ID와 수량을 얻어낸다.
        Integer itemId= buyOrder.getItemId();
        Integer itemNums= buyOrder.getItemNums();
        // 2. 상품을 조회하여 수량이 얼마나 있는 지 확인한다.
        ItemEntity itemEntity= electronicStoreItemRepository.findItemById(itemId);

        // (단, 재고가 아예 없거나 매장을 찾을 수 없으면 살 수 없다. )
        if(itemEntity.getStoreId() == null) throw new RuntimeException("No Store Found");
        if(itemEntity.getStock() == 0) throw new RuntimeException("No stock available");

        //실제로 내가 사고싶은 수량
        Integer successBuyItemNums;
        //실제로 내가 사고싶은 수량이 현재 가지고 있는 수량보다 많으면, 현재 가지고 있는 만큼만 살 수 있음
        if(itemNums > itemEntity.getStock()) successBuyItemNums = itemEntity.getStock();
        else successBuyItemNums= itemNums; //아니면 원하는 만큼 살 수 있음

        // 3. 상품의 수량과 가격을 가지고 계산하여 총 가격을 구한다.
        //총 가격 구하는 식
        Integer totalPrice= successBuyItemNums * itemEntity.getPrice();

        // 4️⃣ 상품의 재고에 기존 계산한 재고를 구매하는 수량을 뺸다.
        //db에 반영을 해야 하므로 updateItemStock라는 새로운 메소드 추가
        electronicStoreItemRepository.updateItemStock(itemId, itemEntity.getStock() - successBuyItemNums);

        // 5️⃣ 상품 구매하는 수량 * 가격 만큼 가계 매상으로 올린다.
        StoreSales storeSales= storeSalesRepository.findStoreSalesById(itemEntity.getStoreId());
        storeSalesRepository.updateSalesAmount(itemEntity.getStoreId(), storeSales.getAmount() + totalPrice);

        return successBuyItemNums;
    }

}
```

```java
// 4️⃣ 상품의 재고에 기존 계산한 재고를 구매하는 수량을 뺸다.
//items db에 반영을 해야하므로

//ElectronicStoreItemRepository.java
public interface ElectronicStoreItemRepository {
        void updateItemStock(Integer itemId, Integer stock);
}

//ElectronicStoreItemJdbcDao.java
public class ElectronicStoreItemJdbcDao implements ElectronicStoreItemRepository{
    @Override
    public void updateItemStock(Integer itemId, Integer stock) {
        jdbcTemplate.update("UPDATE item"+
                        "SET stock= ?" +
                        "WHERE id= ?",
                stock, itemId);

    }
}
```

```java
// 5️⃣ 상품 구매하는 수량 * 가격 만큼 가계 매상으로 올린다.
//store_sales db에 반영을 해야 하므로

//StoreSalesRepository.java
public interface StoreSalesRepository {
    StoreSales findStoreSalesById(Integer storeId);

    void updateSalesAmount(Integer storeId, Integer amount);
}

//StoreSalesJdbcDao.java
public class StoreSalesJdbcDao implements StoreSalesRepository {

    private JdbcTemplate jdbcTemplate; //JdbcTemplate필요

    public StoreSalesJdbcDao(JdbcTemplate jdbcTemplate) { //JdbcTemplate 생성자
        this.jdbcTemplate = jdbcTemplate;
    }

    //RowMapper
    static RowMapper<StoreSales> storeSalesRowMapper= (((rs, rowNum)->
            new StoreSales(
                    rs.getInt("id"),
                    rs.getNString("store_name"),
                    rs.getInt("amount")
            )));

    @Override
    public StoreSales findStoreSalesById(Integer storeId) {
        return jdbcTemplate.queryForObject("SELECT * FROM store_sales WHERE id=?" , storeSalesRowMapper, storeId);
    }

    @Override
    public void updateSalesAmount(Integer storeId, Integer amount) {
        jdbcTemplate.update("UPDATE store_sales"+
                        "SET amount= ?" +
                        "WHERE id= ?", amount, storeId);
    }
}

```
