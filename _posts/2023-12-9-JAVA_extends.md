---
title: Extends
categories: [JAVA, JAVA_Basics]
tags: [extends] # TAG names should always be lowercase
---

## ✅ 상속

- 기존의 클래스에서 더 수정된 클래스 만들고 싶을 때 사용 <br>
- 같은 클래스 내에서 한 클래스를 extend하는 클래스 만들기 <br>
- 자식 클래스가 실행되면 부모 클래스도 무조건 실행된다. <br>
  `public class coffeeDT extends coffee` <br>
  coffeeDT는 coffee를 상속받는다 <br>
  coffeeDT는 coffee의 필드, 메소드를 모두 그대로 따름. <br>
  부모 클래스에 constructor이 있다면, 자식 클래스도 있어야 한다. <br>

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

## 💡 메소드 오버라이딩

부모로부터 메소드를 상속 받았지만, 같은 이름 메소드를 **자식인 저는 제 방식대로 하겠습니다.** <br>
메소드 오버라이딩은 부모와 자식간에 메소드가 다른 것 <br>
🆚 오버로딩은 같은 클래스 내에서 parameter을 다르게 해 같은 이름 메소드 사용하는 것 <br>

- 부모와 매개변수가 같아야 한다. (그러나 부모 메소드로부터 parameter은 달라질 수 없음.)
- 반환 타입이 같아야 한다.
- access modifier는 부모 클래스보다 좁을 수 없다.
- 부모보다 더 많은 예외를 선언할 수 없다.
- static은 오버라이딩 할 수 없음

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

#### ⌨️ `Button.java` override 예시 코드

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

## 👥 shadowing

💥 field는 오버라이딩 같은게 없다. <br>
만약 부모와 자식 같은 이름으로 field있으면? 반영이 되지 않는다. <br>
예를 들어, 부모와 자식 물고기 모두 `protected String color;`이라는 field가 있다고 해보자.<br>
내가 자식 물고기의 색을 바꿔주고 싶어서 아무리 설정을 해 봐도, `this.color= color;`<br>
부모 물고기 클래스의 필드가 자식 물고기 필드를 가려 버리기 때문에 자식 물고기 색 설정 변경이 적용되지 않는다.<br>
**따라서, 부모와 자식 같은 이름으로 field가 있는데, 🐥자식🐥의 field를 바꿀 수 없다. ❌** <br>
이를 **shadowing**이라고 한다.<br>
(부모 클라스가 자식 클라스 필드를 덮어버리는 것)<br>

### 💡 부모와 자식 같은 이름으로 field가 있는데, 🐓부모🐓의 field를 바꾸고 싶다면? ➡️ super

자식(나)의 field는 바꿀 수 없지만, 부모의 field는 바꿀 수 있음.

```java
    public BabyFish(String color, String sea){
        this.sea= sea;
        super.color= color; //나의 color을 바꾸지 말고, 부모의 color을 바꿔
    }
```

## 💡 super

`this`은 자기 자신 받아왔다면, `super`은 부모 클래스 변수 받아오기 <br>
super은 부모 클래스 것 받아오는 것<br>

```java
class Parent{
    int x=10;
}
class child extends Parent{
    int x=20;
    void method(){
        System.out.println(this.x); //20 mine
        System.out.println(super.x); //10 parent
    }
}
```

```java
class Point{
    String getLocation(){
        return x, y
    }
}

class 3DPoint extends Point{
    String getLocation(){
        return super.getLocation() + z;
    }
}
```

## 💡 super()

this()와 마찬가지로 super() 역시 생성자이다.<br>
this()는 같은 클래스의 다른 생성자 호출<br>
super()는 조상 클래스의 생성자 호출<br>
<br>
super이 위로 올라와야 한다.<br>

```java
class Point{
    int x, y;
    Point(int x, int y){
        this.x = x;
        this.y = y;
    }
}
class 3DPoint extends Point{
    Point#D(int x, int y, int z){
        super(); //super이 있어야지 부모를 생성하고 자식을 생성
        this.x = x;
        this.y = y;
        this.z= z;
    }
}
```

```java
//Fish 클래스가 field로 name, food, poison가지고 있음.
//Babyfish 클래스가 field로 sea 가지고 있음.
public class BabyFish extends Fish {
        String sea = "East";

public BabyFish(String name, int food, boolean poison, String sea) {
        super(name, food, false); //부모 객체에서 private인 field들, super써서 가져온다.
        super("Nemo", "shrimp", true)//이런 식으로 field값 정해서 가져오는 것
        this.sea = sea; //이건 babyFish의 field
    }
}
```

## 📌 Template Method Pattern

- 상속을 이용한 대표적인 디자인 패턴

💡 Design Pattern <https://soheeparklee.github.io/posts/JAVA_designPattern/>
