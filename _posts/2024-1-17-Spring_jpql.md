---
title: JPA mapping, JPQL, N+1, PSL
categories: [JAVA, Spring]
tags: [log, logger, logpattern, slf4j] # TAG names should always be lowercase
---

## ✅ JPA mapping, JPQL은 PSA를 따른다.

PSA(Portable Service Abstraction)는 특정 기술에 얽매이지 않는것이다.<br>
예를 들어 JAVA에서 oracle, mysql을 쓰든 oracle, mysql의 문법에 얽매이지 않고 문제 없이 쓰고 싶음.<br>
그래서 JPA, JPQL을 통해서 DB문법에 얽매이지 않는 JAVA코드를 짜는 것이다.<br>

## ✅ JPA mapping

mapping을 하면 서로의 필드를 가져오기가 더 수월해진다.<br>

1. 관계의 다중성<br>

- 1:N @ManyToOne <br>
- N:1 @OneToMany <br>
- 1:1 @OneToOne <br>
- N:M 연결된 두 테이블 사이에 테이블이 있음 <br>

2. 관계의 방향 <br>
   <br>

- 단방향: 기본적으로 단방향 <br>
- 양방향(서로가 서로를 바라보고 있음): 서로가 서로를 참조해야 할 때는 양방향 <br>

3. 관게의 주인<br>
   PK가지고 있는 테이블<br>

#### fetch.LAZY 🆚 fetch.EAGER

- LAZY: getter가 부를 떄 가져오기 <br>
  모두 다 가져올 필요는 없을 때 사용 <br>

- EAGER: fetch할 때 바로 미리 가져다놓기 <br>
  빠르게 동작할 때 필요 <br>

```java
//ItemEntity
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
    //JPA로 table join
    @ManyToOne(fetch= FetchType.EAGER) //내부적으로 storeSales를 가져올 수 있다.
    //FetchType.LAZY로 하면 select만 하고 join은 나중에 한다. 테이블만 불러옴.
    //객체를 빨리빨리 부르기 위해서는 FetchType.EAGER, 굳이 다 부를 필요 없다면 FetchType.LAZY
    @JoinColumn(name= "store_id")
    private StoreSalesEntity storeSalesEntity; //store_id아니고 storeSalesEntity객체를 쓴다.

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
        this.storeSalesEntity = null;
        this.stock= 0;
        this.cpu = cpu;
        this.capacity = capacity;
    }

    //⭐️ storeID can be null
    public Optional<StoreSalesEntity> getStoreSalesEntity() {
        return Optional.ofNullable(storeSalesEntity);
    }

    public void setItemBody(ItemBody itemBody) {
        this.name= itemBody.getName();
        this.type= itemBody.getType();
        this.price= itemBody.getPrice();
        this.cpu= itemBody.getSpec().getCpu();
        this.cpu= itemBody.getSpec().getCapacity();
    }
}
//ItemMapper
//target= storeId ➡️ store
    @Mapping(target= "store", ignore= true)

//ItemService
//이젠 storeID가져오는 것이 아니라 entity전체를 가져온다.
        if(itemEntity.getStoreSalesEntity() == null) throw new RuntimeException("No such store");

        StoreSalesEntity storeSalesEntity= itemEntity.getStoreSalesEntity().orElseThrow(()-> new NotFoundException("No Store with matching ID Found" + itemEntity.getStoreSalesEntity()));
        storeSalesEntity.setAmount(storeSalesEntity.getAmount() + totalPrice); //update
        return buyItemNums;
```

```java

//passenger, user은 서로가 서로를 참조하는데
//주인은 passenger
//user이 passenger을 바라보고 있다.

//UserEntity
public class UserEntity {
    @Id
    @Column(name = "user_id") @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Integer userId;
    @Column(name = "user_name", length = 20)
    private String userName;
    @Column(name = "like_travel_place", length = 30)
    private String likeTravelPlace;
    @Column(name = "phone_num", length = 30)
    private String phoneNum;

    @OneToOne(mappedBy = "userEntity") //passenger에서 나를 userEntity라고 바라보고 있으니까
    private Passenger passenger; //이름은 객체 그 자체

    @Override
    public boolean equals(Object o) {
        if (this == o) {
            return true;
        }
        if (!(o instanceof UserEntity)) {
            return false;
        }

        UserEntity that = (UserEntity) o;

        return userId.equals(that.userId);
    }

    @Override
    public int hashCode() {
        return userId.hashCode();
    }
}

//passenger
public class Passenger {
    @Id
    @Column(name = "passenger_id") @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Integer passengerId;

    @OneToOne(fetch= FetchType.LAZY)
    @JoinColumn (name = "user_id", unique = true)
    private UserEntity userEntity ; //passenger은 무조건 user에 있어야

    @Column(name = "passport_num", length = 50)
    private String passportNum;

}


```

## ✅ JPQL

> JPQL: Java Persistence Query Language
> JPA의 객체지향 쿼리

