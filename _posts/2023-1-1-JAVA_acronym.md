---
title: Java Acyronyms
categories: [JAVA, JAVA_Basics]
tags: [acronyms] # TAG names should always be lowercase
---

## ✅ Security

| Acyronyms | Stands For                   |
| --------- | ---------------------------- |
| XXS       | Cross Site Scripting         |
| CSRF      | Cross Site Request Forgery   |
| SOP       | Same Orgin Policy            |
| CORS      | Cross Orgin Resource Sharing |
|           |                              |
|           |                              |

## ✅ Spring

| Acyronyms   | Stands For                                          |
| ----------- | --------------------------------------------------- |
| IOC         | Inversion of Control                                |
| AOP         | Aspect-Oriented Programming                         |
| OOP         | Object Oriented programming                         |
| ORM         | Object Relation Mapping                             |
| XML         | eXtensible Markup Language                          |
| PSA         | Portable Service Abstraction                        |
| Transaction | set of operations that must be executed as one unit |
| ACID        | Atomicity, Consistency, Isolation, Durability       |
| JPA         | Java Persistence API                                |
| JPQL        | Java Persistence Query Language                     |
| JWT         | JSON Web Token                                      |
| JDBC        | Java Database Connectivity                          |
| DI          | Dependency Injection                                |
| JSON        |                                                     |
| MVC         | Model - View - Controller                           |

- IOC: application controll flow of execution❌ framework manages the lifecycle of objects and their dependencies
- AOP: in traditional OOP, concers such as logging, security, transaction management tend to be spread in multiple classes. However, thanks to AOP in spring, we can put these simmilar mechanisms together to modularize and encapsulate. 여러개의 class에 비슷한 기능들이 계속 반복된다면, 그 기능들을 묶어서 따로 관리. 이로서 코드 재사용성⬆️ 중복 제거👍🏻
- ORM: JAVA와 SQL을 mapping한다. 어떻게? 🤷🏻‍♀️ hibernate, xml, 그리고 annotation(@Entity, @Table, @Column)
- PSA: abstraction, framework that provides various enterprise services in consistent platform-independent(unifed) manner. 💡 for example, JDBC. JDBC in spring provides consistent way to interact with RDBs, regardless of the specific database.
- Transaction: 데이터 베이스를 변화시키는데, 한 번에 일어나야하는 작업의 단위. 💡 예를 들어, A가 B에게 만원을 송금하면 A의 계좌에서는 만원이 인출되고, B의 계좌에는 만원이 입금되어 "송금"이라는 단위의 Transaction이 일어난 것이다.
  - Atomicity: all or none jobs should be committed 모두 반영되거나 전혀 반영되지 않거나.
  - Consistency: data should reflect the changes
  - Isolation: if two or more transactions happen at the same, time, transactions should be isolated from each other
  - Durability: once transaction is commited, the effects should be permanently recorded and recovered if in case of failiure.
  - Rollback: if there is an error during transaction, rollback to before transaction happened.

## ✅ NetWork

| Acyronyms | Stands For                  |
| --------- | --------------------------- |
| HTTP      | Hypertext Transfer Protocol |
|           |                             |
|           |                             |

## ✅ SQL

| Acyronyms | Stands For                |
| --------- | ------------------------- |
| SQL       | Structured Query Language |
|           |                           |
|           |                           |

## ✅ SQL

| Acyronyms | Stands For                          |
| --------- | ----------------------------------- |
| API       | Application Programming Protocol    |
| REST API  | Representational State Transfer API |
| MVC       | Model View Controller               |
|           |                                     |
|           |                                     |

---

| Acyronyms | Stands For |
| Cell 1,1 | Cell 1,2 |
| Cell 2,1 | Cell 2,2 |
| Cell 1,1 | Cell 1,2 |
| Cell 2,1 | Cell 2,2 |
| Cell 1,1 | Cell 1,2 |
| Cell 2,1 | Cell 2,2 |
| Cell 1,1 | Cell 1,2 |
| Cell 2,1 | Cell 2,2 |
| Cell 1,1 | Cell 1,2 |
| Cell 2,1 | Cell 2,2 |
| Cell 1,1 | Cell 1,2 |
| Cell 2,1 | Cell 2,2 |
| | |
| | |
