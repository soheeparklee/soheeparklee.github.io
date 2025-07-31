---
title: Math/ String Buffer/ Time
categories: [JAVA, JAVA_Basics]
tags: [math, random, string, date, now] # TAG names should always be lowercase
---

## ✅ System Class(Utility class)

운영체게 시스템 관련 기능 수행<br>

- 입출력<br>
- 환경변수(컴퓨터 정보 뽑아내기)<br>
- 시간 측정 및 GC 호출<br>

## ✅ Math class

- 인스턴스 생성 불가
- private

절대값 `int absInt = Math.abs(-5);` =5 <br>
올림 `double ceil = Math.ceil(2.34);` <br>
내림 ` double floor = Math.floor(4.56);` <br>
반올림 ` double round = Math.round(2.34);` <br>
min `int largerInt = Math.min(2, 3);` <br>
max `float smallerFlt = Math.max(1.2f, 3.4f);` <br>
제곱 `double pow1 = Math.pow(4, 3);` <br>
루트 ` double pow2 = Math.pow(4, 0.5);` <br>
random한 수 ` double rand = Math.random();` <br>
<br>
1에서 10사이 무작위 정수 <br>

```java
int _1to10_1 = (int) Math.ceil(Math.random() * 10);
        int _1to10_2 = (int) Math.floor(Math.random() * 10) + 1;
```

## ✅ Random

` int randInt1 = random.nextInt();` <br>
<br>
0~10 사이 random `int randInt4 = random.nextInt(0, 10);` <br>
실행할 때마다 항상 똑같은 random 나오도록 해 `random.setSeed(1234);` <br>
참 거짓 random `boolean randBln1 = random.nextBoolean();` <br>

## ✅ BigInteger 클래스

## ✅ BigDecimal 클래스

부동소수점 오차 해결 <br>
그냥 `double num1 = 0.2 + 0.3f;`이렇게만 하면 0.5 안 나옴, 미세한 오류 발생 <br>

```java
float num6 = new BigDecimal("0.2")
                .add(new BigDecimal("0.3"))
                .floatValue();
```

## ✅ String Class

### 💡 `toString()`

String은 char[] 배열을 가진다. <br>
객체 정보를 문자열로 바꾸어 준다.<br>
사실 `println`, `printf`모두 `toString()`을 호출하는 메소드이다.<br>
원래는 `getClass().getName() + '@' + Integer.toHexString(hashCode())` 반환하는데 <br>
`toString()`쓰면 string으로 변환해서 반환<br>

#### 📍 Object의 `toString()` 메소드를 자식 클래스에서 오버라이딩 하기

```java
//toString() override하기 전
Customer customer= new Customer("So Hee");
System.out.println(customer) //exercise.chapter_43.Customer@67b64c45

//toString() override
//customer class
@Override
public String toString(){
  return String.format("Customer name: %s", this.name);
}
//Main.java
System.out.println(customer) //Customer name: So Hee
```

### 💡 `equals()`

두 인스턴스가 같은 객체인지 판단한다.<br>
두 대상의 **데이터 값 자체**를 비교한다 <br>
(하지만 override해서 같은 값을 비교하도록 만들 수 있음⭕️) <br>
<br>

**instance**: Heap에 저장<br>
**literal**: Constant Pool에 저장<br>

```java
Customer customer1= new Customer(123, "So Hee");
Customer customer2= customer1;
Customer customer3= new Customer(123, "So Hee");

String str1= "Cat";
String str2= "Cat";

customer1.equals(cusotmer2); //true
customer1.equals(customer3); //false
//customer 1,3 은 field는 같을지몰라도 저장된 공간은 다르니까

str1.equals(str2); //true
str1 == str2 //true


```

#### 📍 Object의 `equals()` 메소드를 자식 클래스에서 오버라이딩 하기

그래서 customer 1과 customer3 도 같게 만들겠다!<br>
컴퓨터 입장에서는 다를지도 모르지만, 사람 입장에서는 아이디 같으면 같은 사람이니까<br>

