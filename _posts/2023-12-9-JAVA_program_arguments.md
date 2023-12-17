---
title: JAVA Program Arguments, Main method, Package, Block, Scope
categories: [JAVA, JAVA_Basics]
tags: [argument] # TAG names should always be lowercase
---

## ✅ Block

```java
//  💡 { } 로 블록 생성
{
    int x = 1; //한 줄 한 줄이 statement
    System.out.println(x);
}
```

```java
int z =1;
//block
for (int i = 0; i < 5; i++) {
    System.out.println(z + i);  //statement
//  ⚠️ 블록 밖에서 선언된 것은 안에서 재선언 불가
    int z = 2; //불가
}
//  ⚠️ 블록 안에서 선언된 것은 밖에서 사용 불가
    System.out.println(i);  //불가
```

## ✅ Scope

해당 변수가 유효한 범위 <br>
<br>

- 클래스 메소드에서는 인스턴스 변수 사용 불가 <br>
- 클래스 내 필드의 스코프 : 해당 클래스 안 <br>
- 메소드 내 변수의 스코프 : 해당 메소드 안 <br>

변수가 사용되는 범위 <br>
일반적으로하는 한 block 이 새로운 scope <br>
block내에서 선언된 변수는 block을 벗어나면 사용 불가 <br>
<br>
바깥 scope에서 만들어진 변수는 또 다른 scope안에서 사용 가능하지만, <br>
한 block내에서 만들어진 변수는 그 block을 벗어나면 사용 불가 <br>
<br>
scope 외부에서 선언된 변수를 내부에 또 선언 불가능 <br>
그러나 인스턴스의 필드는 scope내에서 변수로 선언 가능 <br>

## Static 🆚 Instance 🆚 Local

```java
public class Variable {
    //static 클래스 변수
    // 프로그램이 처음 시작될 때 생성, 프로그램 끝나고 메모리 해제할 때 소멸
    private static int classVariable;
    //인스턴스 변수
    // 객체에 속한 변수
    // 힙이 생성되고 JVM위에 올라감
    private int instanceVariable1;
    //로컬 변수(지역변수)
    // 메소드에서 쓰이고 사라지는 변수
    // 메소드 안에서만 의미가 있지, 밖에서는 의미가 없음
    public void saySomething(int lcoalVarable){
        int localV= 3;
    }

}
```

## ✅ Program Arguments(Command Line Arguments)

```java
    public static void main(String[] args) {
    }
```

`String[] args`
🟰 JAVA Program Arguments <br>
🟰 Command Line Arguments <br>
🟰 자바 명령 매개변수 <br>
<br>
자바 실행 시, 외부에서 전달받는 변수 <br>
Command Line(terminal)에서 주는 명령이 args에 저장되어서 이름이 명령 매개변수임. <br>
<br>
args라는 배열은 string배열이다. <br>
인텔리제이 ▶️ 누르고 edit configuration <br>
하고 외부에서 args 넣을 수 있다. <br>

<img width="291" alt="스크린샷 2023-12-16 오후 4 59 46" src="https://github.com/soheeparklee/sc_project_carrotMkt_improved/assets/97790983/5c036296-5edf-46f0-bca7-75e0112a4e67">

<img width="1041" alt="스크린샷 2023-12-16 오후 5 00 53" src="https://github.com/soheeparklee/sc_project_carrotMkt_improved/assets/97790983/67544078-7e31-4482-8e58-0ad237178a61">

## ✅ Package

## 클래스 안에서 패키지 정보 가져와 명시

```java
package sec06.chap02.pkg4;
```

패키지 구조를 설명함. <br>
패키지를 import해 주어야 한다. <br>
클래스 이름이 같더라도 다른 패키지 안에 들었으면 사용 가능 <br>
클래스 이름이 똑같아도 어디 패키지에 들어있는지 알기 위해 사용 <br>

### 패키지에 따라 access modifier도 달라진다.

패키지에 따라서 access modifier 달라진다. <br>
예를 들어 protected이면 같은 패키지 또는 상속 관계 안에서는 사용 가능. <br>

- private: 오로지 같은 class 내에서 <br>
- default: 같은 패키지 안에서 <br>
- protected: 상속 관계면 가능(다른 패키지일 때도) <br>

### ⭐️ 다른 패키지에 있는 클래스도 상속할 수 있다.

다른 패키지에서 가져온 클래스로부터도 상속받을 수 있다. <br>
상단에 import하면 가능 <br>
<br>

```java
import sec06.chap02.pkg1.Parent; // pkg1안에 있는 Parent 클래스 가져오기
import sec06.chap02.pkg2.* //⭐️ 와일드카드 *: pkg2안에 있는 모든 클래스 가져오기
```

**protected** access modifier만 사용할 수 있을 것이다.
패키지는 다르지만, 상속 관계는 맞으니까

### 패키지 안에 있는 모든 클래스 가져와 \*

```java
import sec06.chap02.pkg3.* //pkg3안에 있는 모든 클래스 가져오기
```

### 서로 다른 패키지 안에 있는 동명 클래스 불러올 경우

인스턴스 선언할 때 주의해야 함! 어디 패키지의 클래스인지 명시하기

```java
//현재 pkg1안에도 Child클래스 있고, pkg2안에도 Child클래스 있는 상황
//❌ 이렇게 하면 어떤 패키지의 Child인지 알 수가 없음
        Child child1 = new Child();
//  ⭐️ 패키지가 다른 동명의 클래스들을 불러올 경우
        sec06.chap02.pkg1.Child child1 = new sec06.chap02.pkg1.Child();
        sec06.chap02.pkg2.Child child2 = new sec06.chap02.pkg2.Child();

```

```java
    public static void main(String[] args) {
        //외부에서 args배열 값 받아오기
        String menuName = args[0];
        String spicyLevel = args[1];

        System.out.printf("%s 맵기 강도 %s로 주문%n", menuName, spicyLevel);
    }
```
