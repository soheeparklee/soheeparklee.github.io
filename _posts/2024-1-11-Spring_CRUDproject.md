---
title: Spring CRUD
categories: [JAVA, Spring]
tags: [] # TAG names should always be lowercase
---

## ✅ 순서

1. Repository interface, service bean 정의 <br>
2. REST API참고하여 Controller부터 요구사항 코드로 정의 <br>
3. DAO -> Service -> Controller순으로 구현 채우기 <br>

## ✅ 유저 A가 선호하는 여행지의 왕복 항공권 여러개 발견

이 때 왕복 항공권은 출발지/도착지, 출국시간/도착시간 기록<br>
<br>

- 메소드: GET <br>
- HTTP query parameter: user_id, airline_ticket_type <br>
- HTTP response: depart, arrival, departure_time, return_time, ticket_id <br>
- transaction은 필요 없음, 그냥 테이블 read하면 되니까 <br>

### ☑️ 순서

#### Config 파일에 dataSource, jdbcTemplate 추가

```java
    @Bean
    public DataSource dataSource2(){
        DriverManagerDataSource dataSource = new DriverManagerDataSource();
        dataSource.setUsername("root");
        dataSource.setPassword("12341234");
        dataSource.setDriverClassName("com.mysql.cj.jdbc.Driver");
        dataSource.setUrl("jdbc:mysql://localhost:3306/chapter_97?useUnicode=true&characterEncoding=UTF-8");
        return dataSource;
    }

        @Bean
    public JdbcTemplate jdbcTemplate2() { return new JdbcTemplate(dataSource2()); }
```

#### Controller

```java
@RestController
@RequestMapping("/v1/api/air-reservation")
public class AirReservationController {

    private AirReservationService airReservationService;

    public AirReservationController(AirReservationService airReservationService) {
        this.airReservationService = airReservationService;
    }

    @GetMapping("/tickets")
    public TicketResponse findAirlineTickets(@RequestParam("user-Id") Integer userId,
                                             @RequestParam("airline-ticket-type") String ticketType ){
        List<Ticket> tickets = airReservationService.findUserFavoritePlaceTickets(userId, ticketType);
        return new TicketResponse(tickets);
}
```

#### Service

```java
@Service
public class AirReservationService {

    private UserRepository userRepository;
    private AirlineTicketRepository airlineTicketRepository;

    public AirReservationService(UserRepository userRepository, AirlineTicketRepository airlineTicketRepository) {
        this.userRepository = userRepository;
        this.airlineTicketRepository = airlineTicketRepository;
    }

    public List<Ticket> findUserFavoritePlaceTickets(Integer userId, String ticketType) {
      //DB를 인식
        //user가 선호하는 여행지는 UserRepository에 들어있고, ticket은 airline_ticket repository에 들어있음
        //지금 필요한 respository: UserRepository, airline_ticket repository
        //따라서 repository에 각각 파일 만들어주었음

        //1. 유저id로 유저를 가져와서 유저가 선호하는 여행지를 알아낸다.
        //2. 선호하는 여행지와 ticketType으로 Airplane Ticket Table에서 필요한 airline ticket을 가져온다.
        //3. 이 둘의 정보를 조합해 Ticket DTO를 만든다.
        UserEntity userEntity = userRepository.findUserById(userId);
        String likePlace = userEntity.getLikeTravelPlace();

        List<AirlineTicket> airlineTickets
                = airlineTicketRepository.findAllAirlineTicketsWithPlaceAndTicketType(likePlace, ticketType);
        //airReservationService에 새로운 생성자 만들어주어야 한다.
        //airlineTickets을 받아와서 ticket을 만드는 생성자
        List<Ticket> tickets = airlineTickets.stream().map(Ticket::new).collect(Collectors.toList());
        return tickets;
    }
    }
}
```

#### DTO: TicketResponse

⭐️ empty constructor, getter <br>

```java
public class TicketResponse {
    private List<Ticket> tickets;

    public TicketResponse(List<Ticket> tickets) {
        this.tickets = tickets;
    }

    public TicketResponse() {
    }

    public List<Ticket> getTickets() {
        return tickets;
    }
}
```

#### DTO: Ticket

