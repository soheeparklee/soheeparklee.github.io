---
title: Class/ Instance/ Object/ this, constructor, getter, setter
categories: [JAVA, JAVA_Basics]
tags: [this, object, instance, getter, setter, constructor] # TAG names should always be lowercase
---

## ✅ class & instance & object

### ☑️ class

클래스는 인스턴스가 가질 필드, 메소드를 가지고 있음 <br>
인스턴스를 정의한 틀 <br>
인스턴스를 생성하는데 사용 <br>
<br>

- class= 올리브영 본사<br>
  - 필드 + 기능을 지정<br>
  - 매장들이 어떤 기능을 가지고 있을지, 어떤 일을 시킬지 정함<br>

### ☑️ instance

클래스에 의해 정의됨.<br>
<br>

- instance= 올리브영 강남점<br>

### ☑️ object

클래스를 통해 생성된 객체를 클래스의 인스턴스라고 부름 <br>
객체는 멤버(field와 method)를 가진다. <br>
객체를 생성하면 객체의 멤버(field와 method)가 JVM안에 있는 **HEAP**이라는 공간 위에 올라간다. <br>
HEAP에는 반드시 new라는 키워드를 통해 생성된 객체만 올라간다. <br>

### ✔️ instance 🆚 object

엄밀히 말하면 객체는 모든 인스턴스 포함 <br>
인스턴스는 해당 객체가 어떤 클래스로부터 생성된 것인지를 강조 <br>

## ✅ Object oriented Programming

객체끼리 상호작용하듯이 코드를 작성하는 방식 <br>

#### 객체지향 프로그래밍을 떠받히는 네 가지 기둥

- 추상화
- 캡슐화
- 상속
- 다형성

## ✅ field, method

### ✔️ class선언을 하고, instance에 field, method 추가하기

#### 📍field:

method와 constructor에서 사용 가능<br>

#### 📍method:

객체의 행위/ 기능<br>
객체 간의 데이터 전달 수단<br>

#### ⌨️ 본사 코드 `OliveYoung.java` ⌨️ 지점 내는 코드 `Main.java`

- class에서 field, method받아와 정의해주기<br>
- 또 다른 변수에 class에서 field넣어주기도 가능<br>

```java
public class OliveYoung {
    //클래스는 인스턴스가 가질 필드, 메소드를 가지고 있음
    //  인스턴스가 가질 필드(field)들
    int no;
    String name;

    //  인스턴스가 가질 메소드 - 💡 static을 붙이지 않음
    String intro() {
        // no와 name 앞에 this를 붙인 것과 같음
        return "안녕하세요, %d호 %s점입니다."
                .formatted(no, name);

    }
}

public static void main(String[] args) {
        //  본사 소속의 매장을 내는 코드
        //  클래스의 인스턴스를 만드는 코드
        OliveYoung store1 = new OliveYoung();
        // 클래스에서 정의한 필드를 가져와 값 넣어주기
        store1.no = 1; // 🔴
        store1.name = "강남";

        OliveYoung store2 = new OliveYoung();
        store2.no = 2;
        store2.name = "양천";
        //이 방법은 매장을 먼저 낸 이후, 매장에 번호와 이름을 부여한 것이다.


        //  인스턴스의 필드들에 접근하여 값 빼오기
        // 빼온 값을 또 다른 변수 store1No에 저장
        int store1No = store1.no;
        String store2Name = store2.name;

        //  인스턴스의 메소드 호출
        String store1Intro = store1.intro();
    }
```

## ✅ constructor

### 📍 **constructor 생성자:** 인스턴스 초기화 메소드

인스턴스 생성시 실행될 작업을 하기 위해서

- 이름: 해당 클래스랑 똑같 🟰 <br>
- return값 없음❌(해당 클래스 타입의 인스턴스 반환) <br>
- parameter이 있다면 parameter으로 멤버 변수의 값을 초기화한다. <br>
- new 연산자와 함께 사용되어 인스턴스를 반환 <br>
  ⭐️ 이 때 new가 인스턴스를 생성하는 것이지, 생성자가 인스턴스를 생성하는 것은 아니다. <br>
- `OliveYoung store1 = new OliveYoung(1, "강남");`I() <br>
- 내가 자동으로 생성하기 위해서는 `command` + `N` <br>
- 코드에 작성하지 않아도 컴파일러가 자동으로 생성(내가 작성하지 않았다고 생성자가 없는게 아님.) <br>
  <br>

### 📍 **this :** 생성될 인스턴스를 가리킴

생성자에서 다른 생성자 호출하기 <br>
this는 참조변수로, 인스턴스 자신을 가리킨다. <br>

- 생성자의 이름으로 클래스 이름 대신 this를 사용한다.
- 한 생성자에서 다른 생성자를 호출할 떄는 반드시 첫 번째 줄에서만 호출이 가능하다.
- `no`, `name`에 `this`붙인 것과 같음

