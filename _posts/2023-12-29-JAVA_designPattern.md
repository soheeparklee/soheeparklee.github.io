---
title: Design Pattern
categories: [JAVA, JAVA_Basics]
tags: [design, pattern] # TAG names should always be lowercase
---

## ✅ 디자인 패턴

소프트웨어 디자인 과정(🟰 코드 구현 전 설계) 전형적인 해결책 <br>
<br>

**디자인 패턴** 🟰 제품 제작 전 구상도<br>
비즈니스 상황 별 최적의 설계 노하우/전략/공략법 정리<br>
UML(Unified Modeling Language)로 객체 간 구조도 작성<br>

#### ✔️ 생성패턴

기존 코드의 재사용성 증가<br>

- 빌더 패턴<br>
- 싱글턴 패턴<br>

#### ✔️ 구조 패턴

구조를 유지하면서 더 큰 구조로 조립<br>

- 데코레이터 패턴<br>

#### ✔️ 행동패턴

알고리즘 및 객체 책임 할당<br>

- 전략 패턴<br>

## 🧩 JAVA 싱글톤 패턴

**단 하나 인스턴스만** 생성 및 공유하여 **자원 절약** 및 **일관성 유지**를 목적으로 하는 디자인 패턴<br>
<br>

- static<br>
- synchronized<br>

### filewriter 개선

파일을 여러번 읽고 쓸 때,<br>
인스턴스를 여러번 만드는 것이 아니라<br>
싱글톤 패턴 적용하여 한 번만 스레드 생성하게 만들어서 모든 스레드가 이 filewriter사용하도록 하기<br>

#### 👎🏻 기존 코드

비슷한 작업을 하는 객체 여러번 생성해야 함 <br>

```java
//Filewriter.java
public class Filewriter {
    private String filename;

    public Filewriter(String filename) {
        this.filename = filename;
    }

    public void writeToFile(String message) {
        try {
            FileWriter fileWriter = new FileWriter(filename, true);
            fileWriter.write(message + "\n");
            fileWriter.flush();
            fileWriter.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

//FilewriterTest.java
public class FilewriterTest {
    public static void main(String[] args) {
        //👎 같은 파일에 쓰기 위해 매번 객체 생성해야 한다.
        Thread thread1 = new Thread( () -> {
            Filewriter writer = new Filewriter("src/chap60_singleton/test.txt");
            writer.writeToFile("Thread 1: Message 1");
            writer.writeToFile("Thread 1: Message 2");
        });

        Thread thread2 = new Thread(() -> {
            Filewriter writer = new Filewriter("src/chap60_singleton/test.txt");
            writer.writeToFile("Thread 2: Message 3");
            writer.writeToFile("Thread 2: Message 4");
        });

        Thread thread3 = new Thread(() -> {
            Filewriter writer = new Filewriter("src/chap60_singleton/test.txt");
            writer.writeToFile("Thread 2: Message 3");
            writer.writeToFile("Thread 2: Message 4");

            //👎 JVM GC 회수 매번 이루어져야 함
        });

        thread1.start();
        thread2.start();
        thread3.start();
    }
}
```

#### 👌🏻 싱글턴 사용한 코드

```java
//FilewriterSingleton.java
public class FilewriterSingleton {
    //⭐️ 스스로를 static으로 지정
    private static FilewriterSingleton instance;
    private FileWriter fileWriter;

    //FilewriterSingleton constructor
    public FilewriterSingleton() {
        try {
            //스스로를 만든다.
            //같은 파일에다가 쓸거니까 constructor에 바로 파일 정해버림
            this.fileWriter = new FileWriter("src/chap60_singleton/test.txt");
        } catch (IOException e) {
            e.printStackTrace();
        }
        }
    //자기 자신의 인스턴스 생성
    //❗️FilewriterSingleton는 공통영역이므로 동기화 문제 발생 가능
    //⭐️ synchronized
    public synchronized static FilewriterSingleton getInstance(){
        if(instance == null){
            //인스턴스가 처음에는 null
            //null이면 FilewriterSingleton을 생성한다
            instance= new FilewriterSingleton();
        }
        //instance가 null이 아니고 이미 만들어져 있으면 이미 만들어진 instance return
        return instance;
    }

    public synchronized void writeToFile(String message){
        try{
            fileWriter.write(message+"\n");
            fileWriter.flush();
        } catch (IOException e){
            e.printStackTrace();
        }
    }
    public synchronized void closeFile(){
        try {
            fileWriter.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

//FilewriterSingletonTest.java
public class FilewriterSingletonTest {
    public static void main(String[] args) {
        Thread thread1 = new Thread( () -> {
            // 객체 생성 매번 ❌
            // getInstance
            FilewriterSingleton  writer= FilewriterSingleton.getInstance();
            // writer.writeToFile("Thread 1: Message 1");
            // writer.writeToFile("Thread 1: Message 2");
        });
        //두 번째 호출부터는 FilewriterSingleton getInstance가 null이 아님
        //따라서 다시 만들지 않고 모든 thread가 이 객체 사용
        //따라서 singleton으로 코드 재사용성 높일 수 있다. ⬆️
        //❗️FilewriterSingleton는 공통영역이므로 동기화 문제 발생 가능
        //따라서 synchronize
        Thread thread2 = new Thread(() -> {
            FilewriterSingleton  writer= FilewriterSingleton.getInstance();
            // writer.writeToFile("Thread 2: Message 3");
            // writer.writeToFile("Thread 2: Message 4");
        });

        // thread1.start();
        // thread2.start();

        //join해서 파일 닫아야 함
        //GC도 FilewriterSingleton 재사용될 것 알아서 치워버리지 않음
    }
}

```

