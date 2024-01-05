---
title: Static
categories: [JAVA, JAVA_Basics]
tags: [static, instance, local] # TAG names should always be lowercase
---

## ✅ static

`클래스 이름.static 변수 이름` <br>
<br>

static(정적)은 마치 본사의 정보와 기능을 정의해 두는 것과 같다. <br>
모든 인스턴스마다 **동일하게** 가지고 있을 것들에 대해서 사용 <br>
모든 인스턴스들이 **공통적인 값**을 유지해야 하는 속성<br>
모든 인스턴스가 **공통된 저장공간(변수)**를 공유하게 된다. <br>
인스턴스들이 값을 바꿀 수 있음. <br>

### ☑️ static 변수의 의미

🟰 정적 변수<br>
🟰 클래스 변수(클래스에 속해 있음. 인스턴스 아니고❌)<br>
🟰 프로그램 실행 시, 정적 생성<br>
🟰 프로그램 실행 시, 이미 생성되어 있음<br>
🟰 인스턴스 생성 전 정의되어 있음.<br>
🟰 그래서 모든 인스턴스들이 접근 가능하다.<br>
따로 `new`와 `constructor`로 **인스턴스를 생성하지 않아도** 바로바로 불러와서 사용 가능하다 <br>
<br>

## ☑️ instance 변수 🆚 static 변수

1️⃣ instance 변수는 인스턴스를 생성한 다음에 불러올 수 있다. <br>
static 변수는 인스턴스 생성하지 않아도 바로바로 불러올 수 있다. <br>
2️⃣ 인스턴스는 독립적인 공간을 가지므로, 서로 다른 값을 가지지만
static 변수는 모든 인스턴스가 공통적인 값을 유지해야 할 때 사용한다. <br>
3️⃣ 인스턴스의 멤버 변수 앞에는 `this`붙일 수 있지만, ⭕️ <br>
static 변수 앞에서는 붙이지 않는다. ❌ <br>
4️⃣ instance는 static의 field, method를 사용할 수 있지만 ⭕️ <br>
static은 instance의 field, method를 사용할 수 없다. ❌ <br>
<br>

⭐️ static 변수가 instance 변수를 참조 또는 호출하고자 할 때에는 인스턴스를 생성해야 한다. <br>
인스턴스 멤버가 존재하는 시점에 클래스 멤버는 항상 존재하지만, <br>
클래스 멤버가 존재하는 시점에 인스턴스 멤버가 존재하지 **않을 수도** 있기 때문이다. <br>
<br>

따라서 instance 변수는 인스턴스 생성 없이도 static 변수 호출 가능 <br>
그러나, static 변수가 instance 변수를 참조 또는 호출하고 싶으면 인스턴스 생성 해야만 함! <br>
<br>
인스턴스 멤버가 인스턴스 멤버 호출하는데는 제약 없음 <br>
인스턴스 멤버가 있다는 것이 곧 인스턴스가 생성되어 있다는 것을 의미하므로 <br>

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

## ✅ static method

class method(🟰 static method)도 static이므로 객체를 생성하지 않고 호출 가능하다. <br>
static method는 인스턴스 변수를 사용할 수 없다. <br>

### 🆚 static method, instance method

static method: 인스턴스와 관계 없는(인스턴스 변수나 인스턴스 메서드를 사용하지 않는) 메서드<br>
instance method: 인스턴스 변수와 관련된 작업을 하는, 메서드의 작업을 수행하는데 인스턴스 변수를 필요로 하는 메서드<br>
