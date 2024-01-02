---
title: Annotation, Reflection
categories: [JAVA, JAVA_Basics]
tags: [annotation] # TAG names should always be lowercase
---

## ✅ 메타 정보 & JAVA Annotation

일상 세계의 다양한 측면에 대한 **보조 정보** <br>
자바 프로그램의 추가적인 정보를 주는 메타 데이터 <br>
@ 사용 <br>

### ☑️ 종류

Custom annotation <br>
Built-in annotation <br>
<br>

- Meta annotation <br>
  어노테이션에 대한 메타 데이터 <br>
- general purpose annotation <br>
  - override <br>

### ☑️ 용도

✔️ 컴파일 타임 체크 및 오류 검출 <br>
✔️ JAVA 코드 문서화 <br>
✔️ 런타임 추가 기능 처리 ➡️ 메타 프로그래밍에 사용 <br>

## ✔️ 컴파일 타임 체크 및 오류 검출

오류가 있는지 없는지 검출하는 용도 <br>

#### @Override

부모 클래스 메소드가 없으면 error발생 <br>
그래서 만약 Override안 써도 동작은 하지만, <br>
Override쓰면 부모에게 없는 메소드 참조했을 때 error을 띄워 검증해 준다. <br>

#### @FunctionalInterface

람다식에서 <br>
메소드 1개를 초과하면 error발생, 개발자에게 알려준다. <br>

#### @Deprecate

문제가 생길 수 있는 메소드라는 뜻<br>
찍 그어서 경고문을 표시해준다. 사용하지 않는게 좋을텐데?<br>

```java
// ✅ Customer.java
public class Customer implements Serializable {
    @Deprecated
    public int calculatePrice(int price){
        this.bonusPoint += price * bonusRatio;
        return price;
    }
}

// ✅ GoldCustomer.java
//extends Customer
public class GoldCustomer extends Customer{
        @Override
    public int calculatePrice(int price) {
        price -= price * discountRatio;
        this.bonusPoint += price * bonusRatio;
        return price;
    }
}

// ✅ StringNum.java
@FunctionalInterface
//이것은 함수형 인터페이스라는 것을 알리기
//메소드가 1개만 있어야지, 2개 이상 되면 빨간줄
public interface StringNum {
    void printString(String s);
}

```

## ✔️ JAVA 코드 문서화

메소드에 대해서 설명해주기<br>

#### @ Params 및 @return

메소드가 어떤 parameter을 받고 어떤 값을 return하는지 설명해주기<br>

```java
    /**
     *
     * @param price int 물건의 가격을 param으로 받아요
     * @return int 최종 계산된 가격을 반환
     */
    public int calculatePrice(int price){
        this.bonusPoint += price * bonusRatio;
        return price;
    }
```

#### @ throws

이 메소드가 에러를 던진다면, 어떤 에러를 throw하는지 설명해주기 <br>

```java
    /**
     * @param fileName 읽을 파일의 이름
     * @return str 파일을 읽은 결과
     * @throws IOException 파일을 찾을 수 없는 경우 발생
     */
    public static String readFile(String fileName) throws IOException {
        // 파일 읽기 로직
        StringBuilder sb = new StringBuilder();
        try(FileReader fis = new FileReader("")){
            int data;
            while ((data = fis.read()) != -1) {
                sb.append((char) data);
            }
        }
        return sb.toString();
    }
```

## ✔️ 런타임 추가 기능 처리 ➡️ 메타 프로그래밍에 사용

## ✅ 사용자 정의 annotation 만들기

- 메타 어노테이션<br>
- 어노테이션 정의<br>
- 어노테이션 속성<br>
  어노테이션은 메소드가 없다!<br>

#### @Retention

소스 파일 ➡️ 컴파일 ➡️ 클래스 파일 ➡️ JVM ➡️ run<br>
annotation 유지 기간<br>
<br>

- source: 소스 파일에는 존재하고 클래스 파일에는 존재하지 않는다 <br>
- class: 클래스 파일에만 존재하고 실행시에는 사용 불가하다. <br>
  컴파일할 때 까지는 존재한다. <br>
  실제로 프로그램 돌아갈 때는 적용 안 됨 <br>
  기본값 <br>
- runtime: 클래스 파일에 존재하고, 실행시에도 존재합니다. <br>
  제일 긴 시간동안 존재 <br>

#### @Target