```java
@JsonNaming(PropertyNamingStrategies.SnakeCaseStrategy.class) //snakeCase로 return할 수 있도록
public class Ticket {
    private String depart;
    private String arrival;
    private String departureTime;
    private String returnTime;
    private Integer ticketId;

    public Ticket() {
    }

    private static DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss"); //date형식으로 바꿔줘야 함
    public Ticket(AirlineTicket airlineTicket){
        this.ticketId = airlineTicket.getTicketId();
        this.depart = airlineTicket.getDepartureLocation();
        this.arrival = airlineTicket.getArrivalLocation();
        this.departureTime = airlineTicket.getDepartureAt().format(formatter); //date형식
        this.returnTime = airlineTicket.getReturnAt().format(formatter);

    }

    public String getDepart() {
        return depart;
    }

    public String getArrival() {
        return arrival;
    }

    public String getDepartureTime() {
        return departureTime;
    }

    public String getReturnTime() {
        return returnTime;
    }

    public Integer getTicketId() {
        return ticketId;
    }
}
```

#### User Entity

⭐️ getter, setter, equals, hash, 채워져있는 constructor

```java
public class UserEntity {
    private Integer userId;
    private String userName;
    private String likeTravelPlace;
    private String phoneNum;

    public UserEntity(Integer userId, String userName, String likeTravelPlace, String phoneNum) {
        this.userId = userId;
        this.userName = userName;
        this.likeTravelPlace = likeTravelPlace;
        this.phoneNum = phoneNum;
    }

    public Integer getUserId() {
        return userId;
    }

    public void setUserId(Integer userId) {
        this.userId = userId;
    }

    public String getUserName() {
        return userName;
    }

    public void setUserName(String userName) {
        this.userName = userName;
    }

    public String getLikeTravelPlace() {
        return likeTravelPlace;
    }

    public void setLikeTravelPlace(String likeTravelPlace) {
        this.likeTravelPlace = likeTravelPlace;
    }

    public String getPhoneNum() {
        return phoneNum;
    }

    public void setPhoneNum(String phoneNum) {
        this.phoneNum = phoneNum;
    }

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

```

#### UserRepository

```java
public interface UserRepository {
    UserEntity findUserById(Integer userId);
}
```

#### User jdbc Template

```java
@Repository
public class UserJdbcTemplateDao implements UserRepository {

    private JdbcTemplate jdbcTemplate;

    public UserJdbcTemplateDao(@Qualifier("jdbcTemplate2") JdbcTemplate jdbcTemplate) {
        this.jdbcTemplate = jdbcTemplate;
    }

    static RowMapper<UserEntity> userEntityRowMapper = ((rs, rowNums) ->
            new UserEntity(
                    rs.getInt("user_id"),
                    rs.getNString("user_name"),
                    rs.getNString("like_travel_place"),
                    rs.getNString("phone_num")
            ));


    @Override
    public UserEntity findUserById(Integer userId) {
        return jdbcTemplate.queryForObject("SELECT * FROM users WHERE user_id = ?", userEntityRowMapper, userId);
    }
}
```

#### AirlineTicket

