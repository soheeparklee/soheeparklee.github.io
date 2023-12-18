---
title: Object
categories: [JAVA, JAVA_Basics]
tags: [object] # TAG names should always be lowercase
---

## ✅ Java.lang 패키지

Java.lang안에 이런 클래스들이 내장되어 있다.

- Object Class
- System: `System.out.println()`
- String
- Wrapper: 기본 타입의 데이터를 갖는 객체 만들 때 사용
- Math

우리가 가져오지 않아도 자동으로 가져와져서 쓰여짐

## ✅ 최상위 클래스 Object

모든 클래스의 상위 클래스

```java
public class Animal extends Object
//사실은 우리도 모르게 모든 class는 Object를 상속함
//extends Object뒤에 붙여져 있음, 생략되어 있지만~

//당연히 upcasting도 가능함
Animal animal1 = new Animal("cat");
Object animal2 = new Animal("dog");
```

## ✅ Object method

<img width="1130" alt="스크린샷 2023-12-18 오후 10 42 25" src="https://github.com/soheeparklee/sc_project_carrotMkt_improved/assets/97790983/a77d2636-5b96-4f0a-b0ea-754027bfb5f0">

### 💡 `toString()`

객체 정보를 문자열로 바꾸어 준다.
사실 `println`, `printf`모두 `toString()`을 호출하는 메소드이다.
원래는 `getClass().getName() + '@' + Integer.toHexString(hashCode())` 반환하는데
`toString()`쓰면 string으로 변환해서 반환

#### 📍 Object의 `toString()` 메소드를 자식 클래스에서 오버라이딩 하기

```java
//toString() override하기 전
Customer customer= new Customer("So Hee");
System.out.println(customer) //exercise.chapter_43.Customer@67b64c45

//toString() override
//customer class
@Override
public String toString(){
  return String.format("Customer name: %s", this.name);
}
//Main.java
System.out.println(customer) //Customer name: So Hee
```

### 💡 `equals()`'

두 인스턴스가 같은 객체인지 판단한다.
두 인스턴스의 Heap 주소 값을 비교하여 Boolean 값을 리턴
같은 메모리값을 가리키고 있는가?

```java
Customer customer1= new Customer(123, "So Hee");
Customer customer2= customer1;
Customer customer3= new Customer(123, "So Hee");

customer1.equals(cusotmer2); //true
customer1.equals(customer3); //false
//customer 1,3 은 field는 같을지몰라도 저장된 공간은 다르니까
```

#### 📍 Object의 `equals()` 메소드를 자식 클래스에서 오버라이딩 하기

그래서 customer 1과 customer3 도 같게 만들겠다!
컴퓨터 입장에서는 다를지도 모르지만, 사람 입장에서는 아이디 같으면 같은 사람이니까

```java
//equals() override
//parameter로 받은 Obj가 비교하는 obj랑 같은지 보고 싶다.
@Override
public boolean equals(Object obj){
  //일단 obj가 null은 아니어야될거아니야
  if(obj==null){ return false; }
  //downcast-instanceof
  if(obj instanceof Customer){
    Customer customer= (Customer) obj;
    return customer.customerID == this.customerID
  }
  return false;
}

//Main.java
//이제 id가 같으면 같은 사람으로 판단, heap 메모리 주소는 다르더라도
customer1.equals(custotmer2); //true
customer1.equals(customer3); //true
```

#### ==

메모리 주소를 기준으로 boolean값 반환
`equals()` override해서 ID가 같으면 같은 사람 취급하라고 해도 말 안 들음
==과 `equals()`는 상관 없이 실행됨.
==은 항상 메모리값이 기준

```java
customer1 == customer2; //true
customer1 == customer3; // false
```

### 💡 `hashCode()`

객체의 해시 코드 반환
우리가 원하는 값의 해시 코드로 override할 수 있음

### 💡 `clone()`

자신과 같은 객체 복제
override해서 자신을 복제할 떄 이런 값은 복제하고 이런 값은 복제 안하고~
