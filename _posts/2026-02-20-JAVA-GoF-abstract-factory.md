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
- **Factory**: hide the creation of instance in concrete factory
- focus more on how to implement factory, interitance
- move instance creation process to concrte factory class
- 👉🏻 defines an interface for creating an object, but lets subclasses (or a factory class) decide which class to instantiate
- 🆚 create one product

- **AbstractFactory**: client does not have to see the concrete factory
- focus more on how to use factory, composition
- create related instances without relying on a concrete class
- 👉🏻 interface for creating **families of related objects** without specifying their concrete classes.
- 🆚 multiple related products

```
🆚 Factory
CarFactory → Mercedes or Kia

🆚 Abstract Factory
GUIFactory
   ├─ createButton()
   └─ createCheckbox()

WindowsFactory → WindowsButton + WindowsCheckbox
MacFactory → MacButton + MacCheckbox
```

## 👀

[![Screenshot-2026-03-08-at-10-04-04.png](https://i.postimg.cc/vZYtwqpZ/Screenshot-2026-03-08-at-10-04-04.png)](https://postimg.cc/3dqvgB8s)

#### ✔️ Abstract product Interface

```java
interface Button {
    //method that button can perform
    press();
}

interface Checkbox {
    tick();
}
```

#### ✔️ Concete products

```java
class WindowsButton implements Button {
    //override method
    press();
}

class MacButton implements Button {
    //override method
    press();
}

class WindowsCheckbox implements Checkbox {
    //override method
    tick();
}

class MacCheckbox implements Checkbox {
    //override method
    tick();
}
```

#### ✔️ Abstract Factory interface

```java
interface GUIFactory {
    Button createButton();
    Checkbox createCheckbox();
}
```

#### ✔️ Concete Factory

```java
class WindowsFactory implements GUIFactory {

    public Button createButton() {
        return new WindowsButton();
    }

    public Checkbox createCheckbox() {
        return new WindowsCheckbox();
    }
}

class MacFactory implements GUIFactory {

    public Button createButton() {
        return new MacButton();
    }

    public Checkbox createCheckbox() {
        return new MacCheckbox();
    }
}
```

#### ✔️ Client

```java
Button windowButton = new WindowsFactory().createButton();
Checkbox windowCheckbox = new WindowsFactory().createCheckbox();
```

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
