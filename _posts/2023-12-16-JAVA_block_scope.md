---
title: package
categories: [JAVA, JAVA_Basics]
tags: [package, accessmodifier, import] # TAG names should always be lowercase
---

## 클래스 안에서 패키지 정보 가져와 명시

```java
package sec06.chap02.pkg4;
```

패키지 구조를 설명함.
클래스 이름이 같더라도 다른 패키지 안에 들었으면 사용 가능

## access modifier

패키지에 따라서 access modifier 달라진다.
예를 들어 protected이면 같은 패키지 또는 상속 관계 안에서는 사용 가능.

## import

다른 패키지에서 가져온 클래스로부터도 상속받을 수 있다.
상단에 import하면 가능

```java
import sec06.chap02.pkg1.Parent; // pkg1안에 있는 Parent 클래스 가져오기
import sec06.chap02.pkg2.* //⭐️ 와일드카드 *: pkg2안에 있는 모든 클래스 가져오기
```

## 서로 다른 패키지 안에 있는 동명 클래스 불러올 경우

인스턴스 선언할 때 주의해야 함! 어디 패키지의 클래스인지 명시하기

```java
//현재 pkg1안에도 Child클래스 있고, pkg2안에도 Child클래스 있는 상황
//❌ 이렇게 하면 어떤 패키지의 Child인지 알 수가 없음
        Child child1 = new Child();
//  ⭐️ 패키지가 다른 동명의 클래스들을 불러올 경우
        sec06.chap02.pkg1.Child child1 = new sec06.chap02.pkg1.Child();
        sec06.chap02.pkg2.Child child2 = new sec06.chap02.pkg2.Child();

```