annotation 적용 대상 <br>
예를 들어 override는 메소드에만 적용 <br>
functionalInterface는 class에만 적용 <br>

#### @Documented

annotation이 javadoc에 나타나게 된다. <br>

```java
//MyAnnotation.java
//Annotation 어떻게 쓸지 정의한다.
@Retention(RetentionPolicy.RUNTIME) // runtime동안 annotation적용
@Target(ElementType.METHOD) //메소드에만 annotation적용
//@Target({ElementType.METHOD, ElementType.FIELD, ElementType.CONSTRUCTOR}) //메소드, 필드, 생성자에 annotation적용
//이런식으로 Target으로 annotation어디에 적용할지 결정할 수 있다.
@Documented
public @interface MyAnnotation {
    //annotation에서는 field적용할 때 (), default 붙인다.
    String name();
    int count() default 0;
}

//customer.java
public class Customer implements Serializable {
    //method에 MyAnnotation으로 설명해준다.
    @MyAnnotation(name= "똑같은가 확인")
    public boolean equals(Object obj) {
        if (obj == null) return false;
        if (obj instanceof Customer){
            Customer customer = (Customer) obj;
            return customer.customerID == this.customerID;
        }
        else {
            return false;
        }

    @MyAnnotation(name="가격 계산하기 메소드") //annotation으로 메소드 이름 정해주기
    //calculatePrice에 대한 설명을 MyAnnotation에 써준다.
    public int calculatePrice(int price){
        this.bonusPoint += price * bonusRatio;
        return price;
    }
    }
```

## ✅ 메타 프로그래밍

프로그램을 짠 코드를 데이터로 보고 프로그래밍을 하는 것<br>
메타 정보를 가지고 와서 프로그래밍에 적용하는 것<br>
<br>

- Java Custom Annotation <br>
  기본 외 직접 정의한 Annotation <br>
- Java Reflection & Class <br>
  런 타임 때, 해당 클래스 메소드와 변수에 접근 가능 <br>

## ☑️ Java Reflection, Class 클래스

Java Reflection으로 메타 데이터 가져오기 가능하다. <br>
<br>

클래스의 클래스를 정의 <br>
생성자를 타입으로 정의하고 `getConstructors()`로 메타데이터 얻기 가능 <br>
필드도 타임으로 정의하고 `getFields()`로 메타데이터 얻기 가능 <br>
메소드도 타임으로 정의하고 `getMethods()`로 메타데이터 얻기 가능 <br>
<br>
Reflection으로 함수 호출도 가능하다. <br>

```java
//annotation
@Retention(RetentionPolicy.RUNTIME) //실제 동작하는 동안에도 annotation 실행되어야 함
@Target(ElementType.METHOD) //메소드에 적용되는 annotation
public @interface Repeat {
    int value();
}

//MyClass.java
public class MyClass {
    @Repeat(value = 20)
    public void printMessage() {
        System.out.println("Hello, world!");
    }

    @Repeat(value = 10)
    public void foo() {
        System.out.println("This is another method.");
    }
}
//AnnotationTest.java
public class AnnotationTest {
    public static void main(String[] args) {
        MyClass myObj = new MyClass();
        AnnotationUtils.executeMethodsByRepeatAnnotation(myObj);
    }
}
//AnnotationUtils.java
public class AnnotationUtils {
    //Annotation정보를 가지고 메소드를 실행하는 메소드
    //모든 객체를 받을 수 있어 parameter이 object
    public static void executeMethodsByRepeatAnnotation(Object object) {
        //💡 메타 프로그래밍
        Class clazz = object.getClass();
        //메소드를 가져와서 배열에 저장
        Method[] methods = clazz.getDeclaredMethods();

        for (Method method : methods) {
            //메소드에 붙은 annotations 배열로 가져오기
            Annotation[] annotations = method.getDeclaredAnnotations();

            for (Annotation annotation : annotations) {
                //내가 가져온 annotation이 Repeat라는 annotation안에 있다면
                if (annotation instanceof Repeat) {
                    //value로 개수 세기
                    Repeat repeatAnnotation = (Repeat) annotation;
                    int repeatCount = repeatAnnotation.value();

                    for (int i = 0; i < repeatCount; i++) {
                        try {
                            //invoke하는 reflection 실행
                            method.invoke(object);
                        } catch (Exception e) {
                            e.printStackTrace();
                        }
                    }
                }
            }
        }
    }
}
```
