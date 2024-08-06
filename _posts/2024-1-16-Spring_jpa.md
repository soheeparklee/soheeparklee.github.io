---
title: ORM, JPA, Pagination, Dirty Checking
categories: [JAVA, Spring]
tags: [orm, jpa] # TAG names should always be lowercase
---

## ✅ ORM

👎🏻 기존 코드의 한계: SQL을 JAVA안에 삽입해야 하고, rowMapper넣어야 했음 <br>

> ORM: Object Relational Mapping <br>
> maps java object and RDB <br>
> makes object into a DB table <br>

> 영속화: ORM을 적용한 Entity를 구성하는 것을 객체의 table 영속화라고 한다. <br>

- Hibernate
- EclipseLink
- DataNucleus

## ✅ JPA

<img width="358" alt="Screenshot 2024-08-06 at 11 51 55" src="https://github.com/user-attachments/assets/1cfb89d6-04a1-4ea9-a593-565b6b4eedc6">

> JPA: Java Persistence API <br>
> developer does not write SQL himself, JPA API will manage and save DB <br>
> 한마디로 자바의 ORM <br>
> JPA operates between Java application and JDBC <br>

#### ☑️ JPA 내부 구성 요소

✔️ Entity Transaction <br>
✔️ Entity Manager 등장 <br>

#### ☑️ Hibernate

> Hibernate: JPA 구현체<br>

## ✅ 고독 JPA 구현

JPA Entity 조건<br>
<br>

- no args constructor<br>
- getter/setter<br>
- private field<br>
  <br>
  table 명시를 해 주어야 한다.<br>

```java
//기존 ItemEntity
@Getter
@Setter
@AllArgsConstructor
@EqualsAndHashCode(of = "id")
@ToString
@Builder
public class ItemEntity {
    private Integer id;
    private String name;
    private String type;
    private Integer price;
    private Integer storeId;
    private Integer stock;
    private String cpu;
    private String capacity;

    public ItemEntity(Integer id, String name, String type, Integer price, String cpu, String capacity) {
        this.id = id;
        this.name = name;
        this.type = type;
        this.price = price;
        this.storeId = null;
        this.stock = 0;
        this.cpu = cpu;
        this.capacity = capacity;
    }

}
```

```java
//jpa 적용
@Getter
@Setter
@AllArgsConstructor
@EqualsAndHashCode(of = "id")
@ToString
@Builder
@Entity
@Table(name= "item")
public class ItemEntity {

    @Id @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name= "id")
    private Integer id;
    @Column(name= "name", length= 50, nullable = false, unique = true)
    private String name;
    @Column(name= "type", length= 20, nullable = false)
    private String type;
    @Column(name= "price")
    private Integer price;
    @Column(name= "store_id")
    private Integer storeId;
    @Column(name= "stock", columnDefinition = "default 0 CHECK(stock) >= 0")
    private Integer stock;
    @Column(name= "cpu", length = 30)
    private String cpu;
    @Column(name= "capacity", length = 30)
    private String capacity;

    public ItemEntity(Integer id, String name, String type, Integer price, String cpu, String capacity) {
        this.id = id;
        this.name = name;
        this.type = type;
        this.price = price;
        this.storeId = null;
        this.stock= 0;
        this.cpu = cpu;
        this.capacity = capacity;
    }
}
```

```java
//jpa구현 전
@Getter
@Setter
@AllArgsConstructor
@EqualsAndHashCode(of = "id")
@ToString
@Builder

public class StoreSalesEntity {
    private Integer id;
    private String storeName;
    private Integer amount;
}
//jpa 구현 후
@Getter
@Setter
@AllArgsConstructor
@EqualsAndHashCode(of = "id")
@ToString
@Builder
@Entity
@Table(name= "store_sales")
public class StoreSalesEntity {
    @Id @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name= "id")
    private Integer id;
    @Column(name= "store_name", length = 30)
    private String storeName;
    @Column(name= "amount", nullable = false, columnDefinition = "DEFAULT 0 CHECK(amount) =0")
    private Integer amount;
}

```

## ✅ JPA 사용해서 method 자동으로 만들기

```java
//controller
 //jpa사용해서 type으로 item찾기
    @GetMapping("/items-types")
    public List<Item> findItemByTypes(@RequestParam("type") List<String> types){
        List<Item> items= itemService.findItemsByTypes(types);
        return items;
    }

//service
//jpa사용해서 type으로 item찾기

    public List<Item> findItemsByTypes(List<String> types) {
        List<ItemEntity> itemEntities= electronicStoreItemJpaRepository.findItemEntitiesByTypeIn(types);
        return itemEntities.stream().map(ItemMapper.INSTANCE::itemEntityToItem).collect(Collectors.toList());
    }

//ElectronicStoreItemJpaRepository
@Repository
public interface ElectronicStoreItemJpaRepository extends JpaRepository<ItemEntity, Integer> { //id의 type
    List<ItemEntity> findItemEntitiesByTypeIn(List<String> types);
}
```

## ✅ JPA Pagination

페이지 나눠주는 기능<br>

### 모든 아이템 Pagination

```java
//controller
//pagination
    @GetMapping("/items-page")
    public Page<Item> findItemsPagination(Pageable pageable){
        return itemService.findAllWithPageable(pageable);
    }

//service
    public Page<Item> findAllWithPageable(Pageable pageable) {
        Page<ItemEntity> itemEntities= electronicStoreItemJpaRepository.findAll(pageable);
        return itemEntities.map(ItemMapper.INSTANCE::itemEntityToItem);
    }

//ElectronicStoreItemJpaRepository
public interface ElectronicStoreItemJpaRepository extends JpaRepository<ItemEntity, Integer> { //id의 type
    Page<ItemEntity> findAll(Pageable pageable);
}

```

### 조건이 있는 Pagination

```java
//controller
//pagination
    @GetMapping("/items-page")
    public Page<Item> findItemsPagination(@RequestParam("type") List<String> types, Pageable pageable){
        return itemService.findAllWithPageable(types, pageable);
    }
//service
    public Page<Item> findAllWithPageable(List<String> types, Pageable pageable) {
        Page<ItemEntity> itemEntities= electronicStoreItemJpaRepository.findAllByTypeIn(types, pageable);
        return itemEntities.map(ItemMapper.INSTANCE::itemEntityToItem);
    }

    public interface ElectronicStoreItemJpaRepository extends JpaRepository<ItemEntity, Integer> { //id의 type
    Page<ItemEntity> findAllByTypeIn(List<String> types, Pageable pageable);
}
```

## ✅ Dirty Checking

> Within a `transaction` when entity is altered, <br>
> automatically save DB with altered value <br>

```java
@Transactional
public void cancelOrder(Long orderId) {
    //주문 엔티티 조회
    Order order = orderRepository.findOne(orderId);

    //주문 취소
    order.cancel();
}
```

- start `Transaction`
- find `order entity` with `orderId`
- **update** `order entity` with canceled value
- commit `transaction`

There is **no explicit update code**, but **dirty checking** will manage update.

- dirty checking = 변경 감지
- Realizing change in entity ➡️ Apply to DB
