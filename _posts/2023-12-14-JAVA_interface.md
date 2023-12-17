---
title: Interface
categories: [JAVA, JAVA_Basics]
tags: [super, override, extends, default] # TAG names should always be lowercase
---

## ✅ Interface

인간이나 사물, 시스템 간에 **커뮤니케이션**이 가능하도록 설계한 상호 작용 방식 <br>

### 1. 유저 인터페이스 UI<br>

인간(유저)와 사물/시스템 <br>
유저가 편하게 사물/시스템과 통신할 수 있도록 도와주는 것 <br>

#### 하드웨어 유저 인터페이스

인간 <-----> 자동차 핸들 <-----> 자동차<br>
인간 <-----> 리모콘 <-----> 텔레비전 <br>

#### 소프트웨어 유저 인터페이스<br>

GUI(graphic user interface)<br>
application<br>

2. 시스템 인터페이스 SI <br>
   시스템과 시스템이 상호작용 <br>
   사물/시스템 <----> 사물/시스템 <br>

#### 하드웨어 시스템 인터페이스 <br>

케이블, USB <br>

#### 소프트웨어 시스템 인터페이스 <br>

API(앱을 프로그래밍해서 통신하는 인터페이스) <br>
JAVA의 인터페이스(자바의 객체끼리 통신하기 위한 인터페이스) <br>

## ✅ JAVA OOP Interface: 소통

자바 **객체**간 소통이 가능하도록 기능 구현을 설계(메소드)하는 추상화 문법 <br>
인터페이스: 객체들이 이렇게 소통하자! 약속을 정의한 메소드 <br>

### ⭐️ interface 특징

#### 다중 적용 가능

- 하나의 클래스가 여러개의 interface implement가능

#### 생성자 ❌

- interface는 사실 다 abstract임. <br>
- 생성자 필요없음. (`new...`필요 없음 <br>❌)
- 즉, instance를 생성하지 않고도 실행 클래스에서 바로 불러오기 가능

#### interface 의 field는 `public static final` <br>

- 필드 앞에 자동으로 `public static final`이 붙는다. <br>
- 그래서 field를 정할 때 초기값을 무조건 정해줘야 한다. <br>
- 그래서 implement한 class에서는 값을 바꿀 수 없다. Final이니까. <br>

interface 의 메소드는 `public abstract`<br>

- interface 에서는 그냥 메소드 이름만 쓰면 끝 <br>

#### method 구현 override 의무

- 메소드 구현 의무: implement하는 class는 무조건 override해 줘야 함. <br>

### interface정의 방법

```java
public interface Flyable {
    //field
    long atomsphereLimit= 476; //field 꼭 초기값 정해주어야 한다.
    //method
    //이름만 선언하면 끝임
    //Flyable class를 implement한다면 꼭 override 해야 함.
     void fly();
}
```

### interface로도 instance type을 정의할 수 있다.

```java
        //실행 클래스
        //interface로도 인스턴스 타입을 정의할 수 있다.
        //이제 인스턴스 타입  bird의 경우 세 가지나 할 수 있음!!
        Flyable bird1= new Bird();
        Bird bird2 = new Bird();
        Animal bird3= new Bird();
```

### interface로 타입 정의한 인스턴스는 원래 인스턴스 메소드 사용 ❌

interface로 타입 정의한 인스턴스는 그 인스턴스의 메소드는 더 이상 쓸 수 없고, <br>
interface에서 정의한 메소드만 사용 가능 <br>

```java
Flyable bird= new Bird();
Flyable airplane= new Airplane("AB007");
//interface method⭕️
bird.fly();
airplane.fly();
// 기존 instance에서 정의한 Method는 더 이상 사용 불가
//⭐️ 왜냐하면 bird를 flyable(instance type을 interface로 설정했기 떄문이다. )
bird.eat(); //❌
```

#### 💡 근데 원래 인스턴스 메소드 쓰고 싶은데요ㅠㅠ ➡️ downcasting

```java
if(bird instanceof Bird){
        Bird birdDowncast= (Bird) bird;
        birdDowncast.sleep();
        }
```

## abstract class 🆚 interface

![이름 없는 노트북-7](https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/f17614bf-c259-42f5-93cb-030c5a9c21c3)

