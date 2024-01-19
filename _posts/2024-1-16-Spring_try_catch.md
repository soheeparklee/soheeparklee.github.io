---
title: 예외처리, RestController Advice
categories: [JAVA, Spring]
tags: [advice, try, catch] # TAG names should always be lowercase
---

에러가 생길 부분을 미리 예측하여 catch, throw하고
만약 client에게까지 보여져야 하는 error이라면 controller에까지 반영한다.

## ✅ ExceptionControllerAdvice는 AOP를 기반으로 한다.

AOP는 서로 비슷한 코드를 여러번 반복해서 입력하는 것이 아니라 <br>
반복되는 코드끼리 **모듈화**해서 **advice**로 만들어 **침투적용**하는 것을 의미한다. <br>
따라서 에외 처리 하는 코드는 반복되니까 ExceptionControllerAdvice로 빼서 적용시킨다. <br>

## ✅ Advice 없이 예외처리해보기

ticketType 잘못 입력하면 error <br>

```java
//controller
    @GetMapping("/tickets")
    public ResponseEntity findAirlineTickets(@RequestParam("user-id") Integer userId,
                                             @RequestParam("airline-ticket-type") String ticketType ){

        try{
            List<Ticket> tickets = airReservationService.findUserFavoritePlaceTicket(userId, ticketType);
            TicketResponse ticketResponse= new TicketResponse(tickets);
            return new ResponseEntity( ticketResponse, HttpStatus.OK); //tryCatch 할 때는 ResponseEntity를 사용
        } catch(InvalidValueExceptions ive){
            log.error("Problem in Client Request_wrong: ticket type", ive.getMessage());
            return new ResponseEntity(ive.getMessage(), HttpStatus.BAD_REQUEST);
        }
    }

//exceptions
public class InvalidValueExceptions extends RuntimeException{

    public InvalidValueExceptions(String message) {
        super(message);
    }
}

//service
    public List<Ticket> findUserFavoritePlaceTicket(Integer userId, String ticketType) {
        //만약 ticketType이 왕복 또는 편도가 아니라면?
        Set<String> ticketTypeSet= new HashSet<>(Arrays.asList("편도", "왕복"));
        if (!ticketTypeSet.contains(ticketType))
            throw new InvalidValueExceptions(ticketType + "No such ticket Type");

        UserEntity userEntity = userRepository.findUserById(userId);
        String likePlace= userEntity.getLikeTravelPlace();

        List<AirlineTicket> airlineTickets= airlineTicketRepository.findAllAirlineTicketsWithPlaceAndTicketType(likePlace, ticketType);

        List<Ticket> tickets= airlineTickets.stream().map(Ticket::new).collect(Collectors.toList());
        return tickets;
    }
```

<img width="490" alt="스크린샷 2024-01-16 오후 1 35 35" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/ba4446e0-7be8-408d-a358-3ae544dce93c">

<img width="1101" alt="스크린샷 2024-01-16 오후 1 36 08" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/add28d55-65cc-4cd7-8f58-f3727cfc533b">

## ✅ @ RestController Advice

web layer

```java
//service
    public List<Ticket> findUserFavoritePlaceTicket(Integer userId, String ticketType) {
        //만약 ticketType이 왕복 또는 편도가 아니라면?
        Set<String> ticketTypeSet= new HashSet<>(Arrays.asList("편도", "왕복"));
        if (!ticketTypeSet.contains(ticketType))
            throw new InvalidValueExceptions(ticketType + "No such ticket Type"); //⭐️throw하면 advice로 간다.

        UserEntity userEntity = userRepository.findUserById(userId).orElseThrow(
                () -> new NotFoundException("No Such User with ID" + userId));
        String likePlace= userEntity.getLikeTravelPlace();

        List<AirlineTicket> airlineTickets= airlineTicketRepository.findAllAirlineTicketsWithPlaceAndTicketType(likePlace, ticketType);

        if(airlineTickets.isEmpty()) throw new NotFoundException("No matching likeplace and ticketType Found");

        List<Ticket> tickets= airlineTickets.stream().map(Ticket::new).collect(Collectors.toList());
        return tickets;
    }

//기존 코드
//controller
    @GetMapping("/tickets")
    public ResponseEntity findAirlineTickets(@RequestParam("user-id") Integer userId,
                                             @RequestParam("airline-ticket-type") String ticketType ){

        try{
            List<Ticket> tickets = airReservationService.findUserFavoritePlaceTicket(userId, ticketType);
            TicketResponse ticketResponse= new TicketResponse(tickets);
            return new ResponseEntity( ticketResponse, HttpStatus.OK); //tryCatch 할 때는 ResponseEntity를 사용
        } catch(InvalidValueExceptions ive){
            log.error("Problem in Client Request_wrong: ticket type", ive.getMessage());
            return new ResponseEntity(ive.getMessage(), HttpStatus.BAD_REQUEST);
        } catch(NotFoundException nfe){
            log.error("Problem in DB: wrong User", nfe.getMessage());
            return new ResponseEntity( nfe.getMessage(), HttpStatus.NOT_FOUND);
        }
    }
```

### ⭐️ ExceptionControllerAdvice

```java
//
    @PostMapping("/reservation")
    @ResponseStatus(HttpStatus.CREATED)
    public ReservationResult makeReservation(@RequestBody ReservationRequest reservationRequest){

            ReservationResult reservationResult= airReservationService.makeReservation(reservationRequest);
            return reservationResult;

        //⭐️ NotAcceptException catch 삭제하고 ExceptionControllerAdvice에 위임
        //⭐️ NotFoundException catch 삭제하고 ExceptionControllerAdvice에 위임
    }
//ExceptionControllerAdvice
@Slf4j
@RestControllerAdvice
public class ExceptionControllerAdvice {
    @ResponseStatus(HttpStatus.NOT_FOUND)
    @ExceptionHandler(NotFoundException.class)
    public String handleNotFoundException(NotFoundException nfe){
        log.error("Problem in DB: wrong User"+  nfe.getMessage());
        return nfe.getMessage();
    }
    @ResponseStatus(HttpStatus.NOT_ACCEPTABLE)
    @ExceptionHandler(NotAccpetExcpetion.class)
    public String handleNotAcceptException(NotAccpetExcpetion nae){
        log.error("Problem in client", nae.getMessage());
        return nae.getMessage();
    }
}

```
