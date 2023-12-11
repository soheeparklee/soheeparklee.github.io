---
title: Class/ Instance/ Object/ static/ access modifier
categories: [JAVA, JAVA_Basics]
tags: [] # TAG names should always be lowercase
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

객체끼리 상호작용하듯이 코드를 작성하는 방식

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

#### ⌨️ 본사 코드 `OliveYoung.java`

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
```

##### ⌨️ 지점 내는 코드 `Main.java`

- class에서 field, method받아와 정의해주기<br>
- 또 다른 변수에 class에서 field넣어주기도 가능<br>

```java
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

### ✔️ 본사에서 지점을 내는 동시에 지점의 field, method를 정의할 수도 있음.

#### 📍 **constructor 생성자:** 인스턴스를 만드는 메소드

- 이름: 해당 클래스랑 똑같 🟰
- return값 없음❌(해당 클래스 타입의 인스턴스 반환)
- parameter이 있다면 parameter으로 멤버 변수의 값을 초기화한다.
- new 연산자와 함께 사용되어 인스턴스를 반환
- `OliveYoung store1 = new OliveYoung(1, "강남");`I()
- 내가 자동으로 생성하기 위해서는 `command` + `N`
- 코드에 작성하지 않아도 컴파일러가 자동으로 생성(내가 작성하지 않았다고 생성자가 없는게 아님.)

#### 📍 **this :** 생성될 인스턴스를 가리킴

- `no`, `name`에 `this`붙인 것과 같음

#### ⌨️ constructor 생성자 본사 코드 `OliveYoung.java`

instance가 가질 field, method를 class 코드에서 바로 정의
생성자도 하나의 method이다.

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

```

#### ⌨️ 바로바로 instance 생성해서 no, name 넣기

그리고 선언한 instance에다가 method도 불러오기 가능

```java
public static void main(String[] args) {
        //  클래스로 인스턴스를 생성 - 💡 new 연산자 + 생성자 호출
        //  본사의 방침대로 매장을 내는 것
        OliveYoung store1 = new OliveYoung(1, "강남");
        OliveYoung store2 = new OliveYoung(2, "양천");
        OliveYoung store3 = new OliveYoung(24, "제주");

        String[] intros = {store1.intro(), store2.intro(), store3.intro()};
    }
```

## ☑️ instance를 parameter로 받는 method

#### ⭐️ **instance**는 **reference type**

- 그래서 값이 변경될 경우 instance 원본의 값이 변경됨 주의!
- 같은 클래스의 인스턴스라도 필드의 값은 별개임!

#### ⌨️ taegwondo class 정의 `Taegwondo.java`

```java
public class Taegwondo {
    //constructor없음. 왜냐하면 이미 instance의 기본값이 정해져 있으니까.
    double hp = 50;
    int attack = 8;
    double defense = 0.2;
    //공격하는 메소드
    void attack (Taegwondo enemy) { // 💡 다른 슬라임의 인스턴스를 인자로 받음
        enemy.hp -= attack * (1 - enemy.defense);
    }
}
```

#### ⌨️ 선수1이 선수2를 공격

```java
		Taegwondo player1 = new Taegwondo();
        Taegwondo player2 = new Taegwondo();

        player1.attack(player2);
//result:
//player1 hp:50 attack: 8 defense:0.2
//player2 hp:50-8*0.8= 43.6 attack: 8 defense:0.2
//instance is reference type
```

## ☑️ array를 parameter로 받는 method

#### ⌨️ 배열 받는 constructor

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
```

#### ⌨️ 배열을 입력하고, 배열을 instance로 선언하고 instance의 field 받아오기

```java
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

## ✅ static

static(정적)은 마치 본사의 정보와 기능을 정의해 두는 것과 같다.
모든 인스턴스마다 동일하게 가지고 있을 것들에 대해서 사용

#### ⌨️ `static String brand = "올리브영";`

`Oliveyoung.java`

```java
public class Oliveyoung {
    //static 본사의 정보, 기능 정의
    //  인스턴스마다 따로 갖고 있을 필요가 없는 것들에 사용
    static String brand = "올리브영";
    static String contact () {
        return "%s입니다. 무엇을 도와드릴까요?".formatted(brand);
    }

    //여기서부터는 instance 내용임
    //instance의 field정의
    // int no;
    // String name;

    // //instance constructor
    // Oliveyoung(int no, String name) {
    //     this.no = no;
    //     this.name = name;
    // }
    // //instance method
    // String intro () {
    //     //  💡 인스턴스 메소드에서는 정적 프로퍼티 사용 가능
    //     return "안녕하세요, %s %d호 %s점입니다."
    //             .formatted(brand, no, name);
    // }
}
```

#### ⌨️ 따로 `new`와 `constructor`로 인스턴스를 생성하지 않아도 바로바로 불러와서 사용 가능하다.

`Main.java`

```java
public static void main(String[] args) {
        //  💡 클래스 필드와 메소드는 인스턴스를 생성하지 않고 사용
        String Brand = Oliveyoung.brand;
        String Contact = Oliveyoung.contact();

    }
