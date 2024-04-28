---
title: (feat) Date ↔️ LocalDate
categories: [Project, Movie Reservation Project]
tags: [date, localdate]
---

## ✅ Date to LocalDate

> change datatype Date to LocalDate

### 🟢 Date.toInstant().atZone(ZoneId.systemDefault()).toLocalDate()

ReleaseDate type: Date <br>
localReleaseDate type: LocalDate<br>

```java
Date releaseDate= movie.getReleaseDate();
LocalDate localReleaseDate= releaseDate.toInstant().atZone(ZoneId.systemDefault()).toLocalDate();
```

## ✅ LocalDate to Date

### 🟢 java.sql.Date

```java
        LocalDate reviewLocalDate= LocalDate.now();
        //two ways of changing local date => date
        Date reviewDate= Date.valueOf(reviewLocalDate); //Date is from java.sql.Date
```

### 🟢 java.util.Date

```java
        LocalDate reviewLocalDate= LocalDate.now();
        //two ways of changing local date => date
        Date reviewDate= java.sql.Date.valueOf(reviewLocalDate);  //Date is from java.util.Date
```