```java
class Car{
    String color;
    String gearType;
    int door;

    Car(){
        this("white", "auto", 4);
    }

    Car(String color){
        this(color, "auto", 4);
    }

    Car(String color, String gearType, int door){
        this.color= color;
        this.gearType= gearType;
        this.door= door;
    }

}
```

#### ✔️ 매개변수 받는 constructor

`OliveYoung.java` ⌨️ 바로바로 instance 생성해서 no, name 넣기 <br>
<br>
instance가 가질 field, method를 class 코드에서 바로 정의<br>
생성자도 하나의 method이다.<br>
그리고 선언한 instance에다가 method도 불러오기 가능 <br>

```java
public class OliveYoung {
        //field
        int no;
        String name;

        //field, method사이에 constructor을 정의
        //  ⭐ 생성자(constructor) : 인스턴스를 만드는 메소드
        //return 이 따로 없음
        //  ⭐ this : 생성될 인스턴스를 가리킴
         OliveYoung (int no, String name) {
            this.no = no;
            this.name = name;
        }
        //method
        String intro () {
            //  String name = "몽고반"; // 주석해제 시 name 대체
            return "안녕하세요, %d호 %s점입니다." // 🔴
                    .formatted(no, name);
        }
}

public static void main(String[] args) {
        //  클래스로 인스턴스를 생성 - 💡 new 연산자 + 생성자 호출
        //  본사의 방침대로 매장을 내는 것
        OliveYoung store1 = new OliveYoung(1, "강남");
        OliveYoung store2 = new OliveYoung(2, "양천");
        OliveYoung store3 = new OliveYoung(24, "제주");

        String[] intros = {store1.intro(), store2.intro(), store3.intro()};
    }
```

#### ✔️ constructor가 배열을 받을 수도 있음

```java
public class IntArrayInfo {

        int count;
        int sum; // 기본 0
        double average;
//배열 받는 constructor
        IntArrayInfo(int[] nums) {
            count = nums.length;
            for(int num:nums){
                sum +=num;
            }
            average = 1.0 * sum / nums.length;
            }
            // 소수부를 잃지 않도록 먼저 1.0을 곱하여 double로 만듦
}
//배열을 입력하고, 배열을 instance로 선언하고 instance의 field 받아오기
public static void main(String[] args) {
        //배열 받기
        int[] ary1= {1,2,3,4,5};

        //배열을 instance로 선언
      IntArrayInfo ary1Instance= new IntArrayInfo(ary1);

      //isntance의 field받아오기
      double ary1Avg= ary1Instance.average;
      System.out.print(ary1Avg);

    }
```

### 📍 생성자 이용해서 인스턴스 복사하기

현재 사용하고 있는 인스턴스와 같은 상태를 가지는 인스턴스 만들기 <br>
복사하면 서로 독립적으로 메모리 공간에 존재하는 별도의 인스턴스이므로 c1이 변경되어도 c2는 영향을 받지 않는다. <br>

```java
class CarTest{
    public static void main(String[] args){
        Car c1= new Car();
        Car c2= new Car(c1); //c1복사,
    }
}
```

## ✅ Getter and Setter

- 사용자가 field에 접근해서 get하고 set할 수 있도록 하는 기능<br>
- field이름 앞에 get, set써서 만들어준다.<br>
- 그러면 외부에서 그 field의 값을 받고 싶으면 getter, 바꾸고 싶으면 setter을 사용<br>
- 또 getter, setter 안에 코드를 짜서 field의 값을 변경해 get하거나 set하도록 만들수도 있다.<br>
- constructor 과 비슷하게 `command` + `N`눌러서 만들기 가능<br>

### constructor 🆚 setter

field안에 값을 주입하는 두 가지 방법이다. <br>
✔️ **constructor:** 필드 초기화, public<br>
맨 처음에 인스턴스 생성할 때 이런저런 값을 넣을 수 있음. <br>
✔️ **setter:** private, <br>
인스턴스 생성할 떄는 constructor쓰고, 나중에 값을 바꾸기<br>
보통 클래스의 멤버변수를 private access modifier로 설정한 후 getter/setter통해서 멤버변수의 값을 변경한다.<br>

### access modifier 🆚 getter&setter<br>

**access modifier**은 class끼리 또는 패키지 사이에서 어디까지 사용 가능한지 범위를 설정해주고<br>
**getter&setter**은 실행하는 main 실행 클래스에서 class내의 값을 불러올 때 사용한다. <br>

#### ⌨️ discount받는 코드

field 의 속성들이 access modifier로 정의되어 있음 <br>

```java
public class Product {

    private static double discount = 0.2;

    private String name;
    private int price;
}
```

#### ⌨️ getter, setter 만듦

```java
public String getName() {
        return name;
    }
```