```java
public class AirlineTicket {
    private Integer ticketId;
    private String ticketType;
    private String departureLocation;
    private String arrivalLocation;
    private LocalDateTime departureAt;
    private LocalDateTime returnAt;
    private Double tax;
    private Double totalPrice;

    public AirlineTicket() {
    }

    public AirlineTicket(Integer ticketId, String ticketType, String departureLocation, String arrivalLocation, Date departureAt, Date returnAt, Double tax, Double totalPrice) {
        this.ticketId = ticketId;
        this.ticketType = ticketType;
        this.departureLocation = departureLocation;
        this.arrivalLocation = arrivalLocation;
        this.departureAt = departureAt.toLocalDate().atStartOfDay();
        //dataType을 맞춰줘야 한다.
        //sql에서 date가져와야 한다.
        this.returnAt = returnAt.toLocalDate().atStartOfDay();
        this.tax = tax;
        this.totalPrice = totalPrice;
    }

    public Integer getTicketId() {
        return ticketId;
    }

    public void setTicketId(Integer ticketId) {
        this.ticketId = ticketId;
    }

    public String getDepartureLocation() {
        return departureLocation;
    }

    public void setDepartureLocation(String departureLocation) {
        this.departureLocation = departureLocation;
    }

    public String getArrivalLocation() {
        return arrivalLocation;
    }

    public void setArrivalLocation(String arrivalLocation) {
        this.arrivalLocation = arrivalLocation;
    }

    public String getTicketType() {
        return ticketType;
    }

    public void setTicketType(String ticketType) {
        this.ticketType = ticketType;
    }

    public LocalDateTime getDepartureAt() {
        return departureAt;
    }

    public void setDepartureAt(LocalDateTime departureAt) {
        this.departureAt = departureAt;
    }

    public LocalDateTime getReturnAt() {
        return returnAt;
    }

    public void setReturnAt(LocalDateTime returnAt) {
        this.returnAt = returnAt;
    }

    public Double getTax() {
        return tax;
    }

    public void setTax(Double tax) {
        this.tax = tax;
    }

    public Double getTotalPrice() {
        return totalPrice;
    }

    public void setTotalPrice(Double totalPrice) {
        this.totalPrice = totalPrice;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) {
            return true;
        }
        if (!(o instanceof AirlineTicket)) {
            return false;
        }

        AirlineTicket that = (AirlineTicket) o;

        return ticketId.equals(that.ticketId);
    }

    @Override
    public int hashCode() {
        return ticketId.hashCode();
    }
}
```

#### AirlineTicketRepository

```java
public interface AirlineTicketRepository {
    List<AirlineTicket> findAllAirlineTicketsWithPlaceAndTicketType(String likePlace, String ticketType);
}
```

#### AirlineTicketJdbcTemplateDao

```java
@Repository
public class AirlineTicketJdbcTemplateDao implements AirlineTicketRepository {
    private JdbcTemplate jdbcTemplate;

    public AirlineTicketJdbcTemplateDao(@Qualifier("jdbcTemplate2") JdbcTemplate jdbcTemplate) {
        this.jdbcTemplate = jdbcTemplate;
    }

    static RowMapper<AirlineTicket> airlineTicketRowMapper = (((rs, rowNum) ->
            new AirlineTicket(
                    rs.getInt("ticket_id"),
                    rs.getString("ticket_type"),
                    rs.getNString("departure_loc"),
                    rs.getNString("arrival_loc"),
                    rs.getDate("departure_at"), //DateTime을 localDateTime으로 바꿔줘야
                    //이를 위해 AirlineTicket 생성자에서 Date를 받도록 수정한다.
                    rs.getDate("return_at"),
                    rs.getDouble("tax"),
                    rs.getDouble("total_price")
            )
    ));

    @Override
    public List<AirlineTicket> findAllAirlineTicketsWithPlaceAndTicketType(String likePlace, String ticketType) {
        return jdbcTemplate.query("SELECT * FROM airline_ticket " +
                                  "WHERE arrival_loc = ? AND ticket_type = ?", airlineTicketRowMapper, likePlace, ticketType);
    }
}

```

## ✅ 유저 A는 항공편 가격과 수수료 뿐만 아니라 세금이 포함된 해당 항공권의 가격을 확인하고 예약을 진행할 수 있다.

- 메소드: POST <br>
- HTTP request body: user_id, arline_ticket_id <br>
- HTTP response: 항공편 별(Price, charge), tax total_price, 예약 성공 여부 <br>

### ☑️ 순서

1. controller에 필요한 요구사항 구현 <br>
2. DTO 구현: empty constructor, getter, 또 jsonNaming <br>
3. 구체적인 실행 메소드는 service에게 넘긴다. @Service <br>
4. service는 받아서 메소드를 정의하고, 필요한 repository고민 <br>
5. 필요한 repository구현 repository는 interface <br>
6. repository구현 후에는 service에 필드로 가져와야 함, 그리고 생성자 구현해줘야 한다. <br>
7. service에서 db와 매핑 위한 entitiy 구현: 필드 다 있는 constructor, getter, setter, equals, hash <br>
8. repository를 실제로 실행하기 위한 jdbc Template <br>
   이 파일의 이름은 `Dao`일 것이고 @Repository하며 repository interface를 implement 한다. <br>
   db에서 정보 얻어오기 위해 RowMapper(rs, rowNums) <br>
   또 repository에 정의된 메소드를 Override <br>
