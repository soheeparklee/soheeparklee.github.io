---
title: Polymorphism
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

- ⭐️ `extends`
- ⭐️ method overriding

## ✅ Polymorphism: parent can become child

- `parent class`
- `child class extends parent class`
- 1️⃣ **Polymorphism**: parent **CAN** become child instance
- child CAN NOT become parent instance

```java
Parent parent = new Parent();
Parent parentChild = new Child(); //🟢 parent CAN become child instance = Polymorphism
Parent parentGrandson = new Grandson();

//Child child = new Parent(); //🔴 child CAN NOT become parent instance
```

- 2️⃣ can only call **its type** method
- creating `new Child()` instance will create both `child instance` and `parent instance`(as `child` extends `parent`)
- however as `parentChild` is `Parent` type, can only call `Parent` field and method

```java
Parent parentChild = new Child();
parentChild.parentMethod(); //parentChild is Parent type, can call parent method
//parentChild.childMethod(); // parentChild is Parent type, CAN NOT call child method
```

<img width="489" alt="Image" src="https://private-user-images.githubusercontent.com/97790983/437417095-69330a36-bffc-48cb-b0b3-7f84a45ce753.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDc4NjEyNzEsIm5iZiI6MTc0Nzg2MDk3MSwicGF0aCI6Ii85Nzc5MDk4My80Mzc0MTcwOTUtNjkzMzBhMzYtYmZmYy00OGNiLWIwYjMtN2Y4NGE0NWNlNzUzLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA1MjElMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwNTIxVDIwNTYxMVomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTBkYzI1YzQ0NmZhMTVmNThkMWI5YmQxOTJlYTcwNDUzNzc4ODcyM2NlNGY0NDliM2I5YTBiYTk2OWYxYWEyMzYmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.65hGJY4piiZV0kB8Azj2VL_mcM73YvDGnN3SSlj6TFo" />

- `new Child()`: 자식 클래스를 생성하면 `child class` ➕ `parent class` 둘 다 생성됨
- 그러나 `Parent parentChild` 이므로 `parentChild`는 `Parent` 타입이다
- 따라서 `parentChild`는 `Parent`의 `field, method`만 사용 가능하다

## ✅ Downcasting

- I am `parent type` in `child instance`, 👎🏻 so I can only call parent `field and methods`
- 🤨 But I want to call child `field and methods`

- ➡️ **Downcasting**: change `parent type` to `child type`
- CAN NOT omit `type`

```java
public class CastingMain1 {
    public static void main(String[] args) {
        Parent parentPoly = new Child(); // parentPoly is Parent type, but Child instance
        //parentPoly.childMethod(); // 🔴 compile error, 👎🏻 only can call type method

        Child childPoly = (Child) parentPoly; //💡 Downcasting //change parent type to child type
        childPoly.childMethod(); //now can call childMethod();
        //parentPoly type: parent
        //childPoly type: child
    }
}
```

- 🤨 why is downcasting possible?
  - `parent type` is created `child instance`,
  - in memory, both `parent instance` and `child instance` is created
  - thus, can change type from `parent type` to `child type`

```java
ublic class CastingMain3 {
    public static void main(String[] args) {
        Parent parent1 = new Child();
        Child child1 = (Child) parent1; //🟢downcasting

        Parent parent2 = new Parent();
        Child child2 = (Child) parent2; //🔴error, parent2 is parent instance thus downcasting not possible
    }
}
```

- `Parent parent1 = new Child();`를 생성하면 type은 `parent`이지만 `instance`가 `child`이므로 `parent instance`, `child instance`가 모두 생성된다
- 따라서 downcasting 가능 ⭕️
- 그러나 `Parent parent2 = new Parent();`하면 `instance`가 `parent`이므로 `parent instance`만 생성
- 따라서 downcasting 불가능 ❌

## ✅ Upcasting

- **Upcasting**: changing `child type` to `parent type`
- can omit `type`

```java
public class CastingMain2 {
    public static void main(String[] args) {
        Child child = new Child();
        Parent parent1 = (Parent) child; //upcasting
        Parent parent2 = child; //can omit (Parent)

        parent1.parentMethod();
    }
}
```

## Downcasting 🆚 Upcasting

- Downcasting: 부모 ➡️ 자식
- Upcasting: 자식 ➡️ 부모

- Upcasting은 자식 instance를 생성하므로 부모 instance도 모두 항상 생성됨, upcasting하는 `type`을 omit하고 사용 가능
- Downcasting은 부모 instance만 생성되므로 downcasting하는 `type`을 명시해주어야 한다

## ✅ InstanceOf

- what is my instance?
- can I downcast to this `instance`? check `instance`

```java
public class CastingMain5 {
    public static void main(String[] args) {
        Parent parentParent = new Parent();
        parentParent instanceOf Parent //true
        parentParent instanceOf Child //false, downcast NOT possible

        Parent parentChild = new Child();
        parentChild instanceOf Parent //true
        parentChild instanceOf Child //true, downcast possible

    }
}
```

## ✅ Polymorphism and overriding

- method: **overrided** method always has priority
- field: field is not overrided

```java
Parent poly = new Child();
poly.value //field: parent field, field is NOT override
poly.method(); //method: child method, method IS override
```

- `poly` type is `Parent`, instance is `Child`
- when **field** is called, go to `Parent` and find, return `Parent field`
- when **method** is called, look for **override**
- if there is override in child, return `Child method`

## ☑️ 결론

- 1️⃣ polymorphism: 부모 type을 자식 instance로 생성할 수 있다(부모는 자식을 품을 수 있음)
- 2️⃣ 자식 instance로 생성하면 자식, 부모 instance를 모두 생성한다
  - `Animal animal = new Dog();`하면 `animal`, `dog`인스턴스 모두 생성됨
- 3️⃣ Downcasting: 부모 ➡️ 자식으로 타입을 바꿈, 내가 명시한 instance일때만 그 type으로 downcast 가능
- 4️⃣ Upcasting: 자식 ➡️ 부모로 타입을 바꿈, 항상 가능
- 5️⃣ 내가 무슨 instance인지 확인하기 위해 `instanceOf`를 사용할 수 있다
- 6️⃣ overriding한 method가 항상 우선순위를 가진다(자식 인스턴스)
- method is override, field is not overrided
