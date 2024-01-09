---
title: Class_Access Modifier<encapsulation>
categories: [JAVA, JAVA_Basics]
tags: [accessmodifier, private, protected, default, public, final] # TAG names should always be lowercase
---

## ✅ access modifier 접근 제어자, 정보 은닉화

필드 앞에 붙여 이 데이터에 대한 접근성을 제한한다.<br>
이로써 정보를 감추기도 한다. ➡️ 정보 은닉화<br>
메소드 앞에는 붙이지 않는다.<br>

## ⭐️ 캡슐화 encapsulation

- 사용자가 굳이? 볼 필요 없는 부분들을 감싸서 더 편리하게 사용할 수 있게 하기 위함<br>
- 클래스에 선언된 데이터를 보호하기 위해서 🟰 encapsulation<br>

#### ✔️ `public`

**다른 패키지에서도 접근 가능**
동일 패키지 또는 자손 클래스 안에서 접근 가능<br>
동일 패키지 안에서 접근 가능<br>
해당 클래스 안에서 접근 가능<br>

#### ✔️ `protected`

**동일 패키지 또는 자손 클래스 안에서 접근 가능**
동일 패키지 안에서 접근 가능<br>
해당 클래스 안에서 접근 가능<br>

#### ✔️ `default`

**동일 패키지 안에서 접근 가능**
해당 클래스 안에서 접근 가능<br>

#### ✔️ `private`

해당 **클래스** 안에서 접근 가능 <br>

#### ✔️ `final`

값을 변경할 수 없는 상수가 된다. <br>
오버라이딩 ❌<br>
클래스에 사용되면 자신을 확장하는 자식 클래스 정의 ❌<br>

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