#### ⌨️ getter, setter안에 코드를 변경해 원래 field와는 다른 값 get, set하게 만들 수도 있음.

```java
//get변경
    public int getPrice() {
        return (int) (price * (1 - discount));
    }
    //get해서 외부에 값 줄 때 할인율 적용한 가격을 get

//set변경
    public void setName(String name) {
        if (name.isBlank()) return;
        this.name = name;
    }
    //set할 때 이름 비어있으면 return해
```

## ✅ this

인스턴스의 멤버 값 ⭕️ <br>
클래스 자체 멤버 값 ❌ <br>
기본값을 주는 방식으로 사용할 수 있다. <br>

### 1️⃣ 생성자를 호출하기 위한 this() 2️⃣ 인스턴스의 field 또는 method 받아오기 위한 this.field/method

같은 이름으로 생성자 만드는데, 만들 때 넣고 싶은 필드, 속성을 다르게 한다. <br>
이 때 다른 생성자를 `this`로 부를 수 있다. <br>

```java
    //이런 필드를 가지고 있음
    private String name;
    private String gender;
    private int age;

    //1️⃣ 생성자를 호출하기 위한 this()
    //이 생성자는 필드 하나 받음. 이렇게 하면 이름만 가지고 인스턴스 만듦.
    //그러면 아래에 있는 생성자 호출함. (자기보다 필드 많은 생성자)
    public Person(String name){
        this(name, gender: "unknown");
    }
    //이 생성자는 필드 2개만 받음. 이름, 성만 가지고 인스턴스 만들어.
    // 그러면 또 자기보다 필드 많은 생성자 (아래에) 호출함.
    public Person(String name, String gender){
        this(name, gender, age:-1);
    }
    //얘가 필드 제일 많이 받고 (3개)
    //2️⃣ 인스턴스의 field 또는 method 받아오기 위한 this.field/method
    public Person(String name, String gender, int age) {
        this.name = name;
        this.gender = gender;
        this.age = age;
    }
```

### 3️⃣ 인스턴스 주소 확인

인스턴스 자신의 생성 주소를 알려준다. <br>
(인스턴스가 만들어지면 JVM의 heap 메모리에 올라가고 주소를 가지게 됨, 인스턴스를 부르면 이 주소를 알 수 있다. ) <br>

```java
public class Person {
    private String name;
    private String gender;
    private int age;

    public void introduce(){
        System.out.printf("저는 %s이고, %s이고, %d살 입니다.\n", this.name, this.gender, this.age);
    }

    public Person(String name, String gender, int age) {
        //인스턴스의 field 또는 method 받아오기 위한 this
        this.name = name;
        this.gender = gender;
        this.age = age;
    }
    //3️⃣ 인스턴스 주소 확인
    public Person returnInstanceAddress(){
        return this;
    }
}
//실행 class
public class Introduction {

    public static void main(String[] args){
        //make instance
        Person cesar= new Person("Cesar", "Male", 33);
        Person sohee= new Person("So Hee", "Female", 27);

        //person class의 method
        cesar.introduce();
        sohee.introduce();

        //instance의 address
        Person cesarAddress= cesar.returnInstanceAddress();
        System.out.println(cesarAddress);
    }
}
//result
// 저는 Cesar이고, Male이고, 33살 입니다.
// 저는 So Hee이고, Female이고, 27살 입니다.
// test3.Person@234bef66
```

## ✅ 인스턴스에서 class 가져오기

여태까지는 클래스를 만들고, 클래스의 필드, 메소드, 생성자 바탕으로 인스턴스를 만들었다면 <br>
반대로 인스턴스에서 **클래스의 필드, 메소드, 생성자**가져오기 <br>

### reflection 기술

클래스의 메타 정보 빼내서 사용하는 기술 <br>
어떤 클래스의 필드, 메소드, 생성자 뽑아내서 사용하기<br>
spring AOP의 근간이 되는 기술<br>

```java
public class GetClass {
    Class clazz= customer.getClass();
    //GET constructor
    Constructor[] constructors= clazz.getConstructors();
    for( Constructor constructor: constructors ){
        System.out.println(constructor);
    }
    //GET method
    Method[] methods= clazz.getMethods();
    for(Method method: methods){
        System.out.println(method);
    }
    //GET field
    //public field만 출력된다.
    //public 아닌 field도 보고싶으면 getDeclaredFields()
    Field[] fields= clazz.getFields();
    for(Field field: fields){
        System.out.println(field);
    }
    //가져온 constructor을 사용해서 새로운 instance생성
    //그러니까 new Customer하는 것이랑 같으나,
    //이 때 customer은 가장 상위 클래스인 object class 로 생성된다.
    //downcasting필요
    //constructor 여러개라면 어떤 constructor 가져올지 getConstructor(여기에 쓰기)
    Customer customer= (Customer) clazz.getConstructor(String.class).newInstance("Kim");

}

```
