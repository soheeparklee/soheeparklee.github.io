---
title: Date and Time
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ LocalDateTime

- 👍🏻 get time of my local area

- `LocalDate`: `2023-11-21`
- `LocalTime`: `00:20:30.234`
- `LocalDateTime`: `LocalDate` + `LocalTime`, `2023-11-21T00:20:30.234`

- `now()`

```java
LocalDate now = LocalDate.now(); //2025-05-01
LocalTime now = LocalTime.now(); //17:55:06.305827

LocalDateTime now = LocalDateTime.now(); //2025-05-01T17:57:05.637786
LocalDate date = now.toLocalDate(); //get only date from LocalDateTime
LocalTime time = now.toLocalTime(); //get only time from from LocalDateTime
LocalDateTime addDateTime = LocalDateTime.of(date, time); //날짜, 시간 합치기
```

- `isBefore()`
- `isAfter()`
- `isEquals()`

## ✅ ZonedDateTime

- UTC, summertime에 대한 정보 포함한 시간
- for developing international time
- 👍🏻 apply both UTC, summertime

```java
ZoneId.getAvailableZoneIds() // 내가 시간 얻을 수 있는 지역 얻기
ZoneId zoneId = ZoneId.systemDefault(); //내 시스템이 어디 지역 시간 쓰는지
```

- ✔️ **Get other country times**

```java
ZonedDateTime seoul = ZonedDateTime.of(LocalDate.of(2024, 1, 1), LocalTime.of(9, 0, 0), ZoneId.of("Asia/Seoul"));
ZonedDateTime london = seoul.withZoneSameInstant(ZoneId.of("Europe/London"));
ZonedDateTime newyork = seoul.withZoneSameInstant(ZoneId.of("America/New_York"));

```

## ✅ OffsetDateTime

- UTC에 대한 정보 포함한 시간
- 👍🏻 apply UTC, do not apply summertime

## ✅ Instant

- how much time passed since `1970-01-01 00:00:00`
- show how much seconds passed
- 👍🏻 used when the time has to same all over the world

```java
Instant now = Instant.now();
Instant epochSecond = Instant.ofEpochSecond(0);
```

## ✅ Period and Duration

- **amount** of time

- ✔️ **Period**
- amount of time in year, month, days

```java
Period period = Period.ofDays(10); //10days


LocalDate localDate = LocalDate.of(2020, 3, 3);
LocalDate plus = localDate.plus(period); //3 + 10 = 13일


//기간의 차이 구하기
LocalDate startDate = LocalDate.of(2020, 3, 3);
LocalDate endDate = LocalDate.of(2025, 5, 1);

Period between = Period.between(startDate, endDate);
between.getYears(); //5년
between.getMonths(); //1개월
between.getDays(); //28일
```

- ✔️ **Duration**
- amount of time in hour, minutes, seconds

## ✅ Datetime Interface

- `LocalDateTime`, `ZonedDateTime`, `OffsetDateTime` extends `interface Temporal` and `TemporalAccessor`
- ✔️ `interface TemporalAccessor`: read date, time
- ✔️ `interface Temporal`: modify date, time

- `Period` and `Duration` extends `interface TemporalAmount`
- ✔️ `interface TemporalAmount`: amount of time

- `ChronoUnit` extends `interface TemporalUnit`
- ✔️ `interface TemporalUnit`: 시간 단위 제공
- minutes, day, years, decades...

- `ChronoField` extends `interface TemporalField`
- ✔️ `interface TemporalField`: 날짜와 시간의 특정 부분을 나타냄
  - 예를 들어 8월 16일일 때, `MONTH_OF_YEAR: 8`, `DAY_OF_YEAR: 16`

```java
ChronoField.MONTH_OF_YEAR.range(); //1-12
ChronoField.DAY_OF_YEAR.range() //1-365/366
```

## ✅ Get and modify Date, time

- ✔️ **Get date, time**

```java
LocalDateTime dt = LocalDateTime.of(2020, 1, 2, 3, 40, 50);

dt.get(ChronoField.YEAR); //2020
dt.getYear(); //2020
```

- ✔️ **Add time**
- same result, in three ways

```java
LocalDateTime dt = LocalDateTime.of(2020, 1, 2, 3, 40, 50);

// 1️⃣ ChronoUnit
LocalDateTime years1 = dt.plus(10, ChronoUnit.YEARS); //2030
// 2️⃣ plusYears(simplified method of ChronoUnit)
LocalDateTime years2 = dt.plusYears(10); //2030

3️⃣ Period 사용
Period period = Period.ofYears(10);
LocalDateTime years3 = dt.plus(period); //2030
```

- ✔️ **Check if I can get this value from this class**

```java
LocalDate now = LocalDate.now();
now.isSupported(ChronoField.SECOND_OF_DAY); //can I get SECOND_OF_DAY from LocalDate
```

- ✔️ **Modify time**
- `with()`

```java
LocalDateTime dt = LocalDateTime.of(2020, 1, 2, 3, 40, 50);
LocalDateTime changedDt1 = dt.with(ChronoField.YEAR, 2030); //change year to 2030

LocalDateTime changedDt2 = dt.withYear(2030);

//temporal adjuster
//change to next week
LocalDateTime nextFriday = dt.with(TemporalAdjusters.next(DayOfWeek.FRIDAY));
//last sunday of this month
LocalDateTime sameMonthLastSunday = dt.with(TemporalAdjusters.lastInMonth(DayOfWeek.SUNDAY));

```

## ✅ Date ➡️ String

- ✔️ **Date ➡️ String**

```java
LocalDateTime dateTime = LocalDateTime.of(2020, 1, 2, 3, 40, 59);

DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy년 MM월 dd일 HH:mm:ss");
String formattedDateTime = dateTime.format(formatter); //2020년 01월 02일 03:40:59
```

- ✔️ **String ➡️ Date**

```java
String input = "2020년 09월 22일 12:34:32";
LocalDateTime parsedDateTime = LocalDateTime.parse(input, formatter); //2020-09-22T12:34:32
```

## ✅

## ✅
