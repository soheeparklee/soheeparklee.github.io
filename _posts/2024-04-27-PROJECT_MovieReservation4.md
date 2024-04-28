---
title: (feat) LocalDate, LocalTime ↔️ LocalDateTime
categories: [Project, Movie Reservation Project]
tags: [date, localdate, localdatetime]
---

## ✅ LocalDate, LocalTime 합쳐서 LocalDateTime 만들기

### 🟢 localDateTime 🟰 LocalDate.atTime(LocalTime)

```java
LocalDate movieDate= reservationRequestDto.getReserveDate();
LocalTime movieTime= reservationRequestDto.getReserveTime();

LocalDateTime movieDateTime= movieDate.atTime(movieTime);
```

## ✅ LocalDateTime에서 LocalDate, LocalTime 각각 빼오기

### 🟢 LocalDateTime.toLocal

```java
//newSchedule
LocalDateTime startTime;

LocalDate movieDate = newSchedule.getStartTime().toLocalDate()
LocalTime movieTime = newSchedule.getStartTime().toLocalTime()
```