### 공통점

- 둘 다 추상클래스(interface도 일종의 추상클래스) <br>
- 메소드 구현 의무 Override <br>
- 인스턴스화 될 수 없다. <br>
  <br>

### 차이점

#### **abstract class**

`extends` <br>
🔴 물려받는 것(혈통/가문)<br>
🟠 다중 적용 불가 ❌ 단일 상속만 가능 (부모는 하나 밖에 없다!)<br>
🟡 상속 관계에 의한 제한 있음<br>
🟢 생성자 가짐 ⭕️<br>
🔵 메소드 구상, 추상 모두 가능<br>
🟣 필드 모두 가능<br>
추상 클래스는 일반 멤버 변수와 메소드까지 같이 받지만, interface는 메소드만 받음 <br>
작업의 레벨 분할을 위해 사용 <br>
공통 메소드가 있는 경우 추상 클래스가 더 적합 <br>

#### **interface**

`implements` <br>
🔴 장착하는 기능<br>
🟠 다중 상속 가능 ⭕️(상속 여러개 할 수 있다는 뜻) <br>
🟡 상속 관계에 의한 제한 없음<br>
🟢 생성자 없음 ❌<br>
🔵 모든 메소드가 추상 메소드 또는 default붙인 구상 메소드, 클래스 메소드<br>
🟣 추상메소드와 상수만 사용(`final`이 붙은 애들) <br>
하지만 명시할 필요는 없음 어짜피 상수로 정의되니까 <br>

## ✅ Interface default method

### ☑️ default: abstract 벗어나기

interface도 기본적으로 abstract이기 때문에, <br>
default를 사용해서 abstract의 기본적인 제약을 벗어날 수 있음. <br>

❓ 왜 굳이 default해서 abstract 벗어나야 하는거야? <br>
만약 사용되던 interface를 implements하는 newClass가 추가되었는데, <br>
이 newClass는 새로운 기능을 추가해야 함. <br>
그러면 기존 class들은 이 새로운 기능을 또 다~~ Override해서 정의해주어야 함?? 너무 번거로움... <br>
(추상 메소드는 override안하면 실행 안 되니까) <br>
그래서 default해서 abstract 벗어나면, newClass에서 새로운 기능 구현 가능! <br>

```java
//식약청 interface
public interface FoodSafety {
//🔴 static
// announcement ()는 static ➡️ FoodSafety 의 메소드
//인스턴스 선언하지 않아도 FoodSafety 하고 바로 실행 가능
    static void announcement () {
        System.out.println("식품안전 관련 공지");
    }

//🟡 default 는 구상 메소드
// 인스턴스에서 따로 정의하지 않았더라도
//인스턴스에서 바로 사용 가능
    default void regularInspection () {
        System.out.println("정기 체크");
    }
//🟢 추상 메소드
//인스턴스에서 반드시 정의해주고(Override) 사용해야 함.
    void cleanKitchen ();
    void employeeEducation ();
}

//인스턴스 클래스
public class YalcoChicken implements FoodSafety {
    //🟢 추상 메소드 정의해주기(Override)
    @Override
    public void cleanKitchen() {
        System.out.println("매일 주방 청소");
    }

    @Override
    public void employeeEducation() {
        System.out.println("직원 위생 교육");
    }
}

//실행클래스
//🔴 인스턴스 선언하지 않아도 FoodSafety 하고 바로 실행 가능
FoodSafety.announcement();

YalcoChicken store1 = new YalcoChicken();
//🟡 default
//인스턴스에서 따로 정의 안했는데도 사용 가능
store1.regularInspection();
//🟢 추상 메소드
//인스턴스에서 정의 했음.
store1.cleanKitchen();
store1.employeeEducation();

```