```java
//equals() override
//parameter로 받은 Obj가 비교하는 obj랑 같은지 보고 싶다.
@Override
public boolean equals(Object obj){
  //일단 obj가 null은 아니어야될거아니야
  if(obj==null){ return false; }
  //downcast-instanceof
  if(obj instanceof Customer){
    Customer customer= (Customer) obj;
    return customer.customerID == this.customerID
  }
  return false;
}

//Main.java
//이제 id가 같으면 같은 사람으로 판단, heap 메모리 주소는 다르더라도
customer1.equals(custotmer2); //true
customer1.equals(customer3); //true
```

#### 🆚 ==

**메모리 주소**를 기준으로 boolean값 반환 <br>
두 인스턴스의 Heap 주소 값을 비교하여 Boolean 값을 리턴<br>
같은 메모리값을 가리키고 있는가?<br>
`equals()` override해서 ID가 같으면 같은 사람 취급하라고 해도 말 안 들음 <br>
`==`과 `equals()`는 상관 없이 실행됨. <br>
`==`은 항상 **메모리값**이 기준(이게 바로 `equals()`와 차이점) <br>

```java
customer1 == customer2; //true
customer1 == customer3; // false
```

<img width="729" alt="스크린샷 2024-03-11 오후 3 49 25" src="https://github.com/soheeparklee/sc_project_carrotMkt_improved/assets/97790983/bbea44bd-a249-4aae-b5e3-626e96c5445b">

#### ⭐️ 여기서 잠깐!

```java
String str1= "Cat"; // Constant Pool에 저장
String str2= "Cat"; //따라서 메모리 주소 같음

String str3= new String("Cat"); //Heap에 저장
String str4= new String("Cat"); //메모리 주소 다름

```

### 💡 StringJoiner

문자열 배열을 받아서 여기에 들어온 문자열을 끊어주는 문자열, 그리고 그 문자열을 감쌀 기호 <br>
for문을 돌면서 add method로 넣는다. <br>
문자열을 여러 차례에 거쳐 차례차례 받아 실행 후 반환 <br>
String.join은 배열로만 받지만 StringJoiner는 배열도 받고 그냥 문자열도 하나하나 받음. <br>

{% raw %}

```java
String[] strAry = { "감자", "당근", "오이", "양파" };
        StringJoiner strJnr1 = new StringJoiner(",", "<", ">");
        StringJoiner strJnr2 = new StringJoiner(" / ", "{{ ", " }}");

        for (String s : strAry) {
            strJnr1.add(s);
            strJnr2.add(s);
        }
				strJnr1.add("고구마"); //String.join과 다르게 외부에서 추가되었을 때 추가 가능
				strJnr1.add("피망");
        String joined1 = strJnr1.toString(); //joined1: "<감자, 당근, 오이, 양파, 고구마, 피망 >"
        String joined2 = strJnr2.toString(); //joined2: "{{ 감자/ 당근/ 오이/ 양파}}
```

{% endraw %}

### 💡 StringBuffer Class

자주 변경해야 하는 문자열이 있을 때 <br>
예를 들어, 문자열을 여러 차례 이어붙일 때 <br>
`concat`도 있지만 `concat`은 변경할 때마다 저장해서 메모리를 많이 잡아먹는다면, <br>
`StringBuffer`는 변경사항 기억했다가 한 번에 저장해서 메모리를 효율적으로 사용한다. <br>
`.toString()`전까지는 머리속으로 변경사항 기억만 했다가, `.toString()`하면 그제야 종이에 적어 프린트 <br>
⭐️ `StringBuffer`에 추가할 때는 `append()`
<br>

- `String` : 변경이 있을 때마다 새 종이에 수정본을 작성하는 직원<br>
- `StringBuffer` : 컴퓨터로 수정작업을 진행하고 마지막에 프린트하는 직원<br>
  <br>

기본적으로 16개의 문자를 저장할 수 있는 공간을 가진다.<br>

