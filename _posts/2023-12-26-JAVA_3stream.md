---
title: Stream
categories: [JAVA, JAVA_Basics]
tags: [stream] # TAG names should always be lowercase
---

## ✅ Stream API

> 함수형 프로그래밍을 도입하여 컬렉션, 배열 등의 처리/조작을 간단/효율적으로 하는 API <br>
> Stream은 generic <br>

- JAVA 8 이전에는 배열 또는 컬렉션을 다룰 때 `for`, `foreach`문을 돌면서 요소 하나씩을 꺼내서 다루었음
- JAVA 8 부터는 또 다른 방법으로 컬렉션 및 배열의 요소를 **반복 처리**하기 위해 **스트림**을 사용할 수 있게 되었다.

### ☑️ 사용 이유

- 가독성 향상 <br>
- 병렬 연산 가능(하나의 작업을 여러개로 잘게 나눠서 동시에 처리) <br>
- 배열 또는 컬렉션에 함수 여러개를 조합해서 원하는 결과를 필터링하고 가공된 결과를 얻는다. <br>

### 외부 반복자 🆚 내부 반복자

- 외부 반복자: 컬렉션의 요소를 컬렉션 **외부**에서 반복해 가져와 처리
  - Collection: `for`, `iterator`. `for-each`
  - save all value on memory
- 내부 반복자: 요소 처리 방법을 컬렉션 **내부**로 주입시켜서 요소를 반복 처리
  - 작업을 병렬처리 가능
  - 스트림

#### 🆚 iterator, iterable

- 공통점: Java Collection Framework
- iterator:
  - iterate within collection(list, set)
  - get value from collection using `hasNext()`, `next()`

<br>

- iterable: interface to get iterator

### ☑️ 스트림 단계

> 생성 → 매핑 → 필터링 1 → 필터링 2 → 결과 만들기 → 결과물

#### 1️⃣ **생성** <br>

#### 2️⃣ **중간연산** <br>

중간 연산은 여러개 실행 가능<br>

- filtering
- mapping
- sorting
- looping `peek`

#### 3️⃣ **최종연산** <br>

한 번만 실행할 수 있음<br>
진행 연산을 닫고 최종 값 산출<br>

- looping `forEach`
- matching
- aggregate 집계
- collecting

<img width="720" alt="Screenshot 2024-05-30 at 16 40 32" src="https://github.com/soheeparklee/sc_FrontBackTryout/assets/97790983/2cbb513a-05c5-48ee-9f6a-05cf7ddc9385">

<img width="625" alt="스크린샷 2023-12-27 오후 10 30 32" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/96f1c0ec-93ec-436e-8f90-db76abc36332">

### ☑️ 스트림 특징

1️⃣ Stream은 기존 자료를 변형할 수 없다. <br>
예를 들어 `Collection(=List) -> Stream`로 정의했을 때, List는 변하지 않는다. <br>

2️⃣ Stream은 최종연산 후에는 **재사용 불가** <br>

## ✅ Stream API 사용하기

### 정의 방법

⭐️ `Stream.of` <br>
⭐️ `Arrays.stream()` <br>
⭐️ `Collection(List, Set) -> Stream` 인터페이스에 디폴트 메소드로 스트림 사용 가능<br>

### Stream 정의하기

```java
public class StreamTest1 {
    public static void main(String[] args) {
        //⭐️ Stream.of
        //stream is generic
        Stream<String> stringStreamOf= Stream.of("Apple", "Banana", "Cherry");
        Stream<Integer> integerStreamOf= Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

        //⭐️ Arrays.Stream
        Stream<String> stringArraysStream= Arrays.stream(new String[] {"Apple","Banana", "Cherry" });
        Stream<Integer> integerArrayStream= Arrays.stream(new Integer[] {1, 2, 3, 4, 5, 6, 7, 8, 9, 10});

        //⭐️ Collection(=List) -> Stream
        //리스트 만들고
        List<String> stringList= new ArrayList<>();
        stringList.add("Orange");
        stringList.add("Pear");
        stringList.add("Mango");
        //stream으로 정의
        Stream<String> stringListStream= stringList.stream();

        List<Integer> integerList= new ArrayList<>();
        integerList.add(1);
        integerList.add(2);
        integerList.add(3);
        integerList.add(4);

        Stream<Integer> integerListStream= integerList.stream();
    }
}

```

## ☑️ stream으로 for-loop개선하기