```java
public interface Flyable {
    //field
    long atomsphereLimit= 476; //💡field 꼭 초기값 정해주어야 한다.

    //method에 default, static붙여 abstract 벗어남
    //더 이상 abstract가 아니므로 메소드 정의해 주어야 한다.
     default void fly(){
         System.out.println("Now flying");
     }
     static void landing(){
         System.out.println("Now landing");
     }
}
//drone 클라스, implement하는 클라스
public class Drone implements Flyable{ //여러개 interface implement 가능

    public void takePic(){
        Flyable.landing();
        System.out.println("This drone is taking a picture");
    }
}

//실행글래스
public class InterfaceTest2 {
    public static void main(String[] args) {
        //⭐️ 다형성
        //instance type으로 instance 선언 가능
        //🟢 default이기 때문에 인스턴스에서 정의 안했지만 사용 가능
        Flyable drone = new Drone();
        drone.fly();

        //downcast
        if(drone instanceof Drone){
            Drone droneDowncast= (Drone) drone;
            droneDowncast.takePic();
        }
    }
}
```

## ✅ Interface: 역할 여러개

한 객체가 여러 역할을 수행 <br>
그래서 기존 JAVA의 class, abstract class 모두 상속은 1개씩만 가능했지만, <br>
implement는 여러 개 가능! <br>
왜냐하면 한 class가 여러 역할을 수행하니까. <br>

```java
public class Family {
    public static void main(String[] args) {
        //male role: employee, dad, husband 🤵🏻‍♂️👨‍👧👨🏻‍⚖️

        //husband method
        Husband maleHusband= new Male("Galan"); //🤵🏻‍♂️
        Wife femaleWife= new Female("Park");
        maleHusband.takeCareWife(femaleWife);
        maleHusband.sayLove();

        //dad method
        //husband이 downcast
        Dad maleDad= (Dad) maleHusband ; //🤵🏻‍♂️ -> 👨‍👧
        Baby baby= new Baby("Haru");
        maleDad.educateBaby(baby);
        maleDad.sayLove();

        //employee method
        //dad이 downcast
        Employee maleEmployee= (Employee) maleDad; //👨‍👧 -> 👨🏻‍⚖️
        Employee coworker= new Male("boss");
        maleEmployee.workTogether(coworker);

    }
}
```

### 두 interface 간 **default** 메소드가 중복된다면? ➡️ 무조건 Override

Override해서 메소드 재정의해야 한다.
`interface.super.method`로 override

```java
//현재 husband, dad interface에서 같은 이름으로 default메소드가 정의된 상황
public interface Husband {
    default void sayLove(){
        System.out.println("I love my wife");
    }
}

public interface Dad {
        default void sayLove(){
        System.out.println("I love my baby");
    }
}

//impelemt하는 class
//super을 사용해 override한 method 재정의
public class Male implements Husband, Employee, Dad{
    @Override
    public void sayLove() {
        Husband.super.sayLove();
        Dad.super.sayLove();
    }
}
```

혹은 이름이 겹치는 두 method를 다른 interface로 빼내서 만드는 것도 가능 <br>

```java
public interface HusbandAndDad extends Dad, Husband {

    @Override
    default void sayLove() {
        Dad.super.sayLove();
        Husband.super.sayLove();
    }
}
//HusbandAndDad는 Dad, Husband에서 sayLove()함수 받아옴.
//이렇게만 해도 함수 실행됨.
```

### interface 도 상속이 가능하다. 심지어 **여러개** 가능

만약 비슷한 사람이 하나 더 있다면? 두 사람이 비슷한 성질을 공유함 <br>
비슷한 성질들은 그냥 선언만 해두고 불러 쓰고 싶음. ➡️ 추상 클래스를 선언한다. <br>

```java
//Dad, Husband를 합쳐서 FamilyMan이라는 class를 만들어 공통되는 속성을 넣음
public abstract class FamilyMan implements HusbandAndDad{

    @Override
    public void educateBaby(Baby baby) {
        String name= baby.getName();
        System.out.printf("Educate baby %s.\n", name);
    }

    @Override
    public void takeCareWife(Wife wife) {
        String wifeName= wife.getName();
        System.out.printf("Take care of wife %s.\n", wifeName);
    }

}

//이제는 새로운 남자가 나타나도 FamilyMan상속만 받으면 됨
public class MaleNew extends FamilyMan implements HusbandAndDad, Employee{
    @Override
    public void workTogether(Employee employee) {
        String employeeName= employee.getName();
        System.out.printf("Working with %s.\n", employeeName);
    }

    @Override
    public String getName() {
        return this.name;
    }
}

```