```java
        StringBuffer strBffr1 = new StringBuffer(); // 기본: 16
        StringBuffer strBffr2 = new StringBuffer(2); // int로 16아닌 다른 값 지정 가능
        StringBuffer strBffr3 = new StringBuffer("Hello"); // 문자열 길이 + 16

   //  capacity 메소드 : 인스턴스의 문자 저장 공간 확인
        int[] capacities1 = {
                strBffr1.capacity(), strBffr2.capacity(), strBffr3.capacity()
        }; //[16, 2, 21]

        //  💡 값을 위와 같이 정한 이유:
        //  공간 증축(자원 소모)을 할 일을 최소화하도록 적당한 값을 준 것 뿐
        //  아래와 같이 문자들을 추가하면 필요한 만큼 증축됨
        //  append 메소드 : 인자로 주어진 문자열을 뒤에 이어붙임(StringBuffer: 아직까지는 저장하지 않고 변경사랑 기억만 해 둠)
        strBffr1.append("안녕하세요~!"); //자리 충분히 있으므로 증축 안 함
        strBffr2.append("안녕하세요~!"); //자리 2개밖에 없어 5개 증축해 capacity= 7
        strBffr3.append("안녕하세요~!");
        int[] capacities2 = {
                strBffr1.capacity(), strBffr2.capacity(), strBffr3.capacity()
        }; //[16, 7, 21]

        //  작업을 마친 뒤에는 toString 메소드로 문자열 생성 (최종본 프린트)
        String strBffr3Out = strBffr3.toString(); //Hello안녕하세요~!
```

### 💡 StringBuilder & append()

```java
//  StringBuilder도 동일한 기능들 가짐
        StringBuilder strBldr1 = new StringBuilder("한놈");
        strBldr1.append("두시기");

        //  append 메소드는 해당 클래스의 인스턴스 반환
        //  - method chaining
        strBldr1
                .append("석삼")
                .append("너구리")
                .append("다섯놈");

	String strBldr1Out = strBldr1.toString(); //저장string으로 변환하여 종이에 적어내기
        //한놈두시기석삼너구리다섯놈
```

### String Buffer 🆚 String Buffer

- common charecteristics:
  - make one class with `new`(mutable)
  - when caculating String, do not create new object, instead change size
  - can use same methods
- difference
  - StringBuffer: Thread safe
    - **multi** thread
    - `StringBuffer Class`: 멀티 스레드와 관련된 기능을 가지고 있다. 멀티쓰레드에서는 `StringBuffer`<br>
  - StringBuilder: **NOT** thread safe
    - **single** thread
    - `StringBuilder`: 멀티 스레드와 관련된 기능이 없어 단일 스레드에서는 StringBuilder사용<br>
      <br>

### 💡 delete/ deelteCharAt/ insert/ replace/ reverse

```java
StringBuilder strBldr2 = new StringBuilder("0123456789");

        String strBldr2Out1 = strBldr2 // 범위의 문자열 지움
                .delete(3, 7).toString();
//3~7번째까지 지움
//012789
String strBldr2Out2 = strBldr2 // 위치의 문자열 삭제
                .deleteCharAt(3).toString();
//3번째만 지움
//01289

        String strBldr2Out3 = strBldr2 // 위치에 문자열 추가
                .insert(2, "ABC").toString();

//01ABC289

        String strBldr2Out4 = strBldr2 // 범위의 문자열을 치환
                .replace(2, 4, "OneTwo").toString();
//01OneTwoC289

        String strBldr2Out5 = strBldr2 // 문자열 뒤집음
                .reverse().toString();
//982CowTenO10

// 💡 메서드 체이닝으로 한 번에
//.toString();으로 한 번에 적기
        String strBldr2ChainOut = new StringBuilder("0123456789")
                .delete(3, 7)
                .deleteCharAt(3)
                .insert(2, "ABC")
                .replace(2, 4, "OneTwo")
                .reverse()
                .toString();
```

### 💡 subString/ setLength/ capacity