⭐️ **stream은 1회용이다.** ⭐️ <br>
stream을 for each나 filter사용해서 변형하면, 또 사용할 수는 없음 <br>
따라서 integerListStream는 다시 사용 ❌ (stream 특징2) <br>
그러나 원본 데이터 integerList는 또 사용 가능 ⭕️ <br>
원본 데이터 integerList는 변하지 않았을 것이다. (stream 특징1)<br>

```java
        //for-loop으로 정의
        for(String fruit: stringList){
            System.out.println("for loop fruit"+ fruit.toUpperCase());
        }

        for(Integer num:integerList){
            if(num%2 == 0){
                System.out.println("for loop even number"+ num);
            } else continue;
        }
//결과
//stream fruitORANGE
//stream fruitPEAR
//stream fruitMANGO

        //⭐️ for-loop 대신 Stream
        //💡for each
        stringListStream.forEach((fruit)-> System.out.println("stream fruit"+ fruit.toUpperCase() ));
        //💡filter: 이 조건을 만족하는 것만
        integerListStream.filter((num)-> num%2 ==0).forEach(num-> System.out.println("filter, forEach even number"+ num));
//결과
//filter, forEach even number2
//filter, forEach even number4

        //💡filter2개 이상 섞어서도 가능
        integerListStream.filter((num)-> num%2 ==0)
                .filter((num)-> num>4)
                .forEach((num)-> System.out.println("filter, forEach even number"+ num));

        //stream은 1회용이다.
        //stream을 for each나 filter사용해서 변형하면, 또 사용할 수는 없음
        //따라서 integerListStream는 다시 사용 ❌
        //그러나 원본 데이터 integerList는 또 사용 가능⭕️

```

## ✅ Stream API **중간** 연산

### 💡 filter(조건), distinct()

> 조건에 맞는 요소를 걸러내기

- filter(조건): 조건식 만족하는 요소만 남기기 <br>
- distinct(): 중복되는 요소는 제거해버림 <br>

```java
public class StreamIntermediateOopsTest {

    public static void main(String[] args) {
        List<String> fruitList = new ArrayList<>();
        fruitList.add("Orange");
        fruitList.add("Apple");
        fruitList.add("Pear");
        fruitList.add("Mango");
        fruitList.add("Apple");
        fruitList.add("Pineapple");
        fruitList.add("Grape");
        fruitList.add("Strawberry");
        fruitList.add("Apple");
        fruitList.add("Watermelon");

        //💡 filter(조건)
        //fruit 길이가 6이상
        fruitList.stream().filter((fruit)->fruit.length() >= 6)
                .forEach((fruit)-> System.out.println(fruit+ " ")); //Orange Pineapple Strawberry Watermelon
        //💡distinct()
        List<String> fruitDistinctList= fruitList.stream().distinct().collect(Collectors.toList());
        System.out.println(fruitList); //[Orange, Apple, Pear, Mango, Apple, Pineapple, Grape, Strawberry, Apple, Watermelon]
        System.out.println(fruitDistinctList); //[Orange, Apple, Pear, Mango, Pineapple, Grape, Strawberry, Watermelon]
        //// 중복되는 Apple다 지웠음
    }
}

```

### 💡 map(함수)

> 스트림의 요소를 다른 요소로 변환하는 중간 처리 기능<br>
> 이 때 값을 변환하기 위한 람다를 인자로 받는다. <br>

특정 함수에 매핑, 새로운 요소 반환 <br>
get함수 쓰면 원하는 요소만 추출도 가능 <br>

```java
        //💡 map(함수)
        fruitList.stream().map((fruit)->fruit.toUpperCase())
                .forEach((fruit)-> System.out.println(fruit)); //fruitList대문자로 바꿔 반환
        //List로 만든다음 map
        List<String> fruitMapList= fruitList.stream().map((fruit)->fruit.toUpperCase()).collect(Collectors.toList());
        System.out.println("map"+ fruitMapList); //[ORANGE, APPLE, PEAR, MANGO, APPLE, PINEAPPLE, GRAPE, STRAWBERRY, APPLE, WATERMELON]
        //map으로 list datatype도 자유자재로 바꿀 수 있다. (String-> Interger)
        List<Integer> fruitMapList2= fruitList.stream().map((fruit)->fruit.length()).collect(Collectors.toList());
        System.out.println("integer map"+ fruitMapList2); //[6, 5, 4, 5, 5, 9, 5, 10, 5, 10]
```

### 💡 limit(max), skip(n)

