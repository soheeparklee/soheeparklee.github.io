---
title: Class/ Instance/ Object/ Static/ Access modifier/ This/ 상속
categories: [JAVA, JAVA_Basics]
tags: [
    this,
    object,
    static,
    accessmodifier,
    instance,
    getter,
    setter,
    constructor
  ] # TAG names should always be lowercase
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

static(정적)은 마치 본사의 정보와 기능을 정의해 두는 것과 같다. <br>
모든 인스턴스마다 동일하게 가지고 있을 것들에 대해서 사용 <br>
인스턴스들이 값을 바꿀 수 있음. <br>

### ☑️ static 변수의 의미

🟰 정적 변수<br>
🟰 클래스 변수(클래스에 속해 있음. 인스턴스 아니고❌)<br>
🟰 프로그램 실행 시, 정적 생성<br>
🟰 프로그램 실행 시, 이미 생성되어 있음<br>
🟰 인스턴스 생성 전 정의되어 있음.<br>
🟰 그래서 모든 인스턴스들이 접근 가능하다.<br>
따로 `new`와 `constructor`로 인스턴스를 생성하지 않아도 바로바로 불러와서 사용 가능하다 <br>
<br>

### ☑️ instance 변수 🆚 static 변수

인스턴스의 멤버 변수 앞에는 `this`붙일 수 있지만, ⭕️ <br>
static 변수 앞에서는 붙이지 않는다. ❌ <br>
instance는 static의 field, method를 사용할 수 있지만 ⭕️ <br>
static은 instance의 field, method를 사용할 수 없다. ❌ <br>

### ☑️ JAVA static 변수/메소드

만약 static앞에 private를 붙이고 싶다면? ➡️ 불러오기 위해서 getter, setter 만들어야 함. <br>
그런데, **setter**만들 때 static 변수 앞에는 `this`를 붙일수 없다! <br>
대신, class의 이름을 붙여야 한다.

```java
    //static
    private static int serialNum =1;

    //getter
    public static int getSerialNum(){
        return serialNum;
    }
    //원래 setter만들 때 앞에 this붙였지만
    //static 앞에는 this를 붙이지 않는다.
    //instance가 아니니까!
    //대신 class를 붙여야 한다.
    public static void setSerialNum(int serialNum) {
        Student.serialNum = serialNum;
    }
```

