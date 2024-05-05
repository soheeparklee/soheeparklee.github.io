---
title: (feat) Only able to add review for movies 1. with reservation 2. watched
categories: [Project, Movie Reservation Project]
tags: []
---

## ✅ 내가 1. 예약했고 2. 이미 본 영화에 대해서만 리뷰 등록 가능

> check if I have reservation for this movie
> check if the movie start time is passed compared to current time

🔴 하나의 영화에 대해 두 개 이상 예약이 있으면??

> can have more than two reservations for the movie
> 제대로 하려면, 예약 아이디를 받아서 그 예약의 영화 시간을 현재 시간과 비교해야 한다.

## 🟢

```java
        Optional<Reservation> reservationList= reservationJpa.findByUserAndMovie(user, movie);
        boolean hasReservation= reservationList.isEmpty();
        boolean timePassedMovie= reservationList.stream().allMatch(reservation -> reservation.getSchedule().getStartTime().isAfter(LocalDateTime.now()));

```

## 🟢 Final code

```java
    public ResponseDto addReview(CustomUserDetails customUserDetails, Integer movieId, ReviewDto reviewDto) {
        User user= userJpa.findByMyIdFetchJoin(customUserDetails.getMyId())
                .orElseThrow(()-> new NotFoundException("Cannot find user with myId: "+ customUserDetails.getMyId()));
        Movie movie= movieJpa.findById(movieId)
                .orElseThrow(()-> new NotFoundException("Cannot find movie with Id: "+ movieId));
        //only one review in one movie
        if(!reviewJpa.findByUserAndMovie(user, movie).isEmpty()) throw new BadRequestException("You have already posted review for this movie");
        //if score<0 or score>10 not valid
        int score= reviewDto.getScore();
        if(score<0 || score>10) throw new BadRequestException("Score can only be from 1 to 10");


        //내가 본 영화에 대해서만 리뷰 남길 수 있어야 한다.
        Optional<Reservation> reservationList= reservationJpa.findByUserAndMovie(user, movie);
        boolean hasReservation= reservationList.isEmpty();
        //모든 에약의 영화 시작 시간이 지금보다 지났음
        boolean timePassedMovie= reservationList.stream().allMatch(reservation -> reservation.getSchedule().getStartTime().isAfter(LocalDateTime.now()));


        LocalDate reviewLocalDate= LocalDate.now();
        Date reviewDate= Date.valueOf(reviewLocalDate);
        //both false
        //reservation is not empty
        //영화 시작 시간이 지금보다 지나지 않은 예약이 하나라도 있으면
        if(!hasReservation && !timePassedMovie) {
            Review review = Review.builder()
                    .user(user)
                    .movie(movie)
                    .score(score)
                    .content(reviewDto.getContent())
                    .reviewDate(reviewDate) //date만 구하는 방법
                    .build();
            reviewJpa.save(review);
            return new ResponseDto(HttpStatus.OK.value(), "Review add success");

        } else{
            throw new NotAuthorizedException("You can add review for only movies you have watched");
        }

    }
```