9. 결과를 나타내는 DTO 마지막으로 만들기 <br>

#### 1. controller에 필요한 요구사항 구현

```java

    //controller은 service로 다 위임했음.
    //service에다가 makeReservation메소드 만들어줘~
// @RestController
// @RequestMapping("/v1/api/air-reservation")
// public class AirReservationController {
    @PostMapping("/reservations")
    public ReservationResult makeReservation(@RequestBody ReservationRequest reservationRequest){
        return airReservationService.makeReservation(reservationRequest);
    }
// }
```

🔴 그럼 여기서 빨간 줄 생긴다. <br>

- Reservation Result ➡️ DTO <br>
- ReservationRequest ➡️ DTO <br>
- airReservationService ➡️ Service Layer <br>
- makeReservation ➡️ method <br>

#### 2.DTO 구현: empty constructor, getter, 또 jsonNaming

- Reservation Result(마지막에 결과 저장할 DTO) ➡️ 앤 마지막 9번에서 구현 <br>
- ReservationRequest <br>

```java
//⭐️DTO
@JsonNaming(PropertyNamingStrategies.SnakeCaseStrategy.class)
public class ReservationRequest {
    //⭐️DTO는 필드와 빈 생성자, 게터가진다.
    private Integer userId;
    private Integer airlineTIcketId;

    public ReservationRequest() {
    }

    public Integer getUserId() {
        return userId;
    }

    public Integer getAirlineTIcketId() {
        return airlineTIcketId;
    }
}

```

#### 3.구체적인 실행 메소드는 service에게 넘긴다. @Service

- airReservationService ➡️ Service Layer <br>
- makeReservation ➡️ method <br>

```java
@Service
public class AirReservationService {
    //⭐️repository구현 후에는 service에 가져와야 함
    private ReservationRepository reservationRepository;
    private PassengerRepository passengerRepository;

    //⭐️️repository 두 개 추가 되었으니까 생성자도 새로 만듦, update
    public AirReservationService(UserRepository userRepository, AirlineTicketRepository airlineTicketRepository, ReservationRepository reservationRepository, PassengerRepository passengerRepository) {
        this.userRepository = userRepository;
        this.airlineTicketRepository = airlineTicketRepository;
        this.reservationRepository = reservationRepository;
        this.passengerRepository = passengerRepository;
    }

    //⭐️ controller에서 service에 메소드 만들라고 시킴
    //   메소드 만들어놨으니 이제 repository만들러 가야지
    @Transactional(transactionManager = "tm2")
    public ReservationResult makeReservation(ReservationRequest reservationRequest) {
        //어떤 repository가 필요할까?
        // reservation repository, passenger repository, flight, airline_ticket 두 개의 테이블을 join해서 한 개의 repository로 가지고 와야지
        //1. reservation을 만들어야 한다.
        //2. 이를 위해 passenger repository에서 passenger 가져와야 한다.
        //3. passenger을 가져오기 위해서는 userId, airline_ticket_id가 필요하다.
        //⭐️DTO에서 getter로 가져온다.
        Integer userId= reservationRequest.getUserId();
        Integer airlineTicketId= reservationRequest.getAirlineTIcketId();
        //4. 드디어 passenger가져오기,
        //5. Passenger은 Entity여야 한다.
        Passenger passenger = passengerRepository.findPassengerByUserId(userId);
        //6. 이제 passengerId가 필요하다.
        Integer passengerId= passenger.getPassengerId();
        //7. 이제 passengerId, airlineTicketId 사용해서 reservation 만들자
        //8. price, charges, tax, total_price, success 정보 불러오기
        //join 테이블로 불러올 것이다.
        //AirlineTicketAndFlightInfo entity만들어야 함
        //AirlineTicketAndFlightInfo에서 여러개 받아올 거니까 List로
        //airlineTicketRepository에 findAllAirlineTicketAndFlightInfo 메소드 만들어 줘야지
        List<AirlineTicketAndFlightInfo> airlineTicketAndFlightInfos
                = airlineTicketRepository.findAllAirlineTicketAndFlightInfo(airlineTicketId);
        //9. 드디어 reservation 만들기 위한 정보 다 모았음
        //Reservation은 entity
        Reservation reservation= new Reservation(passengerId, airlineTicketId);
        //reservation을 만든걸 ReservationRepository안에 넣어야지
        //그러기 위해 saveReservation 메소드가 필요한데,
        //saveReservation은 만들고, 넣고가 있으니까 transactional
        //reservation만든거 성공했는지 알기 위해 Boolean
        Boolean isSuccess= reservationRepository.saveReservation(reservation);

        //10. DAO를 만들어주자
        //passengerDao, reservation Dao

        //11. Reservation Result DTO에다가 Reservation넣기
        List<Integer> prices= airlineTicketAndFlightInfos.stream().map(AirlineTicketAndFlightInfo::getPrice).collect(Collectors.toList());
        List<Integer> charges= airlineTicketAndFlightInfos.stream().map(AirlineTicketAndFlightInfo::getCharge).collect(Collectors.toList());
        Integer tax=airlineTicketAndFlightInfos.stream().map(AirlineTicketAndFlightInfo::getTax).findFirst().get();
        Integer totalPrice= airlineTicketAndFlightInfos.stream().map(AirlineTicketAndFlightInfo::getTotalPrice).findFirst().get();

        return new ReservationResult(prices, charges, tax, totalPrice, isSuccess);
    }
}

```

