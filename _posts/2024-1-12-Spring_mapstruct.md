---
title: Mapstruct Utility Library, Swagger
categories: [JAVA, Spring]
tags: [mapstuct, mapper, mapping, meta, named] # TAG names should always be lowercase
---

### 👎🏻 기존 코드 한계:

DTO, Entity를 무조건 다른 클래스로 구현하다보니, <br>
사실 두 파일 간 겹치는 부분이 많은데...두 클래스 간 코드가 비슷함. <br>
또 두 파일 간 생성자가 비슷함. <br>
<br>

👌🏻 **Mapstruct**으로 해결! <br>
🕵🏻‍♂️ Mapstruct은 **runtime meta programming** <br>
annotation 프로세서가 컴파일 이후 자동으로 코드를 생성해준다. <br>

## 🔗 Mapstruct

> 목적: 객체 간 편안한 매핑 <br>
> Mapstruct는 이름이 같은 필드는 자동으로 매핑을 해 준다. <br>
> Mapstruct은 interface <br>
> ❗️❗️❗️ 생성하는 target은 **setter**가 무조건 있어야 한다. <br>

💡 default값을 정해줄 수 있다. <br>
default value: 이 필드 값이 없을 때 기본으로 입력되는 값 <br>
💡 custom 함수를 실행할 수 있다. <br>

```java
    //🔗Mapstruct전에 이렇게 선언되어 있었음
    //itemEntity와 Item이 매우 비슷하다.
    //itemEntity를 받아 Item으로 만들기
    //⭐️ 생성자로 db에서 들어온 데이터 JAVA에서 원하는 형식으로 만들기
    public Item (ItemEntity itemEntity){
        this.id= itemEntity.getCapacity();
        this.type= itemEntity.getType();
        this.price= itemEntity.getPrice();
        this.name= itemEntity.getName();
        this.spec= new Spec(itemEntity.getCpu(), itemEntity.getCapacity());
    }


    //🔗Mapstruct을 사용해 ItemMapper을 만든다.
@Mapper
public interface ItemMapper {
    //싱글톤
    ItemMapper INSTANCE= Mappers.getMapper(ItemMapper.class);
    //메소드
    //item을 받아서 itemEntity에 자동으로 매핑해 만들어준다.
    @Mapping(target= "spec.cpu", source= "cpu")
    @Mapping(target= "spec.capacity", source= "capacity")
    Item itemEntityToItem(ItemEntity itemEntity);
    //근데 Item 생성자보면 spec의 경우 좀 특이함. spec안에 Cpu, Capacity있음
    //this.spec= new Spec(itemEntity.getCpu(), itemEntity.getCapacity());
    //이렇게 getCpu랑 getCapacity를 합쳐야 한다.
    //따라서 annotatoin에 명시해주기 @Mapping
}

//이제 ItemEntity를 Item으로 바꾸는 코드에서 🔗Mapstruct 사용
public class ElectronicStoreItemService {
    public List<Item> findAllItem() {
        List<ItemEntity> itemEntities= electronicStoreItemRepository.findAllItems();
        //🔗Mapstruct
        return itemEntities.stream().map(ItemMapper.INSTANCE::itemEntityToItem).collect(Collectors.toList());
    }

    public List<Item> findAllItemsByIds(List<String> ids) {
        List<ItemEntity> itemEntities = electronicStoreItemRepository.findAllItems();
        return itemEntities.stream()
        //이렇게 🔗 Mapstruct 사용
                .map(ItemMapper.INSTANCE::itemEntityToItem)
                .filter((item)->ids.contains(item.getId()))
                .collect(Collectors.toList());
    }

    public Item findItemById(String id) {
        Integer idInt= Integer.parseInt(id);
        ItemEntity itemEntity= electronicStoreItemRepository.findItemById(idInt);
        //🔗Mapstuct
//        Item item= new Item(itemEntity); //기존 코드
        Item item= ItemMapper.INSTANCE.itemEntityToItem(itemEntity);

        return item;
    }
}
```

```java
//ticket과 airline Ticket이 매우 비슷함
//🔗Mapstruct로 연결
@Mapper
public interface TicketMapper {
    //singleTon
    TicketMapper INSTANCE= Mappers.getMapper(TicketMapper.class);
    //method
    @Mapping(target= "depart", source="departureLocation")
    @Mapping(target= "arrival", source="arrivalLocation")
    @Mapping(target= "departTime", source="departureAt")
    @Mapping(target= "returnTime", source="returnAt")

    Ticket airlineTicketToTicket(AirlineTicket airlineTicket);
}

//@mapping 이유
//AirlineTicket이랑 Ticket이랑 조금 다른데 맞춰주기 위해서
public class AirlineTicket {
    private Integer ticketId;
    private String ticketType;
    private String departureLocation;
    private String arrivalLocation;
    private LocalDateTime departureAt;
    private LocalDateTime returnAt;
}

public class Ticket {
    private String depart;
    private String arrival;
    private String departureTime;
    private String returnTime;
    private Integer ticketId;

//앗 근데 departureTime, returnTime원하는 형식이 있음
//💡 custom 함수를 실행할 수 있다.
    private static DateTimeFormatter formatter= DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");

    public Ticket(AirlineTicket airlineTicket) {
        this.depart = airlineTicket.getDepartureLocation();
        this.arrival = airlineTicket.getArrivalLocation();
        this.departureTime = airlineTicket.getDepartureAt().format(formatter); //원하는 형식이 있음
        this.returnTime = airlineTicket.getReturnAt().format(formatter);} //원하는 형식이 있음
}

//💡 custom 함수를 Mapper에 추가하여 수정
@Mapper
public interface TicketMapper {
    //singleTon
    TicketMapper INSTANCE= Mappers.getMapper(TicketMapper.class);
    //method
    @Mapping(target= "depart", source="departureLocation")
    @Mapping(target= "arrival", source="arrivalLocation")
    @Mapping(target= "departTime", source="departureAt", qualifiedByName = "convert") //💡 custom 함수 추가
    @Mapping(target= "returnTime", source="returnAt", qualifiedByName = "convert") //💡 custom 함수 추가

    Ticket airlineTicketToTicket(AirlineTicket airlineTicket);
    // 💡 formatter를 먼저 추가하고
    static DateTimeFormatter formatter= DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");

    //💡 custom 함수 추가
    @Named("convert")
    static String localDateTimeToString(LocalDateTime localDateTime){
        return localDateTime.format(formatter);
    }
}


```