## 🧩 JAVA 빌더 패턴

복잡한 **객체의 생성 과정을 단순화**해서 **가독성**과 **유연성** 높여 객체 생성하기<br>
객체 생성 과정을 1단계, 2단계, 3단계...이렇게 단순화해서<br>

- static inner class<br>
- 내부 this 변환<br>

### userBuilder 개선

유저 객체 생성할 때 이름, 이메일 등 순서를 헷갈릴 수 있음<br>
실수할 수 있는 여지를 줄이기<br>
Builder 이용하면 순서 바꿔서 입력해도 괜찮음.<br>

#### 👎🏻 기존 코드

```java
//User.java
public class User {
    private String firstName;
    private String lastName;
    private int age;
    private String email;

    public User(String firstName, String lastName, int age, String email) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.age = age;
        this.email = email;
    }

    public String getFirstName() {
        return firstName;
    }

    public String getLastName() {
        return lastName;
    }

    public int getAge() {
        return age;
    }

    public String getEmail() {
        return email;
    }
}

//BuilderTest.java
public class BuilderTest {
    public static void main(String[] args) {
        // 적용 전
        User user1 = new User("John", "Doe", 30, "johndoe@example.com");
        System.out.println("적용 전 User: " + user1);
    }
}
```

#### 👌🏻 빌더 패턴 사용한 코드

```java
//User.java
public class User {
    // private String firstName;
    // private String lastName;
    // private int age;
    // private String email;

    // public User(String firstName, String lastName, int age, String email) {
    //     this.firstName = firstName;
    //     this.lastName = lastName;
    //     this.age = age;
    //     this.email = email;
    // }

    //⭐️ 새로운 User생성자
    //private
    //️UserBuilder를 아래에서 받아온다.
    private User(UserBuilder userBuilder){
        this.firstName= userBuilder.firstName;
        this.lastName= userBuilder.lastName;
        this.age= userBuilder.age;
        this.email= userBuilder.email;
    }

    //⭐️UserBuilder는 static inner 클래스로 만든다.
    static class UserBuilder{
        //⭐️ user클래스의 필드 그대로 가지고 있는다.
         String firstName;
         String lastName;
         int age;
         String email;

        //⭐️ UserBuilder 내부 정적 클래스의 constructor
        //빈 constructor을 생성한다.
        //UserBuilder 내부 정적 클래스 안에서 constructor 정의해야 함 유의!
        public UserBuilder() {}

        //⭐️ method
        //UserBuilder을 반환하는 메소드
        public UserBuilder firstName(String firstName){
           this.firstName = firstName;
           return this;
        }
        public UserBuilder lastName(String lastName){
            this.lastName= lastName;
            return this;
        }
        public UserBuilder age(int age){
            this.age= age;
            return this;
        }
        public UserBuilder email(String email){
            this.email= email;
            return this;
        }
        //⭐⭐⭐ 최종 user 반환하는 method
        public User build(){
            return new User(this);
        }

    }

    // public String getFirstName() {
    //     return firstName;
    // }

    // public String getLastName() {
    //     return lastName;
    // }

    // public int getAge() {
    //     return age;
    // }

    // public String getEmail() {
    //     return email;
    // }

    // @Override
    // public String toString() {
    //     return "User{" +
    //             "firstName='" + firstName + '\'' +
    //             ", lastName='" + lastName + '\'' +
    //             ", age=" + age +
    //             ", email='" + email + '\'' +
    //             '}';
    // }
}

public class BuilderTest {
    public static void main(String[] args) {
        // 적용 전
        // User user1 = new User("John", "Doe", 30, "johndoe@example.com");
        // System.out.println("적용 전 User: " + user1);

        //Builder 적용 후
        //이름은 이거, 나이는 이거...이렇게 명시하니 헷갈리지 않아서 좋음
        User user2= new User.UserBuilder()
                .firstName("John")
                .lastName("Doe")
                .age(30)
                .email("johndoe@example.com")
                .build();
        System.out.println("빌더 적용 후 User: " + user2);

        //Builder와 함께하면 순서 바꿔도 상관 없음
        User user3= new User.UserBuilder()
                .email("johndoe@example.com")
                .lastName("Doe")
                .age(30)
                .firstName("John")
                .build();
        System.out.println("빌더 적용하면 순서 바꿔도 상관 없어: " + user3);

    }
}

```