limit(max): 최대 요소 개수 지정, stream 제한 <br>
앞에 max개만 가지고 동작 <br>
skip(n): 처음 n개 요소 제외하고 stream 재생성 <br>
앞에 n개 뛰어넘고 나머지 가지고 동작 <br>

```java
        //💡 limit(max), skip(n)
        fruitList.stream().limit(3).forEach((fruit)->System.out.println(fruit)); //가장 앞에 3개
        List<String> fruitLimitList= fruitList.stream().limit(3).collect(Collectors.toList());
        System.out.println("limit"+ fruitLimitList); //[Orange, Apple, Pear]
        //💡skip(n)
        fruitList.stream().skip(5).forEach((fruit)->System.out.println(fruit)); //앞에 5개 뛰어넘고 출력
        List<String> fruitSkipList= fruitList.stream().skip(5).collect(Collectors.toList());
        System.out.println("skip"+ fruitSkipList); //[Pineapple, Grape, Strawberry, Apple, Watermelon]
```

### 💡 sorted() 정렬

> 요소를 오름차순 또는 내림차순으로 정렬하는 중간 기능 <br>

요소를 특정 정렬 순서에 따라 생성 <br>
특정 기준 안 주면 알파벳 순, 오름차순 <br>

**Comparable 구현 객체의 정렬**<br>
객체가 Comparable을 구현하고 있어야만 `sorted()`메소드 사용 가능 <br>
만약 내림차순으로 정렬하고 싶다면, `Comparator.reverseOrder()` <br>

**Comparator를 이용한 정렬**<br>
특정 순서를 지정하기 위해서는 **JAVA comparator** 람다 인터페이스 가지고 지정 <br>
오름차순 `(s1, s2)->s1.getScore() - s2.getScore()` <br>
내림차순 `.sorted((s1, s2)-> s2.getScore() - s1.getScore())`<br>

```java
        //💡 sorted()
        List<String> fruitSortedList= fruitList.stream().sorted().collect(Collectors.toList());
        System.out.println("sorted: "+ fruitSortedList);
        //아무 sort 조건을 적용하지 않으면 알파벳순, 오름차순
        //[Apple, Apple, Apple, Grape, Mango, Orange, Pear, Pineapple, Strawberry, Watermelon]

        // ⭐JAVA comparator 이용해서 나만의 정렬 기준 설정 가능
        List<String> fruitSortedComparatorList= fruitList.stream().sorted((fruit1, fruit2)-> fruit1.length() - fruit2.length()).collect(Collectors.toList());
        System.out.println("sortedComparator: "+ fruitSortedComparatorList);
        //긴 글자일수록 뒤로 가는 정렬 기준
        //[Pear, Apple, Mango, Apple, Grape, Apple, Orange, Pineapple, Strawberry, Watermelon]
```

## ✅ Stream API **최종** 연산

### 💡 Looping

> Looping은 스트림에서 요소를 하나씩 반복해서 가져와 처리하는 것 <br> > `forEach()`, `peek()` 두 가지 메소드가 있다. <br>

- `peek()`: 중간 처리 메소드
- `forEach()`: 최종 처리 메소드

lambda식에서 parameter하나 받아서 void반환 <br>
대부분 요소 출력에 사용 <br>

```java
public class StreamTerminalOopsTest {

    public static void main(String[] args) {
        List<String> fruitList = new ArrayList<>();
        fruitList.add("Orange");
        fruitList.add("Pear");
        fruitList.add("Mango");
        fruitList.add("Pineapple");

        List<Integer> numList= new ArrayList<>();
        numList.add(1);
        numList.add(2);
        numList.add(3);
        numList.add(4);
        numList.add(5);

//💡 forEach() 출력
        fruitList.stream().forEach((fruit)->System.out.println("forEach: " + fruit));
    }
}

```

### 💡 Match()

> 요소가 특정 조건에 만족하는지 여부 조사하는 최종 처리 기능 <br>

- `anyMatch()`: 하나라도 조건을 만족하는 요소가 있는지
- `allMatch()`: 모두 조건을 만족하는지
- `noneMatch()`: 모두 조건을 만족하지 않는지

### 💡 Aggregate: findFirst() 검색

Stream 첫 번째 값 가져오는데, <br>
단, Optional<T>로 반환한다. <br>

```java
//💡 findFirst() 첫 번째 값 검색
        Optional<String> fruitOptional= fruitList.stream().findFirst();
        System.out.println("Optional Fruit: "+ fruitOptional.orElseGet(()-> "Default fruit")); //Optional Fruit: Orange
```

### 💡 Aggregate: sum(), average()

