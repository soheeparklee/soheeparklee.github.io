---
title: Enumeration
categories: [JAVA, JAVA_Basics]
tags: [enumeration] # TAG names should always be lowercase
---

### 사용 이유

불 꺼짐/ 불 켜짐 같은 특정 개수의 변수만 설정 가능하도록 하고 싶음
근데 `String light= "ON"` 이런식으로 정의했다가 대문자 빼먹으면 어떡함 ㅠㅠ

### 작성 방법

```java
//ButtonMode.java
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

### 클래스 내부에 바로 작성하기

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

### 열거형도 클래스처럼 필드, 생성자, 게터, 세터, 메소드를 가질 수 있다.

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

### 열거형의 메소드

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

#### 💡 values 메소드 : 전체 포함된 배열 반환

```java
 Students[] order = Students.values();

        for (Students person : order) {
            System.out.println(person.getDesc());
        }
```
