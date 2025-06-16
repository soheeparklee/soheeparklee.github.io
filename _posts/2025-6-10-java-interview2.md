---
title: Interview_literal/StringBuilder/Exception/Generic/lambda, stream/Functional programming/Functional Interface/Annotation
categories: [JAVA, JAVA_Basics]
tags: [] # TAG names should always be lowercase
---

## ✅ String literal과 new String("")의 차이

- `String literal`: saved in **constant pool**
- `new String("")`: saved in memory **heap**

- `constant pool`에 저장되면 동일한 문자열에 대해서는 하나의 참조를 재사용
- `constant pool`에서는 같은 값이 존재한다면, 새로 정의한 변수여도 같은 주소값을 가진다

## ✅ What is literal?

- fixed, constant value
- `int PI = 3.14; `
- `String greeting = "Hello, world!";`

## String 🆚 StringBuilder 🆚 StringBuffer

- String: immutable
- StringBuilder: mutable(same memory), single thread
- StringBuffer: mutable(same memory), multithread safe

## Exception 🆚 Error

- markdown

[Screenshot-2025-06-16-at-22-27-07.png](https://postimg.cc/CRZSQWQB)

- git markdown

[![Screenshot-2025-06-16-at-22-27-07.png](https://i.postimg.cc/Dw608hQg/Screenshot-2025-06-16-at-22-27-07.png)](https://postimg.cc/CRZSQWQB)

- homepage?

<a href='https://postimg.cc/CRZSQWQB' target='_blank'><img src='https://i.postimg.cc/Dw608hQg/Screenshot-2025-06-16-at-22-27-07.png' border='0' alt='Screenshot-2025-06-16-at-22-27-07'/></a>

<img width="946" alt="Image" src="https://github.com/user-attachments/assets/5854c6b0-6b59-43d7-bcdb-9140ac64a349" />

<img width="910" alt="Image" src="https://private-user-images.githubusercontent.com/97790983/454097085-6e4a1cfd-0e1a-43c4-996a-3b2530018bdd.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDk2NzQ3MjEsIm5iZiI6MTc0OTY3NDQyMSwicGF0aCI6Ii85Nzc5MDk4My80NTQwOTcwODUtNmU0YTFjZmQtMGUxYS00M2M0LTk5NmEtM2IyNTMwMDE4YmRkLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA2MTElMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwNjExVDIwNDAyMVomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTQ5MTdjZDIxODY0NjgyNjMyNTE4YzRkMjBhOWYyMmQzZWMwODc3MDllNmMzYTNmZDQxMmNjODZhMjg3NWRmZGUmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.p-RHXabBXE10i11MuxSDWoSnY35cfZPCaGitjNCd9VQ" />

- **Exception**: event that disrupts flow, usually recoverable
  - **checked exception**: exception in compile time, handled with `try-catch` or `throws`, `IO exception`, `SQL exception`
  - **unchecked exception**: exception in runtime, `NPE`, `IAE`
- **Error**: _system level_ failure, usually not recoverable
  - `Out of Memory`, `JVM crash`

## ✅ Exception 클래스의 예시

- `IO exception`: checked exception
- `SQL exception`: checked exception
- `Null Pointer Exception`: unchecked runtime exception
- `Illegal Argument Exception`: unchecked runtime exception, divide by 0

## Checked Exception 🆚 Unchecked Exception

- **Checked Exception**: exception in compile time, `"You must deal with me, or your code won’t compile."`, thus, `try-catch or throws`
- **Unchecked Exception**: exception in runtime, ` "You can deal with me, but I won’t force you — until I crash your app."`

## throw 🆚 throws

- `throw`: throw exception

```java
public void checkAge(int age) {
    if (age < 18) {
        throw new IllegalArgumentException("Age must be 18 or older.");
    }
}
```

- `throws`: declare exception in method declaration

```java
public void myMethod() throws IOException, SQLException {
    // method code
}
```

## ✅ try-catch-finally 구문에서 finally의 역할

- `try`: code that might throw exception
- `catch`: what to do when exception occurs
- `finally`: code that must be run regardless of exception

- `finally`: after `IO`, return DB connectoin pool regardless of exception

## Throwable 🆚 Exception의 차이

- `Throwable`: super class of both `Exception` and `Error`
- `Exception`: child class of `Throwable`, a problem developer can fix

## ✅ 제네릭(Generic)이란 무엇이고, 왜 사용할까요?

- create class, interface, methods that operate on `typed parameter`
- postpone the decision of instance type until we use the type
- decide type from **outside** class
- 👍🏻 type safe at compile time
- 👍🏻 write one class/method that works with many types

```java
List<String> stringList = new ArrayList<>();
List<Integer> integerList = new ArrayList<>();

👍🏻 only need to create one List, ArrayList class
- can create ArrayList with both String and Integer
```

## ✅ What is Lambda?

- an anonymous method(method without name) written in one line
- omit return, method name
- `(parameters) -> expression`

```java
User user = userRepository.getByUserId(userId)
    .orElseThrow(() -> new UserNotFoundException());
```

## ✅ What is functional programming(함수형)?

- focus on function, data flow
- focus on immutable
- in Java, `lambda`, `Stream API` (`map()`, `filter()`)

- 🆚 OOP
- focus more on Object and how they interact
- focus on mutable
- inheritence, polymorphism, abstract, encapsulation

## ✅ What is functional interface?

- interface that has exactly one abstract method
- `functional interface` is designed to be used with lambda expressions
- 자바가 자주 사용할 것 같은 lambda 함수 형태를 함수형 인터페이스로 만들어 제공해준 것

```java
@FunctionalInterface //add annotation, limit to one abstract method
public interface Consumer<T> {
    void accept(T t); //only one abstract method
}
```

```java
Consumer<String> printer = s -> System.out.println("Hello " + s); //use functional interface
printer.accept("Java"); // Output: Hello Java
```

- also can use `functional interface` with `List`, `Map`

```java
public static void main(String[] args) {
    List<Integer> list = Arrays.asList(1, 2, 3, 4, 5);

     //replace all: method provided by functional interface
    // 각 요소에 10을 곱함
    list.replaceAll( (x) -> x * 10 );

     //forEach: method provided by functional interface
    list.forEach( (x) -> System.out.println(x) );
}
```

## ✅ What is Stream?

- API to efficiently process data in `Collections`, like `Array` or `List`
- operate on data, and produce results in pipeline

```java
List<String> names = userRepository.findByName();

List<String> result = names
    .stream() //create stream
    .filter(name -> name.startsWith("A")) //intermediate operations
    .map(String::toUpperCase) //intermediate operations
    .collect(Collectors.toList()); //terminal operations
```

## ✅ 람다와 스트림은 왜 생겨났을까요?

- to support `functional programming` in Java
- example of `functional programming` in Java is `lambda` and `Stream API`

## ✅ 어노테이션이란?

- **metadata** to add to class, method, variable, parameters...
- `@Override`
- `@Autowired`: inject dependency into class automatically
- `@Controller`: tell Spring MVC controller to handle web requests
- `@RestController`: `@Controller` + `@ResponseBody`, so return `JSON` or `XML`
- `@GetMapping`, `@RequestMapping`, `@PostMapping`: map HTTP methods
- `@Service`: this class is business logic service class
- `@Repository`: this class is `DAO(Data Access Object)` and interacts with interface
- `@Component`
- `@Value`: inject value from `application.yaml`
- `@RequestParam`: extract query parameter from request URL
- `@PathVariable`: extract variable from URL

## ✅ 어노테이션 사용 이유

- compiler uses `annotation` for checks, like missing `@Override`
- metadata for tools, `@Autowired` for dependency injection
- clean code, other developers can know `@Repository`, `@Controller`

## ✅ 리플렉션이란

- inspect and manipulate classes/members at runtime
- 구체적인 클래스 타입을 몰라도 그 클래스의 method, variable에 접근할 수 있게 해준다
- can access private field, methods
- can create objects dynamically
- ⚠️ can break encapsulation

## ✅ System.out.println 클래스는 성능이 좋지 않다고 하는데 이유?

- lock can occur in `blocking I/O` and `multithreading`
- `println` is `synchronized lock`

## ✅

## ✅
