---
title: Reflection_Movie Reservation project
categories: [Project, Movie Reservation Project]
tags: [project]
---

## ✅ Github

<https://github.com/sc-project2-MovieReservation/MovieReservation-BE>

## ✅ Notion

<https://project-movie-reservation.notion.site/Project-2_Movie-Reservation-Site-7ddd0eab1d0546cf85e7884982a05152?pvs=4>

## ✅ Reflection

### 0. Development Environment

> JAVA 17
> SpringBoot 3.2
> MariaDB
> AWS EC2, RDS

### 1. Project Duration and Team members

> Project Duration : 14th April ~ 7th May 2024
> Team members : 3 front-end programmers and 6 back-end programmers

### 2. Achievements and Improvements

#### 1) What are the achievements of this project?

We have achieved in developing an effective movie-reservation site. <br>

**(1) SignIn, Login, Logout**
Using JWT, the user can sign in, login and logout of the service. When the user logs out, the user’s JWT is blacklisted.
<br>

**(2) Main Page**
In main page, the user can view movies that are shown on cinema with pageable. The user can retrieve information about the movie poster, movie title, ticket sales, release date, scores given by user and the d-day of the movie. The ticket sales are calculated with the number of reservations made on the movie out of total seats. Scores are made from the average score of users who made reviews of this movie with a score ranging from 1 to 10. The d-day is retrieved by the date of today until the release date. If the movie is already released, the d-day will be set to 0.
<br>

**(3) Reservation Page**
In reservation Page, the user can find available reservations with the movie title, cinema name, date and time that the user wishes to make the reservation. The user can make reservations with requested movie title, cinema name, cinema type, date and time. Reservation updates can be made for movie times only. If the movie time or reservation time is in the past, the user will encounter an exception. Deleting a reservation that was made by the user is also possible. <br>
<br>

**(4) My Page**
In my page, the user can find information about the reservations that the user made and the information about the user himself. The user can also update his phone number or password. <br>
There is an additional service for registering reviews. The user can make reviews with a score ranging from 1 to 10 and a short one-sentence comment. After, the user can find all the reviews that the user registered, along with updating and deleting his reviews. <br>
<br>

**(5)ERD**
The ERD is efficiently organised to retrieve the data fast and effectively to provide for the facilitation of the service. The user table holds information about the user and is connected to the user_role table with the role table. Then the user table is also connected to the review table and reservation table, with a one to many relationship. <br>
The movie table is more complex. First, it is connected to the actor table with a connection to movie_actor table, as one movie can have several actors and an actor can have several movies as well. Then, the movie table is connected to the schedule table, which is also connected to the reservation table. Thus, the reservation table connects between the user table and the schedule table. <br>
Now, the schedule table connects the movie table and the cinema_type table. In the cinema type table, cinema type data such as first floor 2D, 3D are registered. Then, the cinema type table is connected to the cinema table, where data such as cinema name, address and phone_number is registered.
This formation of entity makes retrieving and saving data possible in every way. The user can make reservations with movie title, cinema name, date and time and the information will be saved on the tables accordingly. Also, it makes sure data is not duplicated thus effectively saving up memory space and each table has only information about itself. <br>

#### 2) What are the new skills and features acquired during and after the project?

**(1)Jasypt**
For this project, I implemented the use of `Jasypt` to my project. With the use of `Jasypt`, I could cncrypt my email, email password, database username, password, url and jwt-secret-key using SHA256. Thus, I could provide more security for my project. While studying the concept of `Jasypt`, I learned more about encryption and \***\* <br>
**(2)Redis**
The use of `Redis` was also impemented in this project. `Redis` was implemented for email-verification when the user makes a sign-in attempt. The random verification code was saved in `Redis` for a limited amount of time that the user can verify the code. With the implementation of `Redis`, I could save the verification code more effectively than saving verification code on the database. <br>
**(3)JQPL**
Also, I had many chances to practice the use of JPQL. In the service, there were situations where I had to fetch a certain data from several tables, combine them efficiently and make caculations for a field. Specifically I learned how to get the average of reviews and ticket sales using JPQL. Thanks to the use of JPQL, the code in the service was reduced efficiently, making my code more readable. <br>
**(4) EC2, RDS\*\*
The use of EC2 and RDS from AWS was also my first tryout. I had attempted deploying my previous projects two times, but had both failed. So during this project, I really put effort in succeeding my deployment of the project. I spent two full days on learning about EC2 and RDS, and successfully deployed my project on the EC2 server using ubuntu. I also made a RDS database so that the members of the project can share one database together. After linking the front-end and back-end, I also solved the `CORS` error, and deployed again to fix the code. Now I feel comfortable and confident with deployment.

#### 3) What could be improved for this project?

**(1) Logout API, save the blacklisted token on Redis**
Currently in this project, when the user logs out, the user's token is blacklisted, and not saved on any sort of storage. However, this leads to the problem that if for some reason the project is ran again or the server is turned off then back on, all the blacklisted tokens would be lost. As the project already implements `Redis`, the blacklisted tokens can be saved on `Redis` for a limited amount of time. For example, the token can have a key that is `true` if the token is blacklisted, and have a TTL of 7 days. If a user tries to login with a token with which the key is `true`, the user will not be permitted. The `Redis` storage will save the data for 7 days, and after delete the tokens that expired. Thus, using the storage efficiently.

**(2) Social Login**
Instead of an individual person(me in this project) holding the user's token, it would be safer that we use a cerfitied company's authentification service. Implementation of social login with servies such as google services, kakao services and naver login service would be recommendable.

**(3) Payment method**
This service does not have a paying system, as a movie reservation website would have. Thus, in the next coming days the implementation of a paying method should be added.

**(4) Make seat reservation of rows and columns**
This service lets the user reserve the movie, time, schedule and type of cinema, but does not have a system to fetch the seats. However, in real life cinemas, the user would choose a seat, that goes with names such as row A to H and columns from 1 to 8, for example. The ERD and entity for seats should be made.

### 3. Goals and schedule management

#### 1) 프로젝트 목표를 설정하고 이를 달성하기 위해 어떻게 일정을 계획했나요?

### 4. 협업 능력

#### 1) 팀원과의 협업은 어떠한가요? 효과적인 커뮤니케이션과 협업이 이루어졌나요? 그 이유는?

#### 2) 문제 발생 시 해결 과정에서 팀원과의 관계가 어떠한가요?

### 5. 자기주도성 및 학습 능력

#### 1) 새로운 기술이나 도구를 학습하는 과정에서 어떤 어려움이 있었나요?

#### 2) 프로젝트 중에 스스로 문제를 해결하는 자기주도성은 어땠나요?

#### 3) 피드백 or 도움을 받은 경로가 어떻게 되고 적용을 어떻게 하셨나요?

#### 4) 피드백을 받아 개선하거나 새로운 것을 학습하는 능력에 대해 어떻게 평가하시겠어요?

### 6. 완성도 및 기능 구현

#### 1) 프로젝트가 목표한 기능을 얼마나 만족스럽게 구현했나요?

### 7. 문서화

#### 1) 프로젝트 관련 문서화는 어떻게 이루어졌나요?
