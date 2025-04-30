---
title: Immutable
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ Summary

- Immutable: cannot change reference value
- 1️⃣ `final field`, 2️⃣ no setter

## ✅ Primitive 🆚 Reference

- 🆚 **Primitive**

```java
int a = 10;
int b = a;

b = 20;
```

- ❓ 이제 a의 값은? 여전히 10
- ❓ 이제 b의 값은? 20
- b만 바꿨으니 a의 값은 바뀌지 않음

- `int a` and `int b` are primitive type
- primitive values **DO NOT** share memory

- 🆚 **Reference**

```java
Address addressA  = new Address("seoul");
Address addressB  = addressA;

addressB.setValue("busan");
```

- ❓ 이제 addressA의 값은? seoul
- ❓ 이제 addressB의 값은? seoul
- b만 바꿨지만 a의 값도 바뀜

- `addressA` and `addressB` are reference type
- they both reference(point) to the SAME memory

<img width="522" alt="Image" src="https://github.com/user-attachments/assets/0005b2c2-5222-4cc3-aa5e-f29aa6458aaf" />

## ✅ Side effect of reference

- I only want to change `addressB`
- however, end up changing all `reference values`

- 👎🏻 change `addressB`, but change `addressA` as well!

```java
Address addressA  = new Address("seoul");
Address addressB  = addressA;

addressB.setValue("busan"); //👎🏻 this will change both A and B
```

- 💊 immutable

## ✅ Immutable

- `reference value`의 복사를 막을수는 없다
- 🔐 복사한 `reference value`는 값을 바꿀 수 없게 락을 걸어버리자

- 💡 **how to make immutable class**
- `final field`
- no setter

```java
//👎🏻 before, not immutable
public class Address {
    private String value; //👎🏻 not final

    public void setValue(String value) { //👎🏻 setter
        this.value = value;
    }
}

//👍🏻 after, immutable
public class ImmutableAddress {
    private final String value; //1️⃣ final
    //2️⃣ no setter
}
```

- ✔️ result

```java
public static void main(String[] args) {
    Address addressA  = new Address("seoul");
    Address addressB  = addressA;
    addressB.setValue("busan"); //👎🏻 this will make both A, B change

    ImmutableAddress immutableAddresssA = newImmutableAddress("seoul");
    ImmutableAddress immutableAddresssB =immutableAddresssA;

    // 👍🏻 address value is final, cannot change
    // 👍🏻 no setter, cannot change
    immutableAddresssB = new ImmutableAddress("busan");
    }
    //if want to change AddresssB, have to create a new instance
```

## ✅ How to change immutable

- need to **create** a `new instance`, change value, and return the `new instance`
- `old instance` will remain unchanged

- ✔️ Immutable obj class

```java
public class ImmutableObj {
    private final int value; //1️⃣ final

    public ImmutableObj(int value) {
        this.value = value;
    }

    //2️⃣ no setter

    public ImmutableObj add(int addValue){ //return new instance
        int result = value + addValue;
        return new ImmutableObj(result);
        //do not change this instance value
        //create a new instance to return the new value
    }
}
```

- ✔️ Main class using method `add()`

```java
public class ImmutableMain {
    public static void main(String[] args) {
        ImmutableObj immutableObj = new ImmutableObj(10);
        //create new instance
        ImmutableObj newImmutableObj = immutableObj.add(20); //method add()

        System.out.println(immutableObj.getValue()); //10
        System.out.println(newImmutableObj.getValue()); //30
    }
}
```

- old instance `immutableObj` did not change
- created new instance `newImmutableObj` and returned new value

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅
