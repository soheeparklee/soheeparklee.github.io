---
title: Test Code
categories: [JAVA, Spring]
tags: [test] # TAG names should always be lowercase
---

## ✅ Test Code

> 반복적인 검증 과정을 줄이기 위한 코드
> test 단워: 클래스의 단위가 이상적인 단위 또는 메서드 단위

<img width="734" alt="스크린샷 2024-01-18 오후 5 05 08" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/eba1462c-3c32-463c-95f5-7c92e04d5beb">

- Unit Test: 코드 일부분 테스트
- Integration Test
- Acceptance Test

### ☑️ how to use

✔️ JAVA Test JUNIT Annotation
@ Test
@BeforeEach
@DisplayName
✔️ AssertJ
✔️ Given - When - Then

## ✅ Pure Unit Test

> 외부 의존성이 없는 소스 코드 검증
> 외부 라이브러리 동작 검증

```java
//mapper
@Mapper
public interface ItemMapper {
    ItemMapper INSTANCE = Mappers.getMapper(ItemMapper.class);

    @Mapping(target = "spec.cpu", source = "cpu")
    @Mapping(target= "spec.capacity", source= "capacity")
    Item itemEntityToItem(ItemEntity itemEntity);

    @Mapping(target= "cpu", source= "itemBody.spec.cpu")
    @Mapping(target= "capacity", source= "itemBody.spec.capacity")
    @Mapping(target= "store", ignore= true)
    @Mapping(target= "stock", expression ="java(0)")
    ItemEntity idAndItemBodyToItemEntity(Integer id, ItemBody itemBody);
}
```

```java
//ItemMapperUtilTest
class ItemMapperUtilTest {
    @DisplayName("ItemEntity에 있는 ItemEntityToItem method test")
    @Test
    void itemEntityToItem() {
        //given
        ItemEntity itemEntity = ItemEntity.builder()
                .name("name")
                .type("type")
                .id(1)
                .price(1000)
                .stock(0)
                .cpu("CPU 1")
                .capacity("100G")
                .storeSalesEntity(new StoreSalesEntity())
                .build();

        //when
        Item item= ItemMapper.INSTANCE.itemEntityToItem(itemEntity);
        //then
        log.info("item created" + item);
        assertEquals(itemEntity.getPrice(), item.getPrice());
        assertEquals(itemEntity.getId().toString(), item.getId());
        assertEquals(itemEntity.getCpu(), item.getSpec().getCpu());
        assertEquals(itemEntity.getCapacity(), item.getSpec().getCapacity());
    }
}
```

## ✅ Mocking Unit Test

> 서비스, 비스니스 로직 테스트
> 하나의 Mocking Unit Test에서 여러가지 경우를 한 번에 테스트할 수 있다.

#### ❓ 그런데 서비스 로직에는 repository를 의존하고 있는데? 의존성 문제?

> 가짜(mock) repository를 넣어준다.

