---
title: Structural_Flyweight
categories: [JAVA, GoF]
tags: [] # TAG names should always be lowercase
---

## ✅ Flyweight

- 👍🏻 memory optimization, efficiency
- minimize memory usage by **sharing** common object data
- if object is same, do not duplicate ❌
- 똑같은 object이면 또 만들지 말고(메모리 낭비), 공유하자

- What is a common object?
- Object with all same fields

- 🛠️ Use when you have to use identical objects here and there
- 🆚 **singleton**: 목적 - guarantee exactly only one instance of a class in the whole application
- flyweight: 목적 - share many reusable objects, to reduce memory usage

## ✅ Structure and Diagram

[![Screenshot-2026-03-06-at-19-27-14.png](https://i.postimg.cc/kGbzvSh4/Screenshot-2026-03-06-at-19-27-14.png)](https://postimg.cc/gLGgYxpF)

- 👎🏻 before

```
1,000,000 objects
each containing identical data
```

- 👍🏻 after

```
1 shared object + lightweight references
```

## 👀

#### 1. Flyweight class

```java
// Flyweight class
class Book {

    private final String title; // intrinsic state (shared)
    // title will not be changed

    public Book(String title) {
        this.title = title;
    }

    public void read() {
        System.out.println("Reading the book titled: " + title);
    }
}
```

#### 2. Flyweight Factory

```java

// FlyweightFactory class
class Bookshelf {
    //need map to check if same book exists by title
    private static final Map<String, Book> bookshelf = new HashMap<>();

    public static Book getBook(String title) {
        Book book = bookshelf.get(title);

        //check if book with same title exists
        if (book == null) { //if not exists
            book = new Book(title);  //create new book
            bookshelf.put(title, book);
            System.out.println(
                "Adding a new book to the bookshelf: " + title);
        } else {
            System.out.println( //if exsits, use the existring book
                "Reusing existing book from the bookshelf: " + title);
        }
        return book;
    }
}
```

#### Client

```java
// Client code
public class Main {
    public static void main(String[] args) {
        Book book1 = Bookshelf.getBook("Effective Java");
        book1.read();

        Book book2 = Bookshelf.getBook("Effective Java"); //same book
        book2.read();

        Book book3 = Bookshelf.getBook("Clean Code"); //different book
        book3.read();

        // Check if book1 and book2 are the same object
        // book 2 was not created, as the book with same title exists
        System.out.println(
            book1 == book2 ? "Same book for 'Effective Java'."
            : "Different books for 'Effective Java'."
        );
    }
}
```

## 🛠️

- when you have to use the same instance several times
- in different places
