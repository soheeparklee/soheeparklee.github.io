---
<<<<<<< Updated upstream
title: Class_Static
=======
title: Class_Static(Instance 🆚 Local), block, scope
>>>>>>> Stashed changes
categories: [JAVA, JAVA_Basics]
tags: [static, instance, local] # TAG names should always be lowercase
---

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

## ☑️ instance 변수 🆚 static 변수

인스턴스의 멤버 변수 앞에는 `this`붙일 수 있지만, ⭕️ <br>
static 변수 앞에서는 붙이지 않는다. ❌ <br>
instance는 static의 field, method를 사용할 수 있지만 ⭕️ <br>
static은 instance의 field, method를 사용할 수 없다. ❌ <br>

## ☑️ JAVA static 변수/메소드

만약 static앞에 private를 붙이고 싶다면? ➡️ 불러오기 위해서 getter, setter 만들어야 함. <br>
그런데, **setter**만들 때 static 변수 앞에는 `this`를 붙일수 없다! <br>
대신, class의 이름을 붙여야 한다.<br>

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

## ☑️ static을 본사와 지점에 비유하자면?

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
<<<<<<< Updated upstream
=======

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

## ✅ block { }

```java
//  💡 { } 로 블록 생성
{
    int x = 1; //한 줄 한 줄이 statement
    System.out.println(x);
}
```

## ✅ scope

변수가 사용되는 범위 <br>
일반적으로하는 한 block 이 새로운 scope <br>
block내에서 선언된 변수는 block을 벗어나면 사용 불가 <br>
<br>
바깥 scope에서 만들어진 변수는 또 다른 scope안에서 사용 가능하지만, <br>
한 block내에서 만들어진 변수는 그 block을 벗어나면 사용 불가 <br>
<br>
scope 외부에서 선언된 변수를 내부에 또 선언 불가능 <br>
그러나 인스턴스의 필드는 scope내에서 변수로 선언 가능 <br>
>>>>>>> Stashed changes
