---
title: (feat) Get ticket sales
categories: [Project, Movie Reservation Project]
tags: [double]
---

## ✅ How to get ticket sales

> ticket sales= (total seats - remaining seats)/total seats \* 100
> remaining seats: schedule table에 있음
> total seats of a cinema: cinema type table에 있음
> 한 영화에 대한 모든 schedule, 즉 schedule List가 주어짐

## 🟢 caculate total seats

`schedule List`에 있는 각각의 `schedule`에 대해 `cinema type`을 찾아서 <br>
`cinema type table`에 있는 `total seats`구하고 모두 더한다. <br>

```java
private int caculateTotalSeats(List<Schedule> scheduleList){
    //get total seats per cinema
    int totalSeats= scheduleList.stream()
            .map(schedule -> schedule.getCinemaType().getTotalSeats())
            .mapToInt(Integer::intValue)
            .sum();
    return totalSeats;
}
```

## 🟢 caculate ticket sales

이제 remaining seats를 구해야 한다.
두 가지 방법이 있겠으나..
첫 번째 방법이 더 효율적이지만
두 번째 방법도 각각의 RemainingSeats에 대해 무언가를 해줄 수 있다는 점에서 알아두는데 의의가 있다.

### 👍🏻 방법 1. `mapToInt().sum()`

```java
int totalRemainingSeats= scheduleList.stream()
                    .map(Schedule::getRemainingSeats)
                    .mapToInt(Integer::intValue)
                    .sum();
```

### 👍🏻 방법 2. RemainingSeats를 구해 List로 만들고, List를 돌면서 더한다.

```java
List<Integer> remainingSeatsList= scheduleList.stream().map(Schedule::getRemainingSeats).toList();
        int totalRemainingSeats= 0;
        for(int x: remainingSeatsList)  totalRemainingSeats +=x;
        int totalSeats= caculateTotalSeats(scheduleList);
```

### ☑️ 이제 마지막으로, ticket sales를 계산한다.

```java
double ticketSales = ((double) (totalSeats - totalRemainingSeats)totalSeats * 100.0) ;
//show only until 소수점 첫째자리
double formattedTicketSales= Math.round(ticketSales*10.0)/10.0;
return formattedTicketSales;
```

## 🟢 Final Code

```java
private double caculateTicketSales(List<Schedule> scheduleList){
        //remaining seats(schedule) / total seats(cinema type) * 100
        //1. get List<schedule> to get remaining seats
        //2. for each schedule in list, get total seats from cinema type
        //3. do the math
        List<Integer> remainingSeatsList= scheduleList.stream().map(Schedule::getRemainingSeats).toList();
        int totalRemainingSeats= 0;
        for(int x: remainingSeatsList)  totalRemainingSeats +=x;
        int totalSeats= caculateTotalSeats(scheduleList);
        double ticketSales = ((double) (totalSeats - totalRemainingSeats) /totalSeats * 100.0) ;
        //show only until 소수점 첫째자리
        double formattedTicketSales= Math.round(ticketSales*10.0)/10.0;
        return formattedTicketSales;
}
private int caculateTotalSeats(List<Schedule> scheduleList){
        //get total seats per cinema
        int totalSeats= scheduleList.stream()
                .map(schedule -> schedule.getCinemaType().getTotalSeats())
                .mapToInt(Integer::intValue)
                .sum();
        return totalSeats;
}

```

## 🟢 JPA에서 구하는 방법

movie table에 ticket_sales라는 field가 있음 <br>
따라서 ticket_sales를 구해서 movie table에 넣어주는(update해주는) JPQL <br>

```java
@Repository
public interface MovieJpa extends JpaRepository<Movie, Integer> {
    @Transactional
    @Modifying
    @Query(
            value = "UPDATE movie AS A " +
                    "INNER JOIN schedule AS B ON A.movie_id = B.movie_id " +
                    "INNER JOIN cinema_type AS C ON B.cinema_type_id = C.cinema_type_id " +
                    "SET A.ticket_sales = (1 - (B.remaining_seats / C.total_seats)) * 100 "
    , nativeQuery = true)
    void updateTicketSales();
}
```