```java
@Slf4j
class AirReservationServiceUnitTest {
    //user Repository, airline Repository 필요
    @Mock
    private UserJpaRepository userJpaRepository;
    @Mock
    private AirlineTicketJpaRepository airlineTicketJpaRepository;
    @InjectMocks //두 mock repository를 이 service에 넣어주세요
    private AirReservationService airReservationService;

    @BeforeEach
    public void setUp(){
        MockitoAnnotations.openMocks(this);
    }

    @DisplayName("airlineTicket에 해당하는 user. ticket 모두 존재")
    @Test
    void findUserFavoritePlaceTicketsCaseSuccess() {
        //given
        Integer userId= 5;
        String likePlace= "파리";
        String ticketType= "왕복";

        UserEntity userEntity= UserEntity.builder() //test위해 하나 만들어서 넣어줘야 함
                .userId(userId)
                        .likeTravelPlace(likePlace)
                                .userName("name1")
                                        .phoneNum("1234")
                                                .build();

        List<AirlineTicket> airlineTickets = Arrays.asList( //test위해 하나 만들어서 넣어줘야 함
                AirlineTicket.builder()
                        .ticketId(1)
                        .arrivalLocation(likePlace)
                        .ticketType(ticketType)
                        .build(),
                AirlineTicket.builder()
                        .ticketId(2)
                        .arrivalLocation(likePlace)
                        .ticketType(ticketType)
                        .build(),
                AirlineTicket.builder()
                        .ticketId(3)
                        .arrivalLocation(likePlace)
                        .ticketType(ticketType)
                        .build(),
                AirlineTicket.builder()
                        .ticketId(4)
                        .arrivalLocation(likePlace)
                        .ticketType(ticketType)
                        .build()
        );
        //when
        when(userJpaRepository.findById(any())).thenReturn(Optional.of(userEntity)); //어떤 값이 들어가든간에
        when(airlineTicketJpaRepository.findAirlineTicketsByArrivalLocationAndTicketType(likePlace, ticketType))
                .thenReturn(airlineTickets);
        //then
        List<Ticket> tickets= airReservationService.findUserFavoritePlaceTicket(userId, ticketType);
        log.info("tickets" + tickets);
        assertTrue(
                tickets.stream().map(Ticket::getArrival).allMatch((arrival)->arrival.equals(likePlace))
        );
    }

    @DisplayName("airlineTicket에 왕복/편도 ticketType 틀린 경우")
    @Test
    void findUserFavoritePlaceTicketsCaseWrongTicketType() {
        //given
        Integer userId= 5;
        String likePlace= "파리";
        String ticketType= "!@#$%^&*()";

        UserEntity userEntity= UserEntity.builder() //test위해 하나 만들어서 넣어줘야 함
                .userId(userId)
                .likeTravelPlace(likePlace)
                .userName("name1")
                .phoneNum("1234")
                .build();

        List<AirlineTicket> airlineTickets = Arrays.asList( //test위해 하나 만들어서 넣어줘야 함
                AirlineTicket.builder()
                        .ticketId(1)
                        .arrivalLocation(likePlace)
                        .ticketType(ticketType)
                        .build(),
                AirlineTicket.builder()
                        .ticketId(2)
                        .arrivalLocation(likePlace)
                        .ticketType(ticketType)
                        .build(),
                AirlineTicket.builder()
                        .ticketId(3)
                        .arrivalLocation(likePlace)
                        .ticketType(ticketType)
                        .build(),
                AirlineTicket.builder()
                        .ticketId(4)
                        .arrivalLocation(likePlace)
                        .ticketType(ticketType)
                        .build()
        );
        //when
        when(userJpaRepository.findById(any())).thenReturn(Optional.of(userEntity)); //어떤 값이 들어가든간에
        when(airlineTicketJpaRepository.findAirlineTicketsByArrivalLocationAndTicketType(likePlace, ticketType))
                .thenReturn(airlineTickets);
        //then
        assertThrows(InvalidValueExceptions.class, //error뜨도록
                () -> airReservationService.findUserFavoritePlaceTicket(userId, ticketType));

    }

    @DisplayName("User를 찾을 수 없는 경우")
    @Test
    void findUserFavoritePlaceTicketsCaseUserNotFound() {
        //given
        Integer userId= 5;
        String likePlace= "파리";
        String ticketType= "왕복";

        UserEntity userEntity= null;

        List<AirlineTicket> airlineTickets = Arrays.asList( //test위해 하나 만들어서 넣어줘야 함
                AirlineTicket.builder()
                        .ticketId(1)
                        .arrivalLocation(likePlace)
                        .ticketType(ticketType)
                        .build(),
                AirlineTicket.builder()
                        .ticketId(2)
                        .arrivalLocation(likePlace)
                        .ticketType(ticketType)
                        .build(),
                AirlineTicket.builder()
                        .ticketId(3)
                        .arrivalLocation(likePlace)
                        .ticketType(ticketType)
                        .build(),
                AirlineTicket.builder()
                        .ticketId(4)
                        .arrivalLocation(likePlace)
                        .ticketType(ticketType)
                        .build()
        );
        //when
        when(userJpaRepository.findById(any())).thenReturn(Optional.ofNullable(userEntity)); //어떤 값이 들어가든간에
        when(airlineTicketJpaRepository.findAirlineTicketsByArrivalLocationAndTicketType(likePlace, ticketType))
                .thenReturn(airlineTickets);
        //then
        assertThrows(NotFoundException.class, //error뜨도록
                () -> airReservationService.findUserFavoritePlaceTicket(userId, ticketType));

    }
}
```

## ✅ Integration Test: Slice Test

> 원하는 layer만 테스트
> @DataJapTest
> 실제 해당 Layer에 속하는 Bean만 호출, 더 빠르게 실행 가능

```java
class ReservationJpaRepositorJpaTest {
    @Autowired
    private ReservationJpaRepository reservationJpaRepository; //생성자 안 쓰고 @Autpwired
    //repository에 해당되는 bean만 호출 가능

    @Autowired
    private PassengerJpaRepository passengerJpaRepository;

    @Autowired
    private AirlineTicketJpaRepository airlineTicketJpaRepository;

    @DisplayName("ReservationRepository로 항공편 가격과 수수료 가격 검색")
    @Test
    void findFlightPriceAndCharge() {
        //Given
        Integer userId = 10;
        //When
        List<FlightPriceAndCharge> flightPriceAndCharges= reservationJpaRepository.findFlightPriceAndCharge(userId);

        //Then
        log.info("result" + flightPriceAndCharges);
    }

    @DisplayName("Reservation 에약 진행")
    @Test
    void saveReservation(){
        //Given
        Integer userId=10;
        Integer ticketId = 5;
        Passenger passenger= passengerJpaRepository.findPassengerByUserUserId(userId).get();
        AirlineTicket airlineTicket= airlineTicketJpaRepository.findById(5).get();

        //When
        Reservation reservation= new Reservation(passenger, airlineTicket);
        Reservation res= reservationJpaRepository.save(reservation);
        //Then
        log.info("reservation" + res);
        assertEquals(res.getPassenger(), passenger);
        assertEquals(res.getAirlineTicket(), airlineTicket);
    }
}
```

## ✅ Acceptance Test Mock MVC

postman안하고도 바로 테스트 가능

```java
class AirReservationControllerSpringTest {
    @Autowired
    private MockMvc mockMvc;
    @DisplayName("Find Airline Ticket Success")
    @Test
    void findAirlineTickets() throws Exception {
        //Given
        Integer userId = 5;
        String ticketType= "왕복";
        //When & Then
        //AcceptanceTest 일 때는 When & Then 합쳐서 진행
        String content= mockMvc.perform(
                get("/v1/api/air-reservation/tickets") //api요청
                        .param("user-Id", userId.toString())
                        .param("airline-ticket-type", ticketType)
                        .contentType(MediaType.APPLICATION_JSON))
                        .andExpect(status().isOk())
                        .andReturn().getResponse().getContentAsString(StandardCharsets.UTF_8);

        log.info("결과: " + content);

    }
}
```
