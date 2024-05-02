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
