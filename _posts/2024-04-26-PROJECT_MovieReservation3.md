---
title: All about List
categories: [Project, Movie Reservation Project]
tags: [list]
---

## ✅ GOAL: from list entity get list entity

> 영화가 여러개 있는 영화 리스트가 있는 상황에서, 하나의 영화에 대해 여러개의 스케쥴을 받고, 그 스케쥴들에서 ticket sales구해야 함

### 🟢 TRYOUT 1: for(Movie movie: movieList)

#### service

```java
        for(Movie movie: movieList){
            //ticket sales
            List<Schedule> scheduleList= movie.getScheduleList();
            double ticketSales= caculateTicketSales(scheduleList);
            //score
            List<Review> reviewList= reviewJpa.findByMovieId(movie.getMovieId());
            double score= caculateScore(reviewList);
            //dDay
            Date releaseDate= movie.getReleaseDate();
            LocalDate localReleaseDate= releaseDate.toInstant().atZone(ZoneId.systemDefault()).toLocalDate();
            if(localReleaseDate.isBefore(LocalDate.now())) movie.setDDay(0);
            //save to movie
            movie.setTicketSales(ticketSales);
            movie.setScoreAvg(score);
        }
```

### 🟢 TRYOUT 2: forEach

```java
            List<ProductOption> productOptions= productOptionJpa.findByProduct(product);
            productOptions.forEach((po)->po.setStock(0));
            productOptionJpa.saveAll(productOptions);
```

## ✅ GOAL: get only x from xList

> get only actor names from actor List

### 🟢 `stream`, `map`해서 얻고자 하는 `x`를 리스트에서 하나하나 얻어오고, `toList()`

```java
        List<Actor> actorList = actorJpa.findByMovieId(movie.getMovieId());
        List<String> actorNameList= actorList.stream().map(Actor::getActorName).collect(Collectors.toList());
        //get only remaing seats in each schedule in schedule list
        List<Integer> remainingSeatsList= scheduleList.stream().map(Schedule::getRemainingSeats).toList();
```

```java
        List<LocalTime> movieTimes = scheduleList.stream().map(schedule -> schedule.getStartTime().toLocalTime()).collect(Collectors.toList());
```

## ✅ GOAL: get only x from xList, BUT if repeated, add only once.

> if there are same cinema names in scheduleList, just add once to cinenaNameList

### 🟢 distinct()

```java
        List<Schedule> scheduleList= movie.getScheduleList();

        List<String> cinenaNameList= scheduleList.stream()
                .map(schedule -> schedule.getCinemaType().getCinema().getCinemaName())
                .distinct()
                .collect(Collectors.toList());

        //if there are same dates, dont put two same dates in movieDateList
        List<Schedule> scheduleList= movie.getScheduleList();

        List<LocalDate> movieDateList= scheduleList.stream()
                .filter(schedule -> schedule.getCinemaType().getCinema().getCinemaName().equals(cinemaName))
                .map(schedule -> schedule.getStartTime().toLocalDate())
                .distinct()
                .collect(Collectors.toList());
```

## ✅ GOAL: make DTO list from Entity List

> make responseDTO List from review List

### 🟢 `stream`, `map`해서 `DTO list` 안에 있는 dto 하나하나 만들기

```java
        //make DTO list from Entity List
        List<Review> reviewList= reviewJpa.findByMovieId(movie.getMovieId());
        List<ReviewResponseDto> reviewResponseDtoList= reviewList.stream()
                .map(review -> new ReviewResponseDto(
                        review.getUser().getName(),
                        review.getScore(),
                        review.getContent(),
                        review.getReviewDate()
                ))
                .toList();
```

```java
        List<Reservation> reservationList= reservationJpa.findByUser(user);

        //list를 받아 list를 return하는 경우
        List<ReservationResponseDto> reservationResponseDtoList= reservationList.stream()
                .map(reservation -> new ReservationResponseDto(
                        reservation.getReserveNum(),
                        reservation.getSchedule().getMovie().getTitleKorean(),
                        reservation.getSchedule().getCinemaType().getCinema().getCinemaName(),
                        reservation.getSchedule().getStartTime().toLocalDate(),
                        reservation.getSchedule().getStartTime().toLocalTime(),
                        reservation.getReserveTime()
                ) ).collect(Collectors.toList());

```

### 🟢 ArrayList.add()

```java
        //ScheduleList scheduleList= schedule 모아놓은 리스트

        List<ScheduleResponseDto> scheduleResponseDtoList = new ArrayList<>();
        for(Schedule s: scheduleList) {
            ScheduleResponseDto scheduleResponseDto = ScheduleResponseDto.builder()
                    .cinemaTypeName(s.getCinemaType().getTypeName())
                    .totalSeats(s.getCinemaType().getTotalSeats())
                    .movieTime(movieTimes)
                    .remainingSeats(s.getRemainingSeats())
                    .build();
            scheduleResponseDtoList.add(scheduleResponseDto);
        }
```

## ✅ GOAL: JPA에서 find한 결과가 List일지(여러개인지) Object일지(한개일지) 모르곘음

### 🟢 Optional

```java
List<Review> userReviews= reviewJpa.findByUser(user); //내가 쓴 리뷰들만 불러옴
Optional<Review> existingReview = userReviews.stream().filter(r-> r.getReviewId().equals(reviewId)).findFirst();
//내가 쓴 리뷰 중에서 아이디랑 일치하는게 한 개일 수도 있고, 여러개일 수도 있어
//따라서 Optional

```
