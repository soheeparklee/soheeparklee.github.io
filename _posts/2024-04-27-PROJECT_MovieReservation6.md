---
title: (feat) show only with/until N digits
categories: [Project, Movie Reservation Project]
tags: [digit, decimal]
---

## ✅ GOAL: (double) 소수점 첫째짜리까지만 보이고 싶어

### 🟢 Math.round()

```java
        double ticketSales = ((double) (totalSeats - totalRemainingSeats) /totalSeats * 100.0) ;
        //show only until 소수점 첫째자리
        double formattedTicketSales= Math.round(ticketSales*10.0)/10.0;
        return formattedTicketSales;
```

## ✅ GOAL: (String) 항상 2자리 수로 보이고 싶어

> 한 자리 수이면 앞에 0을 추가할래

### 🟢 String.format()

```java
        LocalDate movieDate= reservationRequestDto.getReserveDate();

        String month = String.format("%02d", movieDate.getMonthValue());
        String day = String.format("%02d", movieDate.getDayOfMonth());
        String dateNum = month + day; //0427
```

## ✅ GOAL 마지막 4자리 수만 보이고 싶어

### 🟢 `.subString()`

```java
        String cinemaNum= cinema.getPhoneNumber().substring(cinema.getPhoneNumber().length()-4);
```
