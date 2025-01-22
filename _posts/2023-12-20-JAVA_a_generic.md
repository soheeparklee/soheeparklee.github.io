---
title: Generic
categories: [JAVA, JAVA_Basics]
tags: [generic] # TAG names should always be lowercase
---

## ✅ Generic 프로그래밍

❓ 로직은 다 똑같은데 **datatype**만 바꾸는 코드를 짜야 한다면? <br>
❌ object가 최상위클라스니까, object class로 구현해볼까?<br>
그러나 항상 downcasting해야하는 한계가 있다. 😨<br>

- 안전하게 **같은 코드**를 여러 **참조형**에 사용하여 **코드 재사용성** 올리는 프로그램 기법<br>
- 타입을 일반적으로 지정하지 않은 클래스/인터페이스/메소드를 정의

✔️ **Convariant**

- 상위타입에서 하위타입으로 형 변환 가능
- Number class ➡️ Integer, Double class

✔️ **Contravariant**

- 하위 타입에서 상위 타입으로 형 변환 가능

### Generic type 선언

- class<br>
- interface로 선언<br>

- 제네릭 타입은 **타입을 parameter**로 가지는 클래스와 인터페이스를 말한다.<br>
- class/ interface 이름 뒤에 <> 부호가 붙고 사이에 타입 parameter<br>
- parameter는 꼭 대문자 알파벳 1글자<br>
  <br>

```java
public class GeneralPrint<T> {
    private T material;
//이 method를 string, boolean, integer에서도 다 사용하고 싶어(datatype만 다르게 해서 )
    public void printMyInfo(){
        System.out.println("Using Generic to print " + material + " and this datatype is a "+ material.getClass());
    }
    //getter, setter
    public void setMaterial(T material){
        this.material= material;
    }
    public T getMaterial(){
        return this.material;
    }
}


public class PrintSituation {
    public static void main(String[] args) {
        //똑같이 printer이라서 같은 GeneralPrint class 공유하는데, datatype만 다르게 출력하고 싶음
        //1️⃣ String printer
        //기존에는 이렇게 인스턴스만 만들었다면 여기에 datatype을 붙여준다. <String>
        //GeneralPrint printStr= new GeneralPrint();
        GeneralPrint<String> printStr= new GeneralPrint<String>();
        printStr.setMaterial("So Hee");

        // Generic으로 downcast 할 필요 이제 없어짐!
        //String materialString=  (String) printStr.getMaterial();

        //getter해서 method 실행
        String materialString= printStr.getMaterial();
        printStr.printMyInfo();
        //Using Generic to print So Hee and this datatype is a class java.lang.String

        //2️⃣ Integer printer
        GeneralPrint<Integer> printInt= new GeneralPrint<Integer>();
        printInt.setMaterial(123);


        int materialInt= printInt.getMaterial();
        printInt.printMyInfo();
        //Using Generic to print 123 and this datatype is a class java.lang.Integer

        //3️⃣ boolean printer
        GeneralPrint<Boolean> printBool= new GeneralPrint<Boolean>();
        printBool.setMaterial(true);
        Boolean materialBool= printBool.getMaterial();
        printBool.printMyInfo();
        //Using Generic to print true and this datatype is a class java.lang.Boolean



    }
}

```

## ✅ Generic 심화

✔️ **static은 Generic불가**

static은 시점: class load 시점 <br>
generic 시점: 인스턴스 생성 시점 <br>
따라서 generic생성 시점보다 static 시점이 먼저이기 때문에 static은 Generic불가 <br>

✔️ **Generic은 두 개 이상 사용 가능**

## ✅ Super, Extends
> Generic programming 자료형 제한하기 <br>
> 자바 타입 파라미터를 제한하기 위해 사용 <br>

- 근데...Generic은 너무 넓은 범위의 datatype 받는거 아니야?<br>
- 내가 원하지 않는 datatype이 Generic에 입력되면 어떡하지? 나는 int만 받고 싶은데 
- string들어오면? <br>

### 💡 Super
- 특정 **상위** 타입만을 허용


### 💡 Extends
- 특정 **하위** 타입만을 허용
- number의 하위 타입인 integer, double만 허용
- `extends Number`을 사용해 숫자만 Generic에 들어올 수 있도록 한다. <br>
- ⭐️ number: float, integer, double 모두 속하는게 number <br>

### 💡 ?
- 와일드카드
- `<?>` : 전체 타입 가능
- `<? extends 상위타입 A>` : 상한선, A자식클래스 까지만 가능
- `<? extends 하위타입 B>` : 하한선, B조상클래스까지만 가능



### 좌표의 거리를 구하기: 우선 extends안 쓰고 구현

```java
public class Point <T, V>{ //Generic은 두 개 이상 사용 가능
    //generic
    private T x;
    private V y;

    //getter

    public T getX() {
        return x;
    }

    public V getY() {
        return y;
    }

    //constructor

    public Point(T x, V y) {
        this.x = x;
        this.y = y;
    }

    //method
    public Double caculateDistance(){

        //instanceof
        //x, y 모두 number의 타입이어야 한다. float, integer, double 모두 number에 속한다.
        //x, y 가 숫자가 아니면 null
        // 🥱 근데 매번 이렇게 number 아닌 경우 코드로 짜야 함? ➡️ extends number
        if(!(this.x instanceof Number)){
            return null;
        }
        if(!(this.y instanceof Number)){
            return null;
        }
        //downcast
        Double num1= ((Number) this.x).doubleValue();
        Double num2= ((Number) this.y).doubleValue();

        return Math.sqrt((Math.pow(num1, 2)) + (Math.pow(num2, 2)));
    }
}



public class PointSituation {
    public static void main(String[] args) {
        Point<Integer, Integer> point1= new Point(1, 5);
        Point<Integer, Double> point2= new Point(10, 15.5);
        Point<Double, Double> point3= new Point(4.5, 25.75);
        //이상한 datatype 넣으면?
        Point<String, Double> pointWrong= new Point("Hello", 25.75);


        System.out.println(point1.caculateDistance()); //5.0990195135927845
        System.out.println(point2.caculateDistance()); //18.445866745696716
        System.out.println(point3.caculateDistance()); //26.140246747113924
        System.out.println(pointWrong.caculateDistance()); //null
    }
}

```

### extends 써서 구현

if문 사용할 필요 ❌<br>

```java
//T, V는 number extends하니까 무조건 숫자일 것임.
public class Point <T extends Number, V extends Number>{
    //generic
    private T x;
    private V y;

    //getter

    public T getX() {
        return x;
    }

    public V getY() {
        return y;
    }

    //constructor

    public Point(T x, V y) {
        this.x = x;
        this.y = y;
    }

    //method
    public Double caculateDistance(){
        //downcast
        Double num1= this.x.doubleValue();
        Double num2= this.y.doubleValue();

        return Math.sqrt((Math.pow(num1, 2)) + (Math.pow(num2, 2)));
    }
}

```
