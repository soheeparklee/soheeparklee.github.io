---
title: Enumeration
categories: [JAVA, JAVA_Basics]
tags: [enumeration] # TAG names should always be lowercase
---

## ✅ 현실세계 열거타입

**열거형 타입**: 특정 타입이 몇 가지 한정된 값을 가지는 타입 <br>
선택지가 선택된 타입 <br>

<br>
<br>
예시: <br>

- 게절(봄, 여름, 가을 겨울)
- 3단계 평가(잘 함/ 보통/ 노력 요함)
- 요일

## ✅ Enum

자바 Enum이 바로 열거형 타입 <br>
Enum의 각각 요소는 독립된 **특수한 틀래스**로 구분되는 **인스턴스**이다. <br>

<img width="805" alt="스크린샷 2023-12-25 오후 7 24 32" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/4743d09d-30b6-44dd-8cf5-e9da212b0398">

### 👍🏻 사용 이유

1. 가독성 향상 <br>
2. 허용 가능한 값 제한 ➡️ 유형 안정성 제공 <br>
   불 꺼짐/ 불 켜짐 같은 특정 개수의 변수만 설정 가능하도록 하고 싶음 <br>
   근데 `String light= "ON"` 이런식으로 정의했다가 on 이렇게 대문자 빼먹으면 어떡함 ㅠㅠ <br>
3. final 필드 추가 <br>
4. switch와 함께 쓰면 매우 강력 <br>

### ✔️ 작성 방법

```java
//ButtonMode.java
//enum은 대문자로 적는다.
public enum ButtonMode {
    LIGHT, DARK
}
//ButtonType.java
public enum ButtonType {
    WOOD, STEEL, PLASTIC
}
//Main.java
Button button1 = new Button();
button1.setButtonMode(ButtonMode.DARK);
button2.setButtonType(ButtonType.PLASTIC)
```

### ✔️ 클래스 내부에 바로 작성하기

```java
//Button.java
public class Button {
    enum Mode { LIGHT, DARK }
    enum Type { WOOD, STEEL, PLASTIC }

    private Mode mode = Mode.LIGHT;
    private Type type = Space.PLASTIC;

    public void setMode(Mode mode) {
        this.mode = mode;
    }

    public void setType(Type type) {
        this.type = type;
    }
}

//Main.java
Button button1 = new Button();
button1.setButtonMode(ButtonMode.DARK);
button2.setButtonType(ButtonType.PLASTIC)
```

### ✔️ 열거형도 클래스처럼 필드, 생성자, 게터, 세터, 메소드를 가질 수 있다.

```java
//enum
public enum Students{
    SH("So Hee", 10, 1),
    CS("Cesar", 15, 0),
    KT("KyuTae", 4, 0)

    //enum의 field
    private String name;
    private int age;
    private int gender;
    //enum constructor
    Students(Stirng name, int age, int gender){
        this.name= name;
        this.age= age;
        this.gender= gender;
    }
    //enum getter, setter
    public String getName(){return name;}
    public int getAge(){return age;}
    public void setAge(int age){
        this.age= age;
    }
    //enum method
    public String getDesc(){
        String stickers="";
        if(age > 8){
            stickers= "🏆".repeat(age);
        }
        return "%s 학생은 %s살입니다. ".formatted(name, age);
    }
}

//Main.java

Students students1= Students.SH;
Students students2= Students.CS;
Students students3= Students.KT;
//getter
String studentName= students1.getName();
int studentAge= students2.getAge();
String studentDesc= students2.getDesc()
//setter
students3.setAge(24); //규태 이제 24살 됨
```

### ✔️ 열거형의 메소드

#### 💡 valueOf 메소드

```java
Students.valueOf("SH")

//SH라는 문자를 가진 학생 반환
```

#### 💡 name 메소드 : 각 항목의 이름 반환

```java
student.name()
//각 항목의 이름을 string으로 반환
```

#### 💡 ordinal 메소드 : 순번 반환

```java
int[] standInLine = new int[] {
                student1.ordinal(), student2.ordinal(), student3.ordinal()
        };
```

#### 💡 compareTo: 순번을 비교

열거 객체를 비교하여 순번 차이를 리턴
누가 앞에/뒤에 있는가?

#### 💡 values 메소드 : 전체 포함된 배열 반환

```java
 Students[] order = Students.values();

        for (Students person : order) {
            System.out.println(person.getDesc());
        }
```

```java
public class DayEnumTest {
    public static void main(String[] args) {
        //각자 enum값 정의
        Day monday= Day.MONDAY;
        Day thursday= Day.THURSDAY;
        Day sunday= Day.SUNDAY;

        //💡Ordinal
        System.out.println("Monday ordinal "+ monday.ordinal()); //1
        System.out.println("Thursday ordinal "+ thursday.ordinal()); //4

        //💡CompareTo
        //어떤 값이 더 빨리/뒤에 오는가?
        System.out.println("Monday ordinal "+ monday.compareTo(thursday)); // 1 - 4= -3
        System.out.println("Monday ordinal "+ monday.compareTo(sunday)); // 1 - 0 = 1
        //💡values
        //array로 출력해야
        Day[] days= Day.values();
        System.out.println(Arrays.toString(days)); //[SUNDAY, MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY]
    }
}

```