Stream 요소들의 총합 연산 진행 <br>
**숫자** Stream만 사용 가능 <br>
⭐️ mapToInt() <br>

```java
//💡 sum(), average()
// ⭐️ mapToInt()를 해 주어야 한다.
//numList에는 1,2,3,4,5숫자가 들어있는 상황
        System.out.println("Sum: "+ numList.stream().mapToInt((i)->i).sum()); //Sum: 15
        System.out.println("Average: "+numList.stream().mapToInt((i)-> i).average()); //Average: OptionalDouble[3.0]
```

### 💡 Aggregate: count(), max(), min()

`count()` Stream길이 <br>
`max()`, `min()` Stream에서 가장 큰 값/작은 값 <br>
마찬가지로 숫자 Stream만 사용 가능 <br>
⭐️ mapToInt() <br>

```java
//💡 count(), max(), min()
        System.out.println("Count: "+numList.stream().count()); //Count: 5
        System.out.println("Max: " + numList.stream().mapToInt((i)->i).max()); //Max: OptionalInt[5]
```

### 💡 reduce() 소모

lambda식으로 특정한 규칙을 지정 가능 <br>
identity(초기값)와 연산 <br>

```java
//💡 reduce() 내가 규칙 정하기
        //0 은 초기값, 2개의 Parameter를 넣어야 한다.
        //0에서 시작해서 0에서 1빼고, -1에서 2빼고, -3에서 3빼고...
        int result= numList.stream().reduce(0, (int1, int2)-> int1 - int2);
        System.out.println("Reduce: "+ result); //Reduce: -15
```

### 💡 collect() 수집(=컬렉션 변환)

> 요소들을 필터링 또는 매핑 후 수집해서 반환하는 최종 처리 메소드 <br>

대부분 컬렉션 변환용으로 사용 <br>
모아서(collect) set으로 반환한다. <br>

- `.collect(Collectors.toSet())`
- `.collect(Collectors.toList())`
- `.collect(Collectors.joining())`

```java
//💡 collect() 수집(=컬렉션 반환)
//set을 사용해 string으로 바꾸기
        Set<String> fruitSet= fruitList.stream().collect(Collectors.toSet()); //fruitSet: [Pear, Mango, Pineapple, Orange]
        System.out.println("fruitSet: " + fruitSet);
```

## ☑️ 고객 이름, 고객 비용 다 더하기

Travel 고객의 이름, 총 비용 뽑아오기 <br>

```java
//TravelCustomer.java
public class TravelCustomer {
    private String name;
    private int age;
    private int price;

    public TravelCustomer(String name, int age, int price) {
        this.name = name;
        this.age = age;
        this.price = price;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public int getPrice() {
        return price;
    }

    @Override
    public String toString() {
        return "TravelCustomer{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", price=" + price +
                '}';
    }
}

//TravelTest.java
public class TravelTest {

    public static void main(String[] args){
        // List
        List<TravelCustomer> customers = new ArrayList<>();
        customers.add(new TravelCustomer("아이유", 29, 200000));
        customers.add(new TravelCustomer("박보검", 28, 180000));
        customers.add(new TravelCustomer("송중기", 36, 250000));
        customers.add(new TravelCustomer("김태리", 32, 220000));
        customers.add(new TravelCustomer("전정국", 24, 190000));


        // 1. 고객 명단 이름, 추가된 순서로 출력
        customers.stream()
                .map((customer)-> customer.getName())
                .forEach((name)->System.out.println(name));

        // 2. 총 고객들의 여행 비용 계산
        long total= customers.stream()
                .map((customer)->customer.getPrice())
                .mapToInt((i)->i)
                .sum();
        System.out.println(total);
        //1040000

    }
}
```

### ✔️ 90점 넘는 학생, 중위값 구하기

