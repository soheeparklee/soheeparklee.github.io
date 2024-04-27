---
title: (fix) only user who registered the reservation/review can update/delete
categories: [Project, Movie Reservation WEB BE Project]
tags: [update, delete]
---

## ✅ GOAL

> only user who registered the reservation/review can update/delete
> 내가 만든 예약/리뷰만 수정 또는 삭제할 수 있다.

## 🟢 TRYOUT 1: find reservation/review with id and User

As request, we get the user custom details and the ID of reservation/review. <br>
Thus, in JPA I can find the reservation/review that both matches the user and the reservation/review ID.<br>
The code will look like this.<br>

#### service

```java
        Review review= reviewJpa.findByReviewIdAndUser(reviewId, user) //이로써 내가 쓴 리뷰만 불러오게 된다.
                .orElseThrow(()-> new NotFoundException("Cannot find review with Id and User: "+ reviewId));
```

#### JPA

```java
    @Query(
            "SELECT r " +
                    "FROM Review r " +
                    "JOIN r.user u " +
                    "WHERE r.reviewId = :reviewId AND u= :user"
    )

    Optional<Review> findByReviewIdAndUser(Integer reviewId, User user);
```

### 👎🏻

However, this will not let me to throw different exceptions.<br>
I have to throw a NFE, `"Cannot find review with Id and User: "+ reviewId` and this does not specify if the exception is because of the user of the review ID.<br>

## 🟢 TRYOUT 2: find user info, and check if it matches the user info on reservation/review

First, find the info of the user on user table.<br>
For example, user name.<br>
Second, find the user name on reservation/review.<br>
Third, using `if`, check if the two names match.<br>

#### service

```java
    public ResponseDTO updatePost(CustomUserDetails customUserDetails, Integer postId, PostRequest postRequest) {
        User user= userJpa.findByEmailFetchJoin(customUserDetails.getEmail())
                .orElseThrow(()-> new NotFoundException("이메일" + customUserDetails.getEmail() + "을 가진 유저를 찾지 못했습니다."));
        Post post= postJpa.findById(postId)
                .orElseThrow(()-> new NotFoundException("아이디 "+ postId +"에 해당하는 게시글이 없습니다."));

        String nameUser= user.getName();
        String namePost= post.getName();
        if(nameUser.equals(namePost)){
            post.setTitle(postRequest.getTitle());
            post.setContent(postRequest.getContent());
            Post updatePost = postJpa.save(post);

            PostDetailResponse postDetailResponse = new PostDetailResponse(
                    updatePost.getPostId(),
                    updatePost.getTitle(),
                    updatePost.getName(),
                    updatePost.getContent());

            return new ResponseDTO(HttpStatus.OK.value(), "Post updated successfully", postDetailResponse);
        } else{
            throw new NotSameUserException("Post update fail. 작성자가 아닙니다.");
        }
    }
```

### 👍🏻

Can throw exceptions for each case.<br>

### 👎🏻

However, what if there is no `user name` on both tables?<br>
Should I use userID?<br>

## 👍🏻 TRYOUT 3: no need to get User Name! Just compare user.

#### service

```java
    public ResponseDTO soldout(CustomUserDetails customUserDetails, Integer productId) {
        User user = userJpa.findByEmail(customUserDetails.getEmail())
                .orElseThrow(() -> new NotFoundException("Cannot find user with email: " + customUserDetails.getEmail()));

        Product product= productJpa.findById(productId)
                .orElseThrow(()-> new NotFoundException("Cannot find product with Id: "+ productId));

        if(user.equals(product.getUser())){ //compare user
              //make changes ~~~
            return new ResponseDTO(HttpStatus.OK.value(), "Product status update to soldOut success");
        }else{
            throw new NotAcceptException("You do not have the authorization. You did not register this product.");
        }

    }
```

## 🟢 TRYOUT 4: find reservation/review with JPA that matches user. Then stream to find reservation/review that matches ID.

In this case, we do not know if `existingReview` will be a List or just one review. <br>
Thus, we use `<Optional>`<br>
and afer `<Optional>`, use `get`<br>

```java
    public ResponseDto updateMyReview(CustomUserDetails customUserDetails, Integer reviewId, ReviewDto reviewDto) {
        User user= userJpa.findByMyIdFetchJoin(customUserDetails.getMyId())
                .orElseThrow(()-> new NotFoundException("Cannot find user with myId: "+ customUserDetails.getMyId()));
        List<Review> userReviews= reviewJpa.findByUser(user); //이로써 내가 쓴 리뷰만 불러오게 된다.
        if(userReviews.isEmpty()) throw new NotFoundException("User has no reviews");

        Optional<Review> existingReview = userReviews.stream().filter(r-> r.getReviewId().equals(reviewId)).findFirst(); //?
        Review review= existingReview.get();

        review.setScore(reviewDto.getScore());
        review.setContent(reviewDto.getContent());
        reviewJpa.save(review);
```