#### 4.service는 받아서 메소드를 정의하고, 필요한 repository고민

🙋🏻‍♀️ passenger repository <br>
🎟️ reservation repository <br>
✈️ flight, airline_ticket 두 개의 테이블을 join해서 한 개의 repository로 가지고 와야지 <br>

#### 5.필요한 repository구현 repository는 interface

##### 🙋🏻‍♀️ passenger repository

```java
public interface PassengerRepository {

    Passenger findPassengerByUserId(Integer userId);
}
```

##### 🎟️ reservation repository

```java
public interface ReservationRepository {

    Boolean saveReservation(Reservation reservation);
}
```

##### ✈️ airlineTicket repository에 flight, airline_ticket 두 개의 테이블을 join해서 한 개의 repository로 가지고 와야지

```java
public interface AirlineTicketRepository {
    List<AirlineTicketAndFlightInfo> findAllAirlineTicketAndFlightInfo(Integer airlineTicketId);
}
```

#### 6.repository구현 후에는 service에 필드로 가져와야 함, 그리고 생성자 구현해줘야 한다.

그래서 service에 constructor 수정해 주었음

```java
    //⭐️️repository 두 개 추가 되었으니까 생성자도 새로 만듦, update
    public AirReservationService(UserRepository userRepository, AirlineTicketRepository airlineTicketRepository, ReservationRepository reservationRepository, PassengerRepository passengerRepository) {
        this.userRepository = userRepository;
        this.airlineTicketRepository = airlineTicketRepository;
        this.reservationRepository = reservationRepository;
        this.passengerRepository = passengerRepository;
    }
```

#### 7.service에서 db와 매핑 위한 entitiy 구현

entitiy는 필드 다 있는 constructor, getter, setter, equals, hash
entitiy는 SQL과 1 대 1 매핑되어야 한다.

- Passenger Entity
- AirlineTicketAndFlightInfo Entity
- Reservation Entity

```java
    public Reservation(Integer passengerId, Integer airlineTicketId) {
        this.passengerId = passengerId;
        this.airlineTicketId = airlineTicketId;
        this.reservationStatus = "대기"; //기본값 대기로 넣었음 참고
        this.reserveAt = LocalDateTime.now(); //LocalDateTime 그 시점에 만들기로
    }
```

#### 8.repository를 실제로 실행하기 위한 Jdbc Template

이 파일의 이름은 `Dao`일 것이고
**@Repository**하며
repository interface를 implement 한다.
db에서 정보 얻어오기 위해 **RowMapper(rs, rowNums)**
또 repository에 정의된 메소드를 **Override**

##### 🙋🏻‍♀️ PassengerJdbcTemplateDao

