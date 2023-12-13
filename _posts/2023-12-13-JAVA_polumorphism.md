---
title: JAVA polymorphism 다형성
categories: [JAVA, JAVA_Basics]
tags: [polymorphism, downcasting] # TAG names should always be lowercase
---

## ✅ JAVA OOP 다형성

하나의 타입이나 메소드가 **여러** 타입이나 메소드를 가지거나 실행하는 능력<br>

<br>
아래 코드에서 모든 객체에 같은 함수를 정의해도, 인스턴스 내부에서 어떤 method를 가졌는지에 따라 결과물이 다르다.
Animal이라는 타입이 animal/bird/fish/person 여러 타입이나 메소드를 가지고 실행한다.

```java
public static void main(String[] args) {
        //다형성의 핵심은 왼쪽이 아니라 오른쪽에 있다.
        //왼쪽에 타입을 Animal로 했어도 오른쪽의 인스턴스가 animal/bird/fish/person인지에 따라 행위가 달라진다.
        Animal animal= new Animal();
        Animal bird= new Bird(); //upcast
        Animal fish= new Fish();
        Animal person= new Person();

        feed(animal, "bugs");
        feed(bird, "cherry");
        feed(fish, "shrimp");
        feed(person, "rice");
    }

    //method
    //animal의 method를 불러옴
    public static void feed(Animal animal, String food){
        animal.eat(food);
    }
}
// Animal is eating bugs
// Bird is poking on cherry
// Fish is swimming and eating shrimp
// A person is eating rice with a chopstick
```

## ✅ downcasting

하위 클래스로 형 변환
🟰 upcast의 반대 작용
🟰 부모 클래스에서 자식 클래스로 형 변환
🟰 (단, 인스턴스의 그대로 돌아가야 한다.)

````java

public class AnimalDowncast {
    public static void main(String[] args) {
        //downcasting
        //부모 타입으로 선언한 자식 인스턴스가 다시 자식 인스턴스로 돌아감
        //타입은 animal이지만 사실은 bird이지롱
        //원래 bird였던 애만 다시 bird로 downcast 할 수 있다.
        Animal guessWhatAnimal1= new Bird();
        //downcast ⭕️
        Bird bird= (Bird) guessWhatAnimal1;

        //downcast ❌
        //animal로 만들었고 animal이 부모이기 때문에 자식으로 변환 ❌
        Animal guessWhatAnimal2= new Animal();
        Bird bird2= (Bird) guessWhatAnimal2;

        //class끼리 형 변환 ❌
        //타입은 animal이지만 사실은 fish이지롱
        //그리고 bird로 바꾸면? ❌
        Animal guessWhatAnimal3= new Fish();
        Bird bird3= (Bird) guessWhatAnimal3;

        //upcasting
        //자식 클래스가 부모 클래스의 타입을 받아와 인스턴스 선언하는 것
        Person person= new Person();
        Animal animal= (Animal) person;```

### `instanceof` 사용해 if문
**객체 `instanceof` 클래스**
이 인스턴스가 원래 어떤 클래스꺼지인지 확인하는 연산자 (너 원해 bird야?)
하위 클래스 인스턴스인지 확인하는 함수
인스턴스의 객체 타입을 확인하는 연산자
형 변환 가능 여부를 true/false로 반환
```java
Animal guessWhatAnimal= new Bird();

static void checkBirdThenFly(Animal animal){
    if (guessWhatAnimal instanceof Bird){
        //downcast
        bird= (Bird) guessWhatAnimal;
        }
    }
}
````

## ✅ JAVA final keyword
