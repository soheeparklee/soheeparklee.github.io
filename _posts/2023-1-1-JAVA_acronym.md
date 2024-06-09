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

| Num | Acyronyms   | Stands For                                          |
| --- | ----------- | --------------------------------------------------- |
| 1   | IOC         | Inversion of Control                                |
| 2   | OOP         | Object Oriented programming                         |
| 3   | AOP         | Aspect-Oriented Programming                         |
| 4   | ORM         | Object Relation Mapping                             |
| 5   | XML         | eXtensible Markup Language                          |
| 6   | PSA         | Portable Service Abstraction                        |
| 7   | Transaction | set of operations that must be executed as one unit |
| 8   | ACID        | Atomicity, Consistency, Isolation, Durability       |
| 9   | JPA         | Java Persistence API                                |
| 10  | JPQL        | Java Persistence Query Language                     |
| 11  | JWT         | JSON Web Token                                      |
| 12  | JDBC        | Java Database Connectivity                          |
| 13  | DI          | Dependency Injection                                |
| 14  | JSON        | JavaScript Object Notation                          |
| 15  | MVC         | Model - View - Controller                           |
| 16  | Jasypt      | Json Simplified Encryption                          |
| 17  | POJO        | Plain Old Java Object                               |

1. IOC: application controll flow of execution❌ framework manages the lifecycle of objects and their dependencies
2. OOP: programming of class(field+method) and object(instance of class).
   ✔️ Encapsulation: bundle field+method into a single class <br>
   ✔️ Abstraction<br>
   ✔️ Inheritence<br>
   ✔️ Polymorphism<br>

3. Aspect: Module that encapsulated cross-cutting concern(logging, security, transaction)
4. AOP: in traditional OOP, concers such as logging, security, transaction management tend to be spread in multiple classes. However, thanks to AOP in spring, we can put these simmilar mechanisms together to modularize and encapsulate. 👍🏻 Thus, AOP allows the seperation of cross-cutting concers from business logics.
   여러개의 class에 비슷한 기능들이 계속 반복된다면, 그 기능들을 묶어서 따로 관리.
   이로서 코드 재사용성⬆️ 중복 제거👍🏻
5. ORM: JAVA와 SQL을 mapping한다. 어떻게? 🤷🏻‍♀️ hibernate, xml, 그리고 annotation(@Entity, @Table, @Column)
6. XML: markup language, both human and machine readable. Used for data interexchange between systems and platforms.

- `pom.xml` is used for Maven-based Java projects

6. 12. PSA: abstraction, framework that provides various enterprise services in consistent platform-independent(unifed) manner. 💡 for example, JDBC. JDBC in spring provides consistent way to interact with RDBs, regardless of the specific database.
7. Transaction: 데이터 베이스를 변화시키는데, 한 번에 일어나야하는 작업의 단위. 💡 예를 들어, A가 B에게 만원을 송금하면 A의 계좌에서는 만원이 인출되고, B의 계좌에는 만원이 입금되어 "송금"이라는 단위의 Transaction이 일어난 것이다.

✔️ Atomicity: all or none jobs should be committed 모두 반영되거나 전혀 반영되지 않거나. <br>
✔️ Consistency: data should reflect the changes <br>
✔️ Isolation: if two or more transactions happen at the same, time, transactions should be isolated from each other <br>
✔️ Durability: once transaction is commited, the effects should be permanently recorded and recovered if in case of failiure. <br>
✔️ Rollback: if there is an error during transaction, rollback to before transaction happened.<br>

9. JPA(Persistence): ability to store and retrieve entities from a relatoinal database.

✔️ ORM <br>
✔️ Entity <br>
✔️ Transaction <br>
✔️ Query Language <br>
✔️ Data Access Layer <br>

14. JSON: lightweight data interchage format for transmitting data between web server and client. human readable and machine readable. Based on javaScript, but it is language independent.
15. POJO: simepl Java object that does not extend nor implement any specialized classes or interfaces. 💡 for example, domain objects, DTOs, entities

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
| API       | Application Programming Interface   |
| REST API  | Representational State Transfer API |
|           |                                     |
|           |                                     |
|           |                                     |

- API: set of classes, interfaces, methods provided by library or framework so developers can use the functions without needing to understand its implementation details. APIs define how software components should interact, enabling devleopers to use pre-defied functions and structures to build applications.
- REST API: architectural style for building web services that allow client-server communication over HTTP in a stateless manner

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