복잡한 SQL이 필요할 떄 JPQL을 사용해 query<br>
새로운 객체 생성도 가능하다<br>

```java
//controller
    @ApiOperation("userId의 예약한 항공편과 수수료 총합")
    @GetMapping("/users-sum-price")
    public Double findUserFlightSumPrice(
            @ApiParam(name = "user-Id", value = "유저 ID", example = "1")
            @RequestParam("user-id") Integer userId
    )
    {
        Double sum = airReservationService.findUserFlightSumPrice(userId);
        return sum;
    }

//FlightPriceAndCharge
@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
public class FlightPriceAndCharge {
    private Double flightPrice;
    private Double charge;
}

//service
    public Double findUserFlightSumPrice(Integer userId) {
        // 1. flight_price , Charge 구하기
        //jpql에 가져오고 싶은 값을 임시 DTO(FlightPriceAndCharge)에 가져오기
        List<FlightPriceAndCharge> flightPriceAndCharges = reservationJpaRepository.findFlightPriceAndCharge(userId);

        // 2. 모든 Flight_price와 charge의 각각 합을 구하고
        Double flightSum = flightPriceAndCharges.stream().mapToDouble(FlightPriceAndCharge::getFlightPrice).sum();
        Double chargeSum = flightPriceAndCharges.stream().mapToDouble(FlightPriceAndCharge::getCharge).sum();

        // 3. 두개의 합을 다시 더하고 Return
        return flightSum + chargeSum;
    }

//ReservationJpaRepository
//⭐️ JPQL
public interface ReservationJpaRepository extends JpaRepository {
    @Query("SELECT new com.example.supercoding_crud.repository.reservation.FlightPriceAndCharge(f.flightPrice, f.charge) " +
    "FROM Reservation r " +
    " JOIN r.passenger p " +
    "JOIN r.airlineTicket a" +
    "JOIN a.flightList f" +
    "WHERE p.user.userId= :userId")
     List<FlightPriceAndCharge> findFlightPriceAndCharge(Integer userId);
}
```

## ✅ N+1 문제

> 연관 관계가 설정된 entity를 조회하면, 조회된 횟수 만큼 조회 쿼리가 추가로 실행되는 문제 현상

💡 해결 방법: JPQL 만들기, fetch Join<br>
SQL의 불필요한 동작을 막아준다.<br>
<br>
👎🏻 쿼리가 여러번 반복 실행되는 코드, 개선 필요<br>

```java
//controller
    @ApiOperation("전체 stores 정보 검색")
    @GetMapping("/stores")
    public List<StoreInfo> findAllStoreInfo(){
        return ItemService.findAllStoreInfo();
    }
//ItemService
    @Transactional(transactionManager = "tmJpa1")
    public List<StoreInfo> findAllStoreInfo() {
        List<StoreSalesEntity> storeSalesEntity= storeSalesJpaRepository.findAll();
        List<StoreInfo> storeInfos= storeSalesEntity.stream().map(StoreInfo::new).collect(Collectors.toList());
        return storeInfos;
    }

//StoreInfo
@Getter
@NoArgsConstructor
public class StoreInfo {
    private Integer id;
    private String storeName;
    private Integer amount;
    private List<String> itemNames;

    public StoreInfo(StoreSalesEntity storeSalesEntity) {
        this.id = storeSalesEntity.getId();
        this.storeName = storeSalesEntity.getStoreName();
        this.amount = storeSalesEntity.getAmount();
        this.itemNames = storeSalesEntity.getItemEntities().stream().map(ItemEntity::getName).collect(Collectors.toList());
    }
}
//storeSalesEntity
public class StoreSalesEntity {
    @Id @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name= "id")
    private Integer id;
    @Column(name= "store_name", length = 30)
    private String storeName;
    @Column(name= "amount", nullable = false, columnDefinition = "DEFAULT 0 CHECK(amount) =0")
    private Integer amount;

    @OneToMany(mappedBy = "StoreSalesEntity")
    private List<ItemEntity> itemEntities;
}

```

👍🏻 해결 방법: JPQL: fetch Join

```java
//새로운 JPQL을 StoreSalesJpaRepository에 추가한다.
@Repository
public interface StoreSalesJpaRepository extends JpaRepository<StoreSalesEntity, Integer> {
    @Query("SELECT s FROM StoreSalesEntity s JOIN FETCH s.itemEntities")
    List<StoreSalesEntity> findAllFetchJoin();
}


//service
    @Transactional(transactionManager = "tmJpa1")
    public List<StoreInfo> findAllStoreInfo() {
        List<StoreSalesEntity> storeSalesEntity= storeSalesJpaRepository.findAllFetchJoin();
        List<StoreInfo> storeInfos= storeSalesEntity.stream().map(StoreInfo::new).collect(Collectors.toList());
        return storeInfos;
    }

//storeSalesEntity는 똑같음
```
