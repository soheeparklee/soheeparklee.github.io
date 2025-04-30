---
title: String
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ String is reference

- String is reference value
- can create String as `literal` or as `instance`

```java
String str1= "hello";  //literal
String str2 = new String("hello"); //instance
```

- 🟰 two code is same

## ✅ String and equals()

- `==`: compare memory
- `equals()`: compare value
- for comparing `String`, use `equals()`

- ✔️ String as `instance`

```java
public static void main(String[] args) {
    String str1 = new String("hello");
    String str2 = new String("hello");

    System.out.println(str1 == str2); //false, different memory
    System.out.println(str1.equals(str2)); //true
}
```

- `==`: false
- `equals()`: true

- ❗️ String as `literal`

```java
public static void main(String[] args) {
    String str1 = "hello";
    String str2 = "hello";

    System.out.println(str1 == str2); //true
    System.out.println(str1.equals(str2)); //true
}
```

- `==`: true
- `equals()`: true

- if String is `literal`, Java tries to use memory efficiently
- Java has `String Pool` saved in `heap`
- if same `literal` exists in `String Pool`, **does not create again**
- thus, `str1`, `str2` has **SAME** memory value
- 👍🏻 save memory for same string literal value

## ✅ String is immutable

- once `String` value is set, **CAN NOT** change
- immutable
- if want to change, **CREATE NEW STRING**

```java
//⭐️ String is immutable
String str = "hello";
str.concat("Java"); //try to add "Java"
System.out.println(str); //return hello, does not change

//⭐️ If want to change immutable string, create new String instance
String newStr = str.concat("Java");  //add "Java"
System.out.println(newStr); //return helloJava
```

## ✅ Stringbuilder

- used to change `String` without creating new string instance
- NOT immutable

- 👎🏻 String is immutable side effect
- 👎🏻 everytime you want to change `String`, need to create `a new string instance`

```java
String str = "A" + "B" + "C" + "D"
//to do this need to create A, AB, ABC, ABCD
// 👎🏻 do not need A, AB, ABC
```

- 👎🏻 not efficient memory use
- 💊 string builder

<br>

- ✔️ `StringBuilder` is **NOT immutable**
- can change **without** creating new `String instance`
- 👍🏻 `String`을 자주 바꿀거라면 `String Builder`을 사용하는게 더 효과적

```java
StringBuilder sb = new StringBuilder();
sb.append("A");
sb.append("B");
sb.append("C");
sb.append("D");  //ABCD

sb.insert(4, "Java"); //ABCDJava

sb.delete(4, 8); //ABCD

sb.reverse(); //DCBA

String result = sb.toString() //이제 더 안 바꿀꺼면 toString으로 string으로 바꾸기
```

- ✔️ When is `StringBuilder` used?
- loops
- changing a long `String` many many times

- 🆚 StringBuffer: synchronization, in multi-thread, but slower
- StringBuilder: can run at same time, might have problems in multi-thread, but faster

## ✅ StringBuilder and Method Chaining

- ✔️ **Method Chaining**
- chain methods into one line

```java
ValueAdder adder = new ValueAdder();
adder.add(1);
adder.add(2);
adder.add(3);
int result = adder.getValue();

//method chaining
ValueAdder adder = new ValueAdder();
int result = adder.add(1).add(2).add(3).getValue();
```

- ✔️ **StringBuilder supports method chaining**

```java
StringBuilder sb = new StringBuilder();
sb.append("A");
sb.append("B");
sb.append("C");
sb.append("D");

//method chaining
sb.append("A").append("B").append("C").append("D");
```

## ✅

## ✅

## ✅

## ✅

## ✅