```

- static은 instance의 field, method를 사용할 수 없다. ❌

## ✅ access modifier 접근 제어자, 정보 은닉화

필드 앞에 붙여 이 데이터에 대한 접근성을 제한한다.
이로써 정보를 감추기도 한다. ➡️ 정보 은닉화
메소드 앞에는 붙이지 않는다.

### ⭐️ 캡슐화 encapsulation

- 사용자가 굳이? 볼 필요 없는 부분들을 감싸서 더 편리하게 사용할 수 있게 하기 위함

#### ✔️ `public`

**다른 패키지에서도 접근 가능**
동일 패키지 또는 자손 클래스 안에서 접근 가능
동일 패키지 안에서 접근 가능
해당 클래스 안에서 접근 가능

#### ✔️ `protected`

**동일 패키지 또는 자손 클래스 안에서 접근 가능**
동일 패키지 안에서 접근 가능
해당 클래스 안에서 접근 가능

#### ✔️ `default`

**동일 패키지 안에서 접근 가능**
해당 클래스 안에서 접근 가능

#### ✔️ `private`

해당 클래스 안에서 접근 가능

## ✅ Getter and Setter

- 사용자가 field에 접근해서 get하고 set할 수 있도록 하는 기능
- field이름 앞에 get, set써서 만들어준다.
- 그러면 외부에서 그 field의 값을 받고 싶으면 getter, 바꾸고 싶으면 setter을 사용
- 또 getter, setter 안에 코드를 짜서 field의 값을 변경해 get하거나 set하도록 만들수도 있다.
- constructor 과 비슷하게 `command` + `N`눌러서 만들기 가능

### constructor 🆚 setter

field안에 값을 주입하는 두 가지 방법이다.
✔️ **constructor:** 필드 초기화, public
✔️ **setter:** private, 보통 클래스의 멤버변수를 private access modifier로 설정한 후 getter/setter통해서 멤버변수의 값을 변경한다.

#### ⌨️ discount받는 코드

field 의 속성들이 access modifier로 정의되어 있음

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

인스턴스의 멤버 값 ⭕️
클래스 자체 멤버 값 ❌
기본값을 주는 방식으로 사용할 수 있다.

### 1️⃣ 생성자를 호출하기 위한 this() 2️⃣ 인스턴스의 field 또는 method 받아오기 위한 this.field/method

같은 이름으로 생성자 만드는데, 만들 때 넣고 싶은 필드, 속성을 다르게 한다.  
이 때 다른 생성자를 `this`로 부를 수 있다.

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

인스턴스 자신의 생성 주소를 알려준다.
(인스턴스가 만들어지면 JVM의 heap 메모리에 올라가고 주소를 가지게 됨, 인스턴스를 부르면 이 주소를 알 수 있다. )

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

## ✅ 상속

- 기존의 클래스에서 더 수정된 클래스 만들고 싶을 때 사용
- 같은 클래스 내에서 한 클래스를 extend하는 클래스 만들기
  `public class coffeeDT extends coffee`
  coffeeDT는 coffee를 상속받는다
  coffeeDT는 coffee의 필드, 메소드를 모두 그대로 따름.
  부모 클래스에 constructor이 있다면, 자식 클래스도 있어야 한다.

### 💡 메소드 오버라이딩

부모로부터 메소드를 상속 받았지만, 같은 이름 메소드를 **자식인 저는 제 방식대로 하겠습니다.**
메소드 오버라이딩은 부모와 자식간에 메소드가 다른 것
🆚 오버로딩은 같은 클래스 내에서 parameter을 다르게 해 같은 이름 메소드 사용하는 것

#### ⌨️ 부모 클래스 `Button.java`

```java
public class Button {
    private String print;
    //constructor
    public Button(String print) {
        this.print = print;
    }
    //method
    public void func () {
        System.out.println(print + " 입력 적용");
    }
}
```

#### ⌨️ 자식 클래스 `ShutDownButton.java`

super은 부모 클래스 것 받아오는 것
super이 위로 올라와야 한다.

```java
//ShutDownButton은 Button을 상속합니다.
public class ShutDownButton extends Button {
    public ShutDownButton () {
        super("ShutDown"); // 💡 부모의 생성자 호출,
    }

	//  💡 부모의 메소드를 override
    //부모는 (print+ 입력 적용)이라고 정의했지만, 자식은 다르게 정의함.
    @Override
    //annotation: 상속할 때 부모의 method를 오타내지 않도록 감시
    public void func () {
        super.func(); // 💡 부모에서 정의한 메소드 호출
        this.on = !this.on;
        System.out.println(
                "shutdownBTN: " + (this.on ? "ON" : "OFF")
        );
    }
}
```