`.toString()`: 전체를 다 string으로 만들기 <br>
`.substring()`: 콕 집어서 일부만 string으로 만들기 <br>

```java
StringBuilder strBldr3 = new StringBuilder("ABCDEFG");

        //기본적으로 16공간 가진다고 했잖아
        //  수동으로 저장공간 늘려주기
        //  - 작업할 전체 용량이 초기화 이후 계산되었을 때 유용
        strBldr3.setLength(100);  //strBldr3 : "ABCDEFG--------..."뒤로 빈 문자열 들어가 총 길이 100된다.
        int strBldr3Cap = strBldr3.capacity(); //strBldr3Cap : 100

        //  주어진 범위만 문자열로 반환
        String strBldr3Substr = strBldr3.substring(2, 5);
//2번째에서 5번째까지만 .toString();
//CDE
```

### 💡 CharSequence

```java
//  - String, StringBuffer, StringBuilder 모두  CharSequence를 implement
// 그래서 CharSequence로 세 기능 모두 사용 가능하다.
//  - Integer.parseInt 등의 메서드에 인자 타입으로 널리 사용
//  - 메소드들 살펴볼 것

        CharSequence cs1 = "ABC";
        CharSequence cs2 = new StringBuffer();
        CharSequence cs3 = new StringBuilder();
```

## ✅ java.time

클래스 메소드로 인스턴스 생성,<br>
클래스의 인스터스 반환<br>

### ⏰ now메소드

현재의 날짜, 시간 정보를 가진 해당 클래스의 인스턴스 반환 <br>
컴퓨터를 설정할 때 위치 정보 바탕으로 시간, 날짜 반환 <br>
<br>

#### 🕚 현재 날짜/시간 출력 <br>

```java
//🕚현재 날짜
LocalDate date = LocalDate.now();
//🕚현재 시간
LocalTime thisTime = LocalTime.now();
//🕚 현재 시간과 날짜 모두
LocalDateTime now = LocalDateTime.now();

```

### ⏰ of메소드 사용해 그 때의 날짜, 시간

```java
LocalDate christmas23 = LocalDate.of(2023, 12, 25);
LocalTime lunchTime = LocalTime.of(12, 30);
LocalDateTime familyDinner = LocalDateTime.of(2023, 12, 25, 18, 00);
```

### ⏰ 시간 더하고 빼기

java.time의 Local... 클래스 인스턴스들은 불변이다. <br>
constuctor 생성이 불가한 것은 사용자가 마음대로 인스턴스 생성하는 것을 제한하기 위함이다. <br>
그리고 날짜, 시간 빼거나 더해도 기존 인스턴스는 변하지 **않는다.** <br>
<br>
시, 분, 년, 월, 일을 더하거나 뺄 수 있다.<br>
주어진 차이만큼의 시간, 날짜를 새로 인스턴스를 만들어 반환한다.<br>

```java
LocalDate today = LocalDate.now();
today.plusDays(1); // ⭐️ 기존 인스턴스는 변하지 않음
LocalDate tomorrow = today.plusDays(1); //tomorrow라는 새로운 인스턴스
LocalDate yesterday = today.minusDays(1);
```

#### 💡 메서드 체이닝 사용<br>

```java
LocalTime thisTime = LocalTime.now();
LocalTime hourAndHalfLater = thisTime
                .plusHours(1)
                .plusMinutes(30);
```

### ⏰ ZoneDateTime

지역별 시간대(미국인지, 한국인지...)<br>
컴퓨터를 설정할 때 위치 정보 바탕으로 지금 어디있는지 위치정보까지 얻을 수 있음.<br>
<br>
of 사용해서 시간, 위치 정보 가지는 인스턴스 생성 가능<br>

