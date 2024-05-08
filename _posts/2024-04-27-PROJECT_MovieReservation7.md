---
title: (feat) How to get average score
categories: [Project, Movie Reservation Project]
tags: [average, score, double]
---

## ✅ get average score

> score is in review table
> get all reviews of a movie, set it in reviewList
> for each reviewList, get score and add. `sum()`
> then, get size of reviewList
> average= sum of review scores / size of reviewList

## 🟢 get average score

```java
int scoreSum= reviewList.stream().mapToInt(Review::getScore).sum();
int numberOfReviews= reviewList.size();
```

## 🟢 Final Code

여러번 사용해서 다른 메소드에서 구현

```java
    private double caculateScore(List<Review> reviewList){
        //score(review) 다 더해서 / number of review
        int scoreSum= reviewList.stream().mapToInt(Review::getScore).sum();
        int numberOfReviews=reviewList.size();
        double scoreAvg= (double) scoreSum/numberOfReviews;
        double formattedScoreAvg= Math.round(scoreAvg+10.0)/10.0;
        return scoreAvg;
    }
```

## 🟢 Cleaner Code

같은 메소드 내에서 구현
💡 나누기 할 때는 항상 나누는 수가 0이 되지 않도록 조심해야 한다.

```java
        Page<Movie> moviePage= movieJpa.findAll(pageable);
        for(Movie movie: moviePage){
            //scoreAvg
            List<Review> reviewList= reviewJpa.findByMovieId(movie.getMovieId());
            int scoreSum= reviewList.stream().map(Review::getScore).mapToInt(Integer::intValue).sum();
            int countReview= reviewList.size();
            if(countReview == 0 )throw new NotFoundException("There are no reviews for this movie"); //나누는 수 0 ❌
            double scoreAvg= (double) scoreSum / countReview * 100;

            movie.setScoreAvg(scoreAvg);
            movieJpa.save(movie);
        }
```

## 🟢 JPA에서 구하는 방법

movie table안에 score_avg라는 field있음 <br>
따라서 JPA에서 구해서 movie table안에 score_avg를 update <br>

```java

@Repository
public interface MovieJpa extends JpaRepository<Movie, Integer> {

    @Transactional
    @Modifying
    @Query(
            value = "UPDATE movie AS A " +
                    "INNER JOIN (SELECT movie_id, (count(score) / sum(score)) AS SCORE_AVG " +
                    "            FROM review group by movie_id) AS B ON A.movie_id = B.movie_id " +
                    " SET A.score_avg = B.SCORE_AVG "
    , nativeQuery = true)
    void updateScoreAvg();

    Page<Movie> findAll(Pageable pageable);
}
```
