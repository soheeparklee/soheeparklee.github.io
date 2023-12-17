---
title: Class_Access Modifier_⭐️encapsulation
categories: [JAVA, JAVA_Basics]
tags: [accessmodifier, private, protected, default, public] # TAG names should always be lowercase
---

## ✅ access modifier 접근 제어자, 정보 은닉화

필드 앞에 붙여 이 데이터에 대한 접근성을 제한한다.<br>
이로써 정보를 감추기도 한다. ➡️ 정보 은닉화<br>
메소드 앞에는 붙이지 않는다.<br>

### ⭐️ 캡슐화 encapsulation

- 사용자가 굳이? 볼 필요 없는 부분들을 감싸서 더 편리하게 사용할 수 있게 하기 위함<br>

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

해당 클래스 안에서 접근 가능 <br>