```java
        //💡 ZonedDateTime : 시간대 정보를 추가로 가짐
        ZonedDateTime nowHere = ZonedDateTime.now();

        //  💡 현재 시간대 구하기
        String hereZone = nowHere.getZone().toString();

        //  💡 특정 지역의 특정 시간
        ZonedDateTime newYorkNewYear = ZonedDateTime.of(
                2023, 1, 1,
                0, 0, 0, 0,
                ZoneId.of("America/New_York")
        ); //  ⭐️ ZoneId 클래스에서 지역들 목록 볼 것
        //  서울에서는 오전 5시
```

### ⏰ period

시간 차이 구하기<br>
<br>
of 사용해 어떤 시간의 인스턴스 만들고<br>
현재 구해서<br>
시간이 얼마나 지났나? 구해보기<br>
년, 월, 일을 별도로 가져오기<br>

```java
//of 사용해 어떤 시간의 인스턴스 만들고
LocalDate childrensDay30 = LocalDate.of(2030, 5, 5);
//현재 구해서
LocalDate today = LocalDate.now();
//Period 사용해 차이 구하기
Period toChldDay30 = Period.between(today, childrensDay30);
//년, 월, 일을 별도로 가져오기
int[] toChldDay30inUnits = {
        toChldDay30.getYears(),
        toChldDay30.getMonths(),
        toChldDay30.getDays()
}
// 연, 월, 일 부분 각각 표시

```

### ⏰ duration

마찬가지로 얼마지났나 구하는데 <br>
각각을 일, 시, 분 초로 환산해야 함. <br>

```java
LocalDate today = LocalDate.now();
LocalDateTime year2000 = LocalDateTime.of(2000, 1, 1, 0, 0);

//  💡 Duration 클래스 : 두 시간 사이의 간격을 다루는 클래스
Duration from2000 = Duration.between(year2000, now);
long[] from2000inUnits = {
        from2000.toDays(),
        from2000.toHours(),
        from2000.toMinutes(),
        from2000.toSeconds()
};
// 일, 시, 분, 초 등의 단위로 환산 (위의 Period와 다름)
```

### ⏰ ofPattern

DateTimeFormatter 클래스의 ofPattern 메소드 사용 <br>
원하는 방식대로 시간 표시하기 위함 <br>
어떤 식으로 날짜 표시할지 형식 지정 <br>
for사용해 형식 바꿔서 문자열로 출력 <br>

#### 💡 형식에 따라 시간을 문자열로

```java
        DateTimeFormatter formatter1 =
                DateTimeFormatter.ofPattern("1. yyyy-MM-dd");

        DateTimeFormatter formatter2 =
                DateTimeFormatter.ofPattern("2. yyyy/MM/dd HH:mm:ss");

        DateTimeFormatter formatter3 =
                DateTimeFormatter.ofPattern("3. yy.MM.dd");

        for (DateTimeFormatter formatter : new DateTimeFormatter [] {
                formatter1,
                formatter2,
                formatter3,
        }) {
            //  💡 형식에 따라 시간을 문자열로
            System.out.println(now.format(formatter));
        }
```

#### 💡 반대로 문자열을 받아서 시간 인스턴스로 바꾸기

문자열에서 시간 인스턴스로 <br>

```java

        String christmas25str = "2025-12-25";
        DateTimeFormatter formatterA =
                DateTimeFormatter.ofPattern("yyyy-MM-dd");
        LocalDate christmas25 = LocalDate
                .parse(christmas25str, formatterA);
        //  ⚠️ 시간 정보는 없으므로 LocalDateTime으로 하면 오류 발생

        String christmas25dinnerStr = "2025/12/25 18:00:00";
        DateTimeFormatter formatterB =
                DateTimeFormatter.ofPattern("yyyy/MM/dd HH:mm:ss");
        LocalDateTime christmas25dinner = LocalDateTime
                .parse(christmas25dinnerStr, formatterB);
```

## ✅ `hashCode()`

객체의 해시 코드 반환<br>
우리가 원하는 값의 해시 코드로 override할 수 있음<br>

## ✅ `clone()`

자신과 같은 객체 복제<br>
override해서 자신을 복제할 떄 이런 값은 복제하고 이런 값은 복제 안하고~<br>
