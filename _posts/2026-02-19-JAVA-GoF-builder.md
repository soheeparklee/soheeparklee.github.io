---
title: Creational_Builder Pattern
categories: [JAVA, GoF]
tags: [] # TAG names should always be lowercase
---

## 🤷🏻‍♀️ What would happen if we did not have builder?

- Imagine we have a `trip` class
- attributes such as `place`, `how many nights`, `how many days`, `hotel`, `start date`...
- when we create a trip,
- we have some requirements

- ⚠️ `how many days` should be `how many nights` + 1
- ⚠️ for a one-day trip, we do not want to include `how many nights`, `how many days`, `hotel`
- 💊 maybe we can use several constructors?

- 👍🏻 When creation of an instance is complicated
- condition among attributes,
- several constructors needed
- we can use a `builder pattern` to facilitate the creation of an instance

## ✅ Diagram

[![Screenshot-2026-02-28-at-18-51-48.png](https://i.postimg.cc/QxjFZWjP/Screenshot-2026-02-28-at-18-51-48.png)](https://postimg.cc/qgZJ8qhX)

## 👎🏻 Before builder

- tour plan has many attributes

```java
public class TourPlan {
    private String title;
    private int nights;
    private int days;
    private LocalDate startDate;
    private String whereToStay;
    private List<DetailPlan> plans;
}
```

- In main class

```java
//for several day trip, need to set several attributes
TourPlan longTripPlan = new TourPlan("Spain", 3, 4, "hotel"...);
longTripPlan.setTitle("Spain");
longTripPlan.setNights(3);
longTripPlan.setDays(4); //day should always be night + 1
// 👎🏻 how can I set conditions among attributes
// when creating instance?

//for one day trip, I only want to set name
// 👎🏻 need several constructors with different parameters
TourPlan onedayPlan = new TourPlan("beach");
```

## 👍🏻 After implementing builder pattern

#### ✔️ Builder class

- methods return the `builder class` itself,
- so later method chaining is possible
- look at `App`

```java
public interface TourPlanBuilder {
    //methods return itself, 내가 내 자신을 return함으로써 내 자신의 메소드 또 부르기 가능
    TourPlanBuilder title(String title);
    TourPlanBuilder nightsAndDays(int nights, int days);
    TourPlanBuilder startDate(LocalDate localDate);
    TourPlanBuilder whereToStay(String whereToStay);
    TourPlanBuilder addPlan(int day, String plan);

    //last, return Plan
    TourPlan getPlan(); //and finally return the plan

}
```

#### ✔️ Concrete Builder class

```java
public class DefaultTourBuilder implements TourPlanBuilder{
    private String title;
    private int nights;
    private int days;
    private LocalDate startDate;
    private String whereToStay;
    private List<DetailPlan> plans;

    @Override
    public TourPlanBuilder title(String title) {
        this.title = title;
        return this;
    }
    
    //override all methods

    @Override
    public TourPlan getPlan() {
        return new TourPlan(title, nights, days, startDate, whereToStay, plans); //return Plan
    }
}
```

#### ✔️ Main class

```java
public class App {
    public static void main(String[] args) {
        TourPlanBuilder builder = new DefaultTourBuilder();

        // 👍🏻 without creating many constructors, can call methods I want from builder class
        TourPlan shortPlan = builder.title("beach")
                .startDate(LocalDate.of(2020, 10, 10))
                .getPlan();

        TourPlan longPlan = builder.title("Spain")
                .nightsAndDays(4, 5)
                .whereToStay("hotel")
                .startDate(LocalDate.of(2020, 10, 10))
                .addPlan(0, "madrid")
                .addPlan(1, "barcelona")
                .addPlan(2, "sevilla")
                .addPlan(3, "toledo")
                .getPlan();
    }
```

#### ✔️ Director class
- if instance is created in the same way several times, 
- create director class
- can hide how to make the instance

```java
public class Director {
    private TourPlanBuilder tourPlanBuilder;

    public Director(TourPlanBuilder tourPlanBuilder) {
        this.tourPlanBuilder = tourPlanBuilder;
    }

    //when I want to set everything for the plan
    public TourPlan SpainPlan(){
        return tourPlanBuilder.title("Spain")
                .nightsAndDays(4, 5)
                .whereToStay("hotel")
                .startDate(LocalDate.of(2020, 10, 10))
                .addPlan(0, "madrid")
                .addPlan(1, "barcelona")
                .addPlan(2, "sevilla")
                .addPlan(3, "toledo")
                .getPlan();
    }

    //when I want to only set title and startDate for plan
    public TourPlan shortPlan(){
        return tourPlanBuilder.title("beach")
                .startDate(LocalDate.of(2020, 10, 10))
                .getPlan();
    }
}
```

#### ✔️ Main class

```java
public class App {
    public static void main(String[] args) {
        Director director = new Director(builder);
        TourPlan shortPlan1 = director.shortPlan();
        TourPlan longPlan2 = director.SpainPlan();
    }
```

#### ➕ Minimum code

- in `TourPlanBuilder interface` add method `newInstance()`
```java
public interface TourPlanBuilder {
    TourPlanBuilder newInstance();
}
```

- do not have to re-write all the attributes in `DefaultTourBuilder`

```java
public class DefaultTourBuilder implements TourPlanBuilder{
    private TourPlan tourplan; //now do not need all fields

    @Override
    public TourPlanBuilder newInstance() { //but need to initiate new instance
        this.tourplan = new TourPlan();
        return this;
    }

    @Override
    public TourPlanBuilder title(String title) {
        this.tourplan.setTitle(title);
        return this;
    }
}
```



## 👍🏻
- can create difficult instances easily
- can put orders in creating instances
- can put conditions in creating instances
- do not need so many constructors for all different cases

## 🛠️
- StringBuilder(`not synchronized`)
- can use `append()` to keep adding String

- Stream.builder()
- can use `add()`

- annotation `@Builder`
- creates builder for that class

- `UriComponentsBuilder`
- has methods such as `scheme()`, `host()`