## 🧩 JAVA 데코레이터 패턴

기존 **객체 변경 없이** 동적으로 기능을 **추가**하거나 **수정**하는 디자인 패턴<br>
기존 객체에 옵션이나 기능을 추가해야 하는 상황에 주로 사용<br>

- 추상클래스<br>
- 인터페이스<br>
- upcasting<br>

### 커피 만드는 코드

그냥 커피에 우유, 설탕, 크림 추가하는 코드<br>
<br>

- implements inferface<br>
- extends class<br>
- upcasting<br>

```java
//✅ Beverage interface
public interface Beverage {
    String getDescription();
    double cost();
}

//✅ BeverageDecorator.java
public class BeverageDecorator implements Beverage{
    protected Beverage beverage;

    public BeverageDecorator(Beverage beverage) {
        this.beverage = beverage;
    }

    @Override
    public String getDescription() {
        return beverage.getDescription();
    }

    @Override
    public double cost() {
        return beverage.cost();
    }
}

//✅ Coffee.java
public class Coffee implements Beverage{
    @Override
    public String getDescription() {
        return "Coffee";
    }

    @Override
    public double cost() {
        return 5.0;
    }
}

//✅ milk.java
public class Milk extends BeverageDecorator{
    public Milk(Beverage beverage) {
        super(beverage);
    }

    //👌🏻 데코레이터 사용한 코드
    @Override
    public String getDescription() {
        return super.getDescription() + ", Milk";
    }
    //👌🏻 데코레이터 사용한 코드
    @Override
    public double cost() {
        return super.cost() + 0.5;
    }
}

//✅ sugar.java
public class Sugar extends BeverageDecorator{

    public Sugar(Beverage beverage) {
        super(beverage);
    }
    //👌🏻 데코레이터 사용한 코드
    @Override
    public String getDescription() {
        return super.getDescription()+ ", Sugar";
    }
    //👌🏻 데코레이터 사용한 코드
    @Override
    public double cost() {
        return super.cost() + 0.3;
    }
}

//✅ Cream.java
public class Cream extends BeverageDecorator{


    public Cream(Beverage beverage) {
        super(beverage);
    }
    //👌🏻 데코레이터 사용한 코드
    @Override
    public String getDescription() {
        return super.getDescription() + ", Cream";
    }
    //👌🏻 데코레이터 사용한 코드
    @Override
    public double cost() {
        return super.cost() + 2.0;
    }
}

//✅ 실행클래스
public class OrderCoffee {
    public static void main(String[] args){

        // 현재 Milk 추가 가능
        //💡upcasting: coffee ➡️ beverage
        Beverage coffee = new Coffee();
        System.out.println(coffee.getDescription() + ": $" + coffee.cost());

        //💡upcasting: milk ➡️ beverage
        Beverage coffeeWithMilk = new Milk(coffee);
        System.out.println(coffeeWithMilk.getDescription() + ": $" + coffeeWithMilk.cost());


        //💡upcasting: sugar ➡️ beverage
        Beverage coffeeWithSugar= new Sugar(coffeeWithMilk);
        System.out.println(coffeeWithSugar.getDescription()+ ": $" +coffeeWithSugar.cost());

        Beverage coffeeWithCream= new Cream(new Milk(new Coffee())); //커피에 우유 타고 그 위에 크림 얹기
        System.out.println(coffeeWithCream.getDescription() + ": $" + coffeeWithCream.cost());

    }
}
// 실행결과
// Coffee: $5.0
// Coffee, Milk: $5.5
// Coffee, Milk, Sugar: $5.8
// Coffee, Milk, Cream: $7.5

```