```java
@Repository
public class PassengerJdbcTemplateDao implements PassengerRepository{
    private JdbcTemplate template;

    public PassengerJdbcTemplateDao(@Qualifier("jdbcTemplate2") JdbcTemplate template) {
        this.template = template;
    }

    static RowMapper<Passenger> passengerRowMapper = (((rs, rowNum) ->
            new Passenger(
                    rs.getInt("passenger_id"),
                    rs.getInt("user_id"),
                    rs.getNString("passport_num"))
    ));

    @Override
    public Passenger findPassengerByUserId(Integer userId) {
        return template.queryForObject("SELECT * FROM passenger WHERE user_id = ?", passengerRowMapper, userId);
    }
}

```

##### 🎟️ Reservation Jdbc Template

```java
//⭐️Reservation Dao
@Repository
public class ReservationJdbcTemplateDao implements ReservationRepository{
    private JdbcTemplate jdbcTemplate;

    public ReservationJdbcTemplateDao(@Qualifier("jdbcTemplate2") JdbcTemplate jdbcTemplate) {
        this.jdbcTemplate = jdbcTemplate;
    }


    @Override
    public Boolean saveReservation(Reservation reservation) {
        Integer rowNums= jdbcTemplate.update("INSERT INTO reservation(passenger_id, airline_ticket_id, reservation_status, reserve_at) VALUES (? ,? , ?, ? )",
                reservation.getPassengerId(), reservation.getAirlineTicketId(), reservation.getReservationStatus(),
                new Date(Timestamp.valueOf(reservation.getReserveAt()).getTime()));
        //sqlDate로 바꿔서 넣는다.
        return rowNums>0;
        //0보다 크면 reservation이 하나 이상 만들어졌다는 의미이니 성공했다는 것이다.
    }
}

```

##### ✈️ AirlineTicketJdbcDao

```java
@Repository
public class AirlineTicketJdbcDao implements AirlineTicketRepository{

    private JdbcTemplate jdbcTemplate;

    public AirlineTicketJdbcDao(@Qualifier("jdbcTemplate2") JdbcTemplate jdbcTemplate) {
        this.jdbcTemplate = jdbcTemplate;
    }

    //⭐️두 테이블을 join하기 위해서는 AirlineTicketAndFlightInfo를 위한 RowMapper
    static RowMapper<AirlineTicketAndFlightInfo> airlineTicketAndFlightInfoRowMapper = ((rs, rowNums)->
            new AirlineTicketAndFlightInfo(
                    rs.getInt("A.ticket_id"), //join을 통해서 A table로부터 ticket_id얻을 것이다.
                    rs.getDouble("F.flight_price"), //join을 통해서 F table로부터 flight_price얻을 것이다.
                    rs.getDouble("F.charge"), //double로 얻고 싶으니까 AirlineTicketAndFlightInfo 생성자 바꿔주기
                    rs.getDouble("A.tax"),
                    rs.getDouble("A.total_price"))

            );

    //⭐️
    @Override
    public List<AirlineTicketAndFlightInfo> findAllAirlineTicketAndFlightInfo(Integer airlineTicketId) {
        //두 테이블 join
        return jdbcTemplate.query("SELECT A.ticket_id, F.flight_price, F.charge, A.tax, A.total_price"+
                "   FROM airline_ticket A"+
                "   INNER JOIN flight F"+
                "   ON A.ticket_id = F.ticket_id" +
                "   WHERE A.ticket_id = ?", airlineTicketAndFlightInfoRowMapper, airlineTicketId);
    }
}

```

#### 9.결과를 나타내는 DTO 마지막으로 만들기

```java
@JsonNaming(PropertyNamingStrategies.SnakeCaseStrategy.class)
//snake로 와도 잘 받을 수 있다.
public class ReservationResult {
    //⭐️DTO
    private List<Integer> prices;

    private List<Integer> charges;
    private Integer tax;
    private Integer totalPrice;
    private Boolean success;

    public ReservationResult() {
    }

    public ReservationResult(List<Integer> prices, List<Integer> charges, Integer tax, Integer totalPrice, Boolean success) {
        this.prices = prices;
        this.charges = charges;
        this.tax = tax;
        this.totalPrice = totalPrice;
        this.success = success;
    }

    public List<Integer> getPrices() {
        return prices;
    }

    public List<Integer> getCharges() {
        return charges;
    }

    public Integer getTax() {
        return tax;
    }

    public Integer getTotalPrice() {
        return totalPrice;
    }

    public Boolean getSuccess() {
        return success;
    }
}

```
