---
title: ⭐️Abstract 추상화
categories: [JAVA, JAVA_Basics]
tags: [abstract, override] # TAG names should always be lowercase
---

## ✅ 추상화

현 상황에 불필요한 정보들은 없애고, 정말 필요한 핵심 특징만 모아놓은 것 <br>
코드도 마찬가지, 물고기에게는 많은 특징이 있지만 필드, 메소드에서 모든 특징을 정의하지 않음. <br>
지금 함수에 필요한 특징만 정의하고 인스턴스로 선언함. ➡️ 추상화 <br>

## ✅ abstract class

- 실재하지는 않지만, 하위의 공통적인 필드, 메소드를 기준으로 묶어놓은 개념<br>
- 실재하지 않기때문에 **인스턴스화 할 수는 없음.**<br>
- **자식 클래스로 파생되기 위한 클래스**
- 자식들이 **공통된 특성**을 가지기 위함
- 실행 클래스에서 instance생성하지 않고도 바로바로 불러와 사용 가능<br>

## ✅ abstract method

참고로, 추상 필드는 없음.<br>

### ⭐️ 추상 메소드 특징

#### 추상 클래스에서만 사용 가능

- **추상클래스 일 떄** 추상 메소드 선언 가능<br>

#### 스스로는 선언만 하고 구현하지 않음.

- 그냥 메소드 이름만 쓰면 끝
- 자식 클래스가 구현할 것임(Override)

#### 메소드 override 의무

- 다른 클래스에서 추상 메소드를 **무조건** Override해야 한다.<br>
- 부모가 선언만 했지, 정의는 안했으니까 자식이 꼭 해야 한다.

```java
//abstract인 animal class
public abstract class Animal {
    protected int legNum;
    //abstract method 선언만 하고 끝
    abstract void eat();
    abstract void sleep();
}
//Dog class는 Animal을 extend하고 싶음.
//이 떄, 이렇게만 하면 상속 불가 ❌
public class Dog extends Animal{
}

//💡 추상 클래스의 메소드들을 override해야 한다.
//이렇게하면 상속 가능 ⭕️
public class Dog extends Animal{
    private String action;
    //추상 클래스에서 field받아오기 super
    public Dog(int legNum, String action){
        super(legNum);
        this.action= action;
    }
    //💡 추상 클래스의 메소드들을 override
    @Override
    public void eat(String food) {
        System.out.printf("Dog is barking and eating %s", food);
    }
    //💡 추상 클래스의 메소드들을 override
    @Override
    public void sleep() {
        System.out.println("Dog is sleeping");
    }
}

```