### ☑️ static을 본사와 지점에 비유하자면?

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

    static int lastestNum = 0;

    int no;
    //int no = ++lastestNum; // 이렇게 해도 됨

    String name;

    Oliveyoung(String name) {
        // 클래스 변수를 활용하여 생성마다 새 번호 부여 (또는 위처럼)
        no = ++lastNo;
        this.name = name;
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
- 자식 클래스가 실행되면 부모 클래스도 무조건 실행된다.
  `public class coffeeDT extends coffee` <br>
  coffeeDT는 coffee를 상속받는다 <br>
  coffeeDT는 coffee의 필드, 메소드를 모두 그대로 따름. <br>
  부모 클래스에 constructor이 있다면, 자식 클래스도 있어야 한다. <br>

### 💡 메소드 오버라이딩

부모로부터 메소드를 상속 받았지만, 같은 이름 메소드를 **자식인 저는 제 방식대로 하겠습니다.** <br>
메소드 오버라이딩은 부모와 자식간에 메소드가 다른 것 <br>
그러나 부모 메소드로부터 parameter은 달라질 수 없음. <br>
🆚 오버로딩은 같은 클래스 내에서 parameter을 다르게 해 같은 이름 메소드 사용하는 것 <br>

### 👥 shadowing

💥 field는 오버라이딩 같은게 없다.
만약 부모와 자식 같은 이름으로 field있으면? 반영이 되지 않는다.
예를 들어, 부모와 자식 물고기 모두 `protected String color;`이라는 field가 있다고 해보자.
내가 자식 물고기의 색을 바꿔주고 싶어서 아무리 설정을 해 봐도, `this.color= color;`
부모 물고기 클래스의 필드가 자식 물고기 필드를 가려 버리기 때문에 자식 물고기 색 설정 변경이 적용되지 않는다.
**따라서, 부모와 자식 같은 이름으로 field가 있는데, 🐥자식🐥의 field를 바꿀 수 없다. ❌**
이를 **shadowing**이라고 한다.
(부모 클라스가 자식 클라스 필드를 덮어버리는 것)

#### 💡 부모와 자식 같은 이름으로 field가 있는데, 🐓부모🐓의 field를 바꾸고 싶다면? ➡️ super

자식(나)의 field는 바꿀 수 없지만, 부모의 field는 바꿀 수 있음.

```java
    public BabyFish(String color, String sea){
        this.sea= sea;
        super.color= color; //나의 color을 바꾸지 말고, 부모의 color을 바꿔
    }
```

### 💡 super

`this`은 자기 자신 받아왔다면, `super`은 부모 클래스 변수 받아오기
super은 부모 클래스 것 받아오는 것<br>
super이 위로 올라와야 한다.<br>

```java
//Fish 클래스가 field로 name, food, poison가지고 있음.
//Babyfish 클래스가 field로 sea 가지고 있음.
public class BabyFish extends Fish {
public BabyFish(String name, int food, boolean poison, String sea) {
        super(name, food, false); //부모 객체에서 private인 field들, super써서 가져온다.
        this.sea = sea; //이건 babyFish의 field
    }
}
```

### 💡 upcasting

자식 클래스는 부모 클래스로 묵시적 변환이 가능하다. <br>
우리가 int 타입을 float으로 변환했듯, 자식 클래스는 부모 클래스로 변환 가능 <br>
근데 그러면 자식 클래스에서 확장했던 field는 더이상 사용할 수 없다. <br>
그런데 만약 override된 method를 실행한다면 자식의 override된 method가 실행됨!!!! <br>

```java
        //타입 선언: 부모 인스턴스화: 부모 ⭕️
        Fish fish1= new Fish();
        //타입 선언: 부모  인스턴스화: 자식 ⭕️ ⭐️묵시적 형 변환
        Fish fish2= new BabyFish();
        //타입 선언: 자식 인스턴스화: 자식 ⭕️
        BabyFish Fish3= new BabyFish();
        //타입 선언: 자식 인스턴스화: 부모 ❌ 큰 타입에서 작은 타입은 ❌
        BabyFish Fish4= new Fish();
```

#### ⌨️ `Button.java`

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

//ShutDownButton은 Button을 상속합니다.
public class ShutDownButton extends Button {
    public ShutDownButton () {
        super("ShutDown"); // 💡 부모의 생성자 호출 super
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

#### 물고기 상속 예시 코드

```java
public class Fish {
    //field
    private String name;
    private int food;
    private boolean poison;

    //method

    public String fishInfo(){
        return String.format("물고기 이름: %s, 먹이 개수: %d, 독: %b%n", this.name, this.food, this.poison);
    }
    public void printFishInfo(){
        System.out.println(fishInfo());
    }

    //setter
    public void setName(String name) {
        this.name = name;
    }
    public void setFood(int food) {
        this.food = food;
    }
    public void setPoison(boolean poison) {
        this.poison = poison;
    }
}

public class BabyFish extends Fish{
    //BabyFish에만 있는 필드
    private String sea;
    //BabyFish에만 있는 메소드
    public void swimming(){
        System.out.println(fishInfo() + "Look! I am swimming.");
    }

    public String getSea() {
        return sea;
    }

    public void setSea(String sea) {
        this.sea = sea;
    }
}

public class SeaSwim {

    public static void main(String[] args){
        //instance만들고 setter로 속성
        Fish fish = new Fish();
        fish.setName("Nemo");
        fish.setFood(10);
        fish.setPoison(true);

        fish.printFishInfo();

        BabyFish baby= new BabyFish();
        baby.setName("Baby Nemo");
        baby.setFood(5);
        baby.setPoison(false);
        baby.setSea("East sea");

        //printFishInfo()는 BabyFish에게 없지만 상속했기 때문에 잘 출력되는 것을 알 수 있다.
        baby.printFishInfo();
        baby.swimming();
    }
}
//물고기 이름: Nemo, 먹이 개수: 10, 독: true
//물고기 이름: Baby Nemo, 먹이 개수: 5, 독: false
```

#### 물고기 @Override 예시 코드

```java
public class Fish {

    public String fishInfo(){
        return String.format("물고기 이름: %s, 먹이 개수: %d, 독: %b%n", this.name, this.food, this.poison);
    }
    //같은 이름 메소드
    void eat(String food, int foodNum){
        System.out.println(fishInfo() + food + "를" + foodNum + "개 먹고 있습니다.");
    }
}

public class BabyFish extends Fish{
    //override
    //같은 이름 메소드
    @Override
    void eat(String food, int foodNum){
        System.out.println(fishInfo() + food + "안 먹을래!");
    }

    @Override
    void fishInfo(String sea){
        return super.fishInfo()+ "is parent fish," + String.format("baby fish lives in %s sea.", this.sea;
    }
}

public class SeaSwim {

    public static void main(String[] args){
        //instance만들고 setter로 속성
        Fish fish = new Fish();
        fish.eat("새우", 10);


        BabyFish baby= new BabyFish();
        baby.eat("새우", 0);
    }
}
//새우를10개 먹고 있습니다.
//새우안 먹을래!
```