### ✔️ JAVA 데코레이터 패턴과 I/O Stream

I/O Stream이 대표적인 데코레이터 패턴이다.<br>
bufferReader같은 경우, reader의 기능을 유지하면서 속도 빠르게 기능만 추가하는 것이고<br>
Printwriter도 writer의 기능을 유지하면서 println, printf기능을 추가하는 것이다.<br>

## 🧩 JAVA 전략 strategy 패턴

동적으로 **교체 가능한 전략**을 제공하고 객체 관계를 우연하게 만드는 디자인<br>
골프칠 때 거리, 상황에 맞는 골프채를 고르는 것<br>
변경이나 수정이 잦은 내부 정책 클래스에 주로 사용<br>
상황마다 비즈니스 전략 바뀌는 경우<br>
(백화점에서 시즌에 따라서 세일을 진행하거나, 가격 인상을 하는 경우)<br>

- 인터페이스<br>
- setter<br>
- 다형성<br>

### discount 코드에 전략 패턴 적용

신규 가입자/ 시즌 할인/ 친구 추천 할인 적용된 전략 패턴 코드 사용 <br>

```java
//Interface
//✅ DiscountStrategy.java
public interface DiscountStrategy {
        double calculateDiscount(double amount);
}

//✅ DiscountCaculator.java
//계산기는 여기서
public class DiscountCaculator {
    private DiscountStrategy discountStrategy;

    public void setDiscountStrategy(DiscountStrategy discountStrategy) {
        this.discountStrategy = discountStrategy;
    }

    public double calculateDiscount(double amount) {
        if (discountStrategy != null) {
            return discountStrategy.calculateDiscount(amount);
        } else {
            return 0; // 할인 없음
        }
    }
}

//✅ NewCustomerDiscount.java
//신규고객 할인
public class NewCustomerDiscount implements DiscountStrategy{
    @Override
    public double calculateDiscount(double amount) {
        return amount * 0.2; // 20% 할인
    }
}
//✅ SeasonDiscount.java
//시즌 할인
public class SeasonDiscount implements DiscountStrategy{
    @Override
    public double calculateDiscount(double amount) {
        return amount * 0.1;
    }
}
//✅ FriendDiscount.java
//친구추천 할인
public class FriendDiscount implements DiscountStrategy{
    @Override
    public double calculateDiscount(double amount) {
        return amount * 0.15;
    }
}
//✅ StrategyTest.java
//실행메소드
public class StrategyTest {
    public static void main(String[] args) {

        DiscountCaculator calculator = new DiscountCaculator();

        // 신규 가입자 할인
        // 상황마다 각각 다른 전략
        calculator.setDiscountStrategy(new NewCustomerDiscount());
        double discount1 = calculator.calculateDiscount(10000);

        System.out.println("신규 가입자에게 " + discount1+ "원 만큼 할인해 줍니다.");

        //시즌 할인
        calculator.setDiscountStrategy(new SeasonDiscount());
        double discount2= calculator.calculateDiscount(10000);

        System.out.println("시즌 할인으로 " + discount2+ "원 만큼 할인해 줍니다.");

        //친구 할인
        calculator.setDiscountStrategy(new FriendDiscount());
        double discount3= calculator.calculateDiscount(10000);

        System.out.println("친구 추천으로 " + discount3+ "원 만큼 할인해 줍니다.");
    }
}

```

## 🧩 Template Method Pattern

> Capsulize part of the overall service <br>
> change small details for each stage <br>

- 상속 `extends` 이용한 대표적인 디자인 패턴
- `parent class`: define overall algorithm
- `child class`: override algorithm

- 전체적으로는 동일
- 부분적으로는 다른 구문으로 구성되는 메소드의 코드 중복 최소화
- `parent class`: 동일한 기능 정의
- `child class`: 확장/변화 필요한 부분만 서브 클라스에서 구현

- 예시
- 대량 집 짓기
- `parent class`: 뼈대 만들기
- `child class`: 세부 사항 조절

- 👍🏻 reduce code repetition
- 👍🏻 OOP
- 👍🏻 child class burden ⬇️
- 👍🏻 centralized management of critical code
- 👎🏻 lots of abstract class
- 👎🏻 relationship among class can become complex