```java
//Student.java
public class Student {
    // 속성 (1) 학교 정보
    private int schoolYear; // 몇 학년
    private int classroomNumber; // 몇 반
    private int studentNumber; // 학번

    // 속성 (2) 학생 개인정보
    private String name; // 이름 // 단축키 Ctrl + 마우스
    private String gender; // 성별

    private int score;

    // 행위
    public String getName(){
        return this.name;
    }
    public void setName(String name) {
        this.name = name;
    }

    public int getScore() {
        return score;
    }

    Student(){
        this("unknown", "unknown");
    }
    Student(String name, String gender){
        this(name, gender, 5, 10 , 0, 0);
    }

    Student(String name, String gender, int score){
        this(name, gender, 5, 10 , 0, score);
    }
    Student(String name, String gender, int schoolYear, int classroomNumber, int studentNumber, int score){
        this.name = name;
        this.gender = gender;
        this.schoolYear = schoolYear;
        this.classroomNumber = classroomNumber;
        this.studentNumber = studentNumber;
        this.score = score;
    }
}

//ScoreTest.java
public class ScoreTest {
    public static void main(String[] args){
        // List 제공
        List<Student> students = new ArrayList<>();

        students.add(new Student("Kim", "여자", 95));
        students.add(new Student("Park", "여자", 100));
        students.add(new Student("Lee", "남자", 92));
        students.add(new Student("Jun", "남자", 90));
        students.add(new Student("Han", "여자", 85));
        students.add(new Student("Kang", "남자", 88));
        students.add(new Student("Song", "남자", 70));
        students.add(new Student("Sin", "여자", 63));
        students.add(new Student("Bang", "여자", 68));
        students.add(new Student("Ha", "남자", 75));
        students.add(new Student("Choi", "남자", 80));

        // 1. 90점 넘는 학생들 이름 구하기
        students.stream()
                .filter((student)-> student.getScore()>= 90)
                .map((student)-> student.getName())
                        .forEach((name)-> System.out.println(name));


        // 2. 중위값 구하기
        long size= students.stream().count();
        int medium= students.stream()
                .map((student)-> student.getScore())
                .sorted()
                .skip(size/2)
                .findFirst().orElseGet(() -> 0);
        System.out.println(medium);

        //3. 남학생들 중 가장 낮은 성적을 가진 학생의 이름 출력하기
        String boy= students.stream()
        .filter((student)->student.getGender().equals("남자") )
        .min((s1, s2)->s1.getScore() - s2.getScore())
        .map((student)->student.getName())
        .orElse("N/A");

        //4. 여학생들 중 성적 상위 3명의 평균 성적 구하기
            double girlCount= students.stream()
            .filter((student)->student.getGender().equals("여자"))
            .count();

    double averageGirlStudents = girlCount<3 ? 0:
                    students.stream()
                    .filter((student)->student.getGender().equals("여자"))
                    .sorted((s1, s2)-> s2.getScore() - s1.getScore())
                    .limit(3)
                    .mapToInt((student)-> student.getScore())
                    .average()
                    .orElse(0);

    System.out.println(averageGirlStudents);
    }
}

```

## ✅ 요소 병렬 처리

> 병렬 처리란, 멀티코어 CPU환경에서 전체 요소를 분할해 각각의 코어가 병렬적으로 일을 처리하는 것<br>
> 목적: 작업 처리 시간 줄이기<br>
> 병렬 스트림 parallel stream이 요소 병렬 처리의 예이다<br>

- 동시성: 멀티 스레드가 하나의 코어에서 번갈아가며 실행됨(1명이 5개의 작업 번갈아가며 하기)
- 병렬성: 멀티 코어를 각각 이용해서 병렬로 실행(5명이 5개의 작업)
  - 데이터 병렬성: 전체 데이터를 분할해 서브 데이터셋으로 만들고 이 서브 데이터셋들을 병렬 처리
  - 작업 병렬성: 서로 다른 작업을 병렬 처리

### 💡 병렬 스트림 사용

- `parallelStream()`: 컬렉션으로부터 병렬 스트림을 바로 리턴
- `parallel()`: 기존 스트림을 병렬 처리 스트림으로 변환

### 💡 포크조인 프레임워크

자바 병렬 스트림은 요소들을 병렬 처리하기 위해 `ForkJoin FrameWork` 사용 <br>

- Fork: 전체 요소들을 서브 요소셋으로 분할, 각각의 서브 요소셋을 멀티 코어에서 병렬 처리
- Join: 서브 결과를 결합해 최종 결과 도출

<img width="709" alt="Screenshot 2024-05-30 at 17 08 16" src="https://github.com/soheeparklee/sc_FrontBackTryout/assets/97790983/55a6940d-4d00-4f8b-af2e-c277b2f9f94d">

## ✅ Stream의 장점, 문제점

- 👍🏻 선언형, 간결하고 가독성이 좋다
- 👍🏻 조립 가능, 유연성
- 👍🏻 병렬화, 처리 성능 향상
- 👎🏻 메모리 부족 문제
- 👎🏻 느린 처리 속도
- 👎🏻 어려운 디버깅
- 상태 변경 불가: 한번 생성 이후에는 상태 변경 불가, 결과를 다시 사용하려면 새로운 스트림 생성 필요
