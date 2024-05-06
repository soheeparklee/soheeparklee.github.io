---
title: (feat) Sort by ticketSales/review
categories: [Project, Movie Reservation Project]
tags: [double]
---

## ✅ How to sort movie list by ticket sales/ review score

> ticket sales, scoreAvg는 모두 movie table에 있음
> 두 가지 정렬 기준을 이용하여 movielist를 정렬한다.
> `sorted()` > `Comparator.comparingDouble()` > `.reversed()` 해서 ticket sales/ review score이 높은 순서대로 보인다.
> 즉, 예매율 높은 순, 평점 높은 순

## 🟢 `sorted()`

```java
//sort
        List<MainPageResponseDto> mainPageResponseDtoList = new ArrayList<>();
        if(sort.equals("ticket-sales")){
            mainPageResponseDtoList= moviePage.stream()
                    .sorted(Comparator.comparingDouble(Movie::getTicketSales).reversed())
                    .map(movie -> new MainPageResponseDto(
                            movie.getPoster(),
                            movie.getTitleKorean(),
                            movie.getTicketSales(),
                            movie.getReleaseDate(),
                            movie.getScoreAvg(),
                            movie.getDDay()
                    ))
                    .toList();
        }else if(sort.equals("reviews")){
            mainPageResponseDtoList= moviePage.stream()
                    .sorted(Comparator.comparingDouble(Movie::getScoreAvg).reversed())
                    .map(movie -> new MainPageResponseDto(
                            movie.getPoster(),
                            movie.getTitleKorean(),
                            movie.getTicketSales(),
                            movie.getReleaseDate(),
                            movie.getScoreAvg(),
                            movie.getDDay()
                    ))
                    .toList();
        }else{
            throw new BadRequestException("Invalid sort criteria: " + sort);
        }
```

## 🟢 code with method

```java
public ResponseDto findMainPageSort(Pageable pageable, String sort) {

    // DTO List만드는 메소드
    List<MainPageResponseDto> mainPageResponseDtoList = moviePage.getContent().stream()
            .sorted(getComparator(sort))
            .map(movie -> new MainPageResponseDto(
                    movie.getPoster(),
                    movie.getTitleKorean(),
                    movie.getTicketSales(),
                    movie.getReleaseDate(),
                    movie.getScoreAvg(),
                    movie.getDDay()
            ))
            .toList();

    return new ResponseDto(HttpStatus.OK.value(), "Main page sort find success", mainPageResponseDtoList);
}
//sort 기준 만드는 method
private Comparator<Movie> getComparator(String sort) {
    if ("ticket-sales".equals(sort)) {
        return Comparator.comparingDouble(Movie::getTicketSales).reversed();
    } else if ("reviews".equals(sort)) {
        return Comparator.comparingDouble(Movie::getScoreAvg).reversed();
    } else {
        throw new BadRequestException("Invalid sort criteria: " + sort);
    }
}
```

## 🟢 Final code

```java
//controller
    @GetMapping("/findBySort/{sort}")
    public ResponseDto findMainPageSort(Pageable pageable,
                                        @PathVariable String sort){
        return mainPageService.findMainPageSort(pageable, sort);
    }

//service
public ResponseDto findMainPageSort(Pageable pageable, String sort) {
        ArrayList<String> sortArray= new ArrayList();
        sortArray.add("ticket-sales");
        sortArray.add( "reviews");

        Page<Movie> moviePage= movieJpa.findAll(pageable);
        for(Movie movie: moviePage){
            //ticketSales
            List<Schedule> scheduleList= movie.getScheduleList();
            int remainingSeats= scheduleList.stream().mapToInt(Schedule::getRemainingSeats).sum();
            int totalSeats= scheduleList.stream().map(Schedule::getCinemaType).map(CinemaType::getTotalSeats).mapToInt(Integer::intValue).sum();
            if (totalSeats == 0) throw new NotFoundException("There are no total seats for this movie");
            double ticketSales= ((double) (totalSeats- remainingSeats)/totalSeats)*100;
            double formattedTicketSales= (double) Math.round(ticketSales*10.0)/10.0;


            //scoreAvg
            List<Review> reviewList= reviewJpa.findByMovieId(movie.getMovieId());
            int scoreSum= reviewList.stream().map(Review::getScore).mapToInt(Integer::intValue).sum();
            int countReview= reviewList.size();
            if(countReview == 0 )throw new NotFoundException("There are no reviews for this movie");
            double scoreAvg= (double) scoreSum / countReview;

            movie.setTicketSales(formattedTicketSales);
            movie.setScoreAvg(scoreAvg);
            movieJpa.save(movie);
        }
        //sort
        List<MainPageResponseDto> mainPageResponseDtoList = new ArrayList<>();
        if(sort.equals("ticket-sales")){
            mainPageResponseDtoList= moviePage.stream()
                    .sorted(Comparator.comparingDouble(Movie::getTicketSales).reversed())
                    .map(movie -> new MainPageResponseDto(
                            movie.getPoster(),
                            movie.getTitleKorean(),
                            movie.getTicketSales(),
                            movie.getReleaseDate(),
                            movie.getScoreAvg(),
                            movie.getDDay()
                    ))
                    .toList();
        }else if(sort.equals("reviews")){
            mainPageResponseDtoList= moviePage.stream()
                    .sorted(Comparator.comparingDouble(Movie::getScoreAvg).reversed())
                    .map(movie -> new MainPageResponseDto(
                            movie.getPoster(),
                            movie.getTitleKorean(),
                            movie.getTicketSales(),
                            movie.getReleaseDate(),
                            movie.getScoreAvg(),
                            movie.getDDay()
                    ))
                    .toList();
        }else{
            throw new BadRequestException("Invalid sort criteria: " + sort);
        }
        return new ResponseDto(HttpStatus.OK.value(), "Main page sort find success",mainPageResponseDtoList);

    }
```
