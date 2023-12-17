---
title: JAVA Program Arguments, Main method, Package, Block, Scope
categories: [JAVA, JAVA_Basics]
tags: [argument] # TAG names should always be lowercase
---

## ✅ Block

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

해당 변수가 유효한 범위

- 클래스 메소드에서는 인스턴스 변수 사용 불가
- 클래스 내 필드의 스코프 : 해당 클래스 안
- 메소드 내 변수의 스코프 : 해당 메소드 안

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

<<<<<<< Updated upstream
자바 실행 시, 외부에서 전달받는 변수
Command Line(terminal)에서 주는 명령이 args에 저장되어서 이름이 명령 매개변수임.

<img width="291" alt="스크린샷 2023-12-16 오후 4 59 46" src="https://github.com/soheeparklee/sc_project_carrotMkt_improved/assets/97790983/5c036296-5edf-46f0-bca7-75e0112a4e67">

<img width="1041" alt="스크린샷 2023-12-16 오후 5 00 53" src="https://github.com/soheeparklee/sc_project_carrotMkt_improved/assets/97790983/67544078-7e31-4482-8e58-0ad237178a61">

## ✅ Package

패키지를 import해 주어야 한다.

```java
import sec06.chap02.pkg1.Parent;
```

클래스 이름이 똑같아도 어디 패키지에 들어있는지 알기 위해 사용

### 패키지에 따라 access modifier도 달라진다.

- private: 오로지 같은 class 내에서
- default: 같은 패키지 안에서
- protected: 상속 관계면 가능(다른 패키지일 때도)

### ⭐️ 다른 패키지에 있는 클래스도 상속할 수 있다.

**protected** access modifier만 사용할 수 있을 것이다.
패키지는 다르지만, 상속 관계는 맞으니까

### 패키지 안에 있는 모든 클래스 가져와 \*

```java
import sec06.chap02.pkg3.* //pkg3안에 있는 모든 클래스 가져오기
```
=======
args라는 배열은 string배열이다. <br>

```java
    public static void main(String[] args) {
        //외부에서 args배열 값 받아오기
        String menuName = args[0];
        String spicyLevel = args[1];

        System.out.printf("%s 맵기 강도 %s로 주문%n", menuName, spicyLevel);
    }
```

인텔리제이 ▶️ 누르고 edit configuration <br>
하고 외부에서 args 넣을 수 있다. <br>
<img width="291" alt="스크린샷 2023-12-16 오후 4 59 46" src="https://github.com/soheeparklee/sc_project_carrotMkt_improved/assets/97790983/76918986-b83c-4f63-9ed1-f2b381d9b23e">

<img width="1041" alt="스크린샷 2023-12-16 오후 5 00 53" src="https://github.com/soheeparklee/sc_project_carrotMkt_improved/assets/97790983/d79d1d14-73eb-4465-b3df-b440639adf59">
>>>>>>> Stashed changes
