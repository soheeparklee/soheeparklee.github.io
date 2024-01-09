---
title: Framework 🆚 Library
categories: [WEB, WebBasics]
tags: [library, framework]
---

### **Framework VS Library**

#### ☑️ Framework

> 클래스 + 인터페이스의 집합

framework is already **fixed** how to use  
애플리케이션 코드가 프레임워크에 의해 사용, 결정된다.  
프레임워크에 따라 사용자가 그 안에 필요한 코드 작성

- 앱/서버 구동
- 메모리 관리
- 이벤트 루프
- 소프트웨어의 설계, 구현을 재구성이 가능하게 하는 인터페이스

💡 Example of Framework

- **Spring** for JAVA
- **Django** for Python
- **Android** for android app

#### ☑️ Library

> 라이브러리는 개발에 필요한 것들을 미리 구현해 놓은 도구이다.  
> 재사용이 가능하도록 기능을 미리 구현해놓고 필요한 곳에서 호출해 사용한다.

프레임워크와는 다르게, 사용자가 라이브러리를 사용해 애플리케이션 흐름을 직접 제어

- 미리 작성된 코드
- 함수
- 클래스 등

💡 Example of Library

- Python pip로 설치한 패키지/모듈 (tensorflow, pandas, beautifulsoup 등등)
- C++의 표준 템플릿 라이브러리 (STL)
- Node.js에서 npm으로 설치한 모듈
- HTML의 클라이언트 사이드 조작을 단순화하는 JQuery
- 웹에서 사용자 인터페이스 개발에 사용되는 React.js

#### ☑️ IOC 제어의 역전

> Inversion of Control
> 프레임워크와 라이브러리의 차이는 **제어흐름**이 어디에 있는가이다.  
> Who has the **flow** of the application?

- 어떤 일을 하도록 만들어진 `framework`에 의해 `control`권한을 위임하는 것
- 프레임워크에게 **제어의 흐름**을 넘겨서 개발자가 코드를 편하게 작성

- When you use a library, you are in charge of the flow of the application. You are choosing when and where to call the library.
- When you use a framework, the framework is in charge of the flow. It provides some places for you to plug in your code, but it calls the code you plugged in as needed.

`framework`는 `library`를 포함한다!
`프레임워크` 위에 사용자가 코드를 입력하다가 필요할 떄 `라이브러리`를 호출!
