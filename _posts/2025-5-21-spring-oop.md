---
title: SOLID
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## ✅ What is a good OOP

- SRP
- OCP
- LSP

## ☑️ Single Responsible principle

- one class should have one responsibility
- when extended, modification should be minimized
- ex) `MVC`: model, view, controller code is distinguished
- ex) `controller`, `service`, `repository`

## ☑️ Open Closed principle

- open for extension, closed for modification
- should be able to add `Fish`, without changing `Animal`, `Dog` class
- use polymorphism, interface

<!-- ```java
public class MemberService{
    //MemberRepository repo = new JDBCMemberRepository();
    MemberRepository repo = new JPAMemberRepository();
}
``` -->

## ☑️ Liskov Substitution principle

- correctly use inheritence without breaking the program
- Objects of a superclass should be **replaceable** with objects of its subclass

- If `Bird superclass` has `fly()` method
- `Penguin extends Bird` should override `fly()` and penguin should be able to fly ➡️ bad LSP
- thus, create `Bird superclass` and `Flyable interface` with `fly()`
- `Penguin extends Bird` only
- `Parrot extends Bird implements Flyable`

## ☑️

## ☑️

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅
