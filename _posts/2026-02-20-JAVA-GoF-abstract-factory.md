---
title: Creational_Abstract Factory
categories: [JAVA, GoF]
tags: [] # TAG names should always be lowercase
---

## ✅ Abstract Factory

- similar to factory,
- but with a focus on the client
- add `client` to factory pattern

- interface creates the related classes instance
- 👍🏻 can hide which `concrete product` to the client

## ✅ Diagram

[![Abstract-factory-UML.jpg](https://i.postimg.cc/wBtn8Zmp/Abstract-factory-UML.jpg)](https://postimg.cc/CZgcbv7P)

## 👀 ShipFactory example

[![Screenshot-2026-02-28-at-09-08-34.png](https://i.postimg.cc/sg7LD72m/Screenshot-2026-02-28-at-09-08-34.png)](https://postimg.cc/4Y4PWKVH)

## Factory 🆚 AbstractFactory

- 공통점: make creation of instance abstract with instance
- Factory: hide the creation of instance in concrete factory
- focus more on how to implement factory, interitance
- move instance creation process to concrte factory class
- 👉🏻 defines an interface for creating an object, but lets subclasses (or a factory class) decide which class to instantiate
- AbstractFactory: client does not have to see the concrete factory
- foducs more on how to use factory, composition
- create related instances without relying on a concrete class
- 👉🏻 interface for creating **families of related objects** without specifying their concrete classes.

## 🛠️

- in `javax.xml.parsers`
- `DocumentBuilderFatory` to create xml

```java
public static void main(String[[ args) throws ParserConfigurationException, IOException, SAXException{
  DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
  DocumentBuilder builder = factory.newDocumentBuilder();
  Document document = builder.parse(new File("src/main/resource/config.xml"));
  System.out.println(document.getDocumentElement());
}
```

- `FactoryBean<T>`
