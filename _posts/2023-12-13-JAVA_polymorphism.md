---
title: JAVA polymorphism 다형성_downcasting/ instanceof/ final
categories: [JAVA, JAVA_Basics]
tags: [polymorphism, downcasting, upcasting, final] # TAG names should always be lowercase
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
🟰 자식 클래스는 부모 클래스에 속한다는 것을 알 수 있다.
❌ 단, 부모 클래스는 자식 클래스로 선언하는 것 불가
(새, 물고기, 사람은 동물이지만, 모든 동물이 새가 아닌 것처럼 )

```java

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
        Animal animal= (Animal) person;
    }
```

## 💡 `instanceof` 사용해 if문

**객체 `instanceof` 클래스**
이 인스턴스가 원래 어떤 클래스꺼지인지 확인하는 연산자 (너 원해 bird야?) <br>
하위 클래스 인스턴스인지 확인하는 함수 <br>
인스턴스의 객체 타입을 확인하는 연산자 <br>
형 변환 가능 여부를 true/false로 반환 <br>

```java
Animal guessWhatAnimal= new Bird();

static void checkBirdThenFly(Animal animal){
    if (guessWhatAnimal instanceof Bird){
        //downcast
        Bird bird= (Bird) guessWhatAnimal;
        }
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

## ✅ JAVA final keyword

### ☑️ final field

final이 field 앞에 붙으면 값을 바꿀 수 없는 field가 되었음. <br>
그래서 필드 선언할 때 생성자에서 초기화해야 하고, 이 값은 평생 가는 값이다. <br>
수정이 불가능하기 때문이다. <br>

### ☑️ final method

final로 메소드 오버라이딩 막기 <br>
메소드 앞에 final을 추가하면 오버라이딩 불가 <br>

```java
public final class Animal{
    //method 앞에 final 붙이기
    public final void eat(String food)
}
//이렇게 final로 함수 만들면 Animal.eat()함수를 override하던 함수들에서
//💥 Make Animal.eat() not final이라고 뜬다.
```

### ☑️ final instance

다른 값을 넣는 것은 불가하다. <br>
field는 바꿀 수 있음 (주소는 못 바꾸지만 인테리어는 바꿀 수 있는 것처럼) <br>

### ☑️ final class

final로 클래스 상속 막기 <br>
final을 추가하면 이 클래스는 부모가 될 수 없음. <br>

```java
public final class Animal{

}
//이렇게 final로 만들면 animal클라스를  inherit하던 함수들 빨간줄
//💥 Cannot inherit from final
//make animal not final
```
