---
title: Stream
categories: [JAVA, JAVA_Basics]
tags: [stream] # TAG names should always be lowercase
---

## ✅ Stream API

함수형 프로그래밍을 도입하여 컬렉션, 배열 등의 처리/조작을 간단/효율적으로 하는 API <br>
Stream은 generic <br>

### ☑️ 사용 이유

- 가독성 향상 <br>
- 병렬 연산 가능 <br>

### ☑️ Stream 단계

1. 생성 <br>
2. 중간연산 filter <br>
3. 최종연산 forEach <br>

<img width="625" alt="스크린샷 2023-12-27 오후 10 30 32" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/96f1c0ec-93ec-436e-8f90-db76abc36332">

### ☑️ 특징

#### 1️⃣ Stream은 기존 자료를 변형할 수 없다.

예를 들어 `Collection(=List) -> Stream`로 정의했을 때, List는 변하지 않는다. <br>

#### 2️⃣ Stream은 최종연산 후에는 **재사용 불가**

## ✅ Stream API 사용하기

### 정의 방법

⭐️ `Stream.of` <br>
⭐️ `Arrays.Stream` <br>
⭐️ `Collection(=List) -> Stream` <br>

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

⭐️ stream은 1회용이다. <br>
stream을 for each나 filter사용해서 변형하면, 또 사용할 수는 없음 <br>
따라서 integerListStream는 다시 사용 ❌ (stream특징 2️⃣) <br>
그러나 원본 데이터 integerList는 또 사용 가능⭕️ <br>
원본 데이터 integerList는 변하지 않았을 것이다. (stream특징 1️⃣) <br>

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

        //⭐️ Stream in for-loop
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
                .forEach(num-> System.out.println("filter, forEach even number"+ num));

        //stream은 1회용이다.
        //stream을 for each나 filter사용해서 변형하면, 또 사용할 수는 없음
        //따라서 integerListStream는 다시 사용 ❌
        //그러나 원본 데이터 integerList는 또 사용 가능⭕️

```

## ✅ Stream API 최종 연산

### 💡 forEach() 출력

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

### 💡 collect() 수집(=컬렉션 변환)

대부분 컬렉션 변환용으로 사용 <br>
빼오기 <br>

```java
//💡 collect() 수집(=컬렉션 반환)
//set을 사용해 string으로 바꾸기
        Set<String> fruitSet= fruitList.stream().collect(Collectors.toSet()); //fruitSet: [Pear, Mango, Pineapple, Orange]
        System.out.println("fruitSet: " + fruitSet);
```

### 💡 findFirst() 검색

Stream 첫 번째 값 가져오는데, <br>
단, Optional<T>로 반환한다. <br>

```java
//💡 findFirst() 첫 번째 값 검색
        Optional<String> fruitOptional= fruitList.stream().findFirst();
        System.out.println("Optional Fruit: "+ fruitOptional.orElseGet(()-> "Default fruit")); //Optional Fruit: Orange
```

### 💡 sum(), average()

Stream 요소들의 총합 연산 진행 <br>
숫자 Stream만 사용 가능 <br>
⭐️ mapToInt() <br>

```java
//💡 sum(), average()
// ⭐️ mapToInt()를 해 주어야 한다.
        System.out.println("Sum: "+ numList.stream().mapToInt((i)->i).sum()); //Sum: 15
        System.out.println("Average: "+numList.stream().mapToInt((i)-> i).average()); //Average: OptionalDouble[3.0]
```

### 💡 count(), max(), min()

Stream길이 <br>
Stream에서 가장 큰 값/작은 값 <br>
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
        //0 은 초기값
        int result= numList.stream().reduce(0, (int1, int2)-> int1 - int2);
        System.out.println("Reduce: "+ result); //Reduce: -15
```

## ✅ Stream API 중간 연산

### 💡 filter(조건), distinct()

filter(조건): 조건식 만족하는 요소만 남겨 <br>
distinct(): 중복되는 요소는 제거해버림 <br>

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

요소를 특정 정렬 순서에 따라 생성 <br>
특정 기준 안 주면 알파벳 순, 오름차순 <br>
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

### ☑️ 90점 넘는 학생, 중위값 구하기

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
