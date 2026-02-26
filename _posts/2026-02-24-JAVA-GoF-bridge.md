---
title: Structural_Bridge
categories: [JAVA, GoF]
tags: [] # TAG names should always be lowercase
---

## ✅ Bridge

- decouple abstract and implementation
- bridge can connect abstract and concrete

## ✅ Structure

```
             bridge
Abstraction  ----->  Implementor
     |                   |
RefinedAbstraction   ConcreteImplementor
```

- client uses `Abstraction`
- `Implementor` will be interface
- `Abstraction` will have `Implementor` as attribute
- so, `Abstraction` is dependent on `Implementor`

## 👀 Remote controller and Device example

```
Abstraction(Remote)          ----->       Implementor(Device)
     |                                            |
RefinedAbstraction(RemoteController)   ConcreteImplementor(TV, Radio)
```

#### ✔️ **Implementation**: Device

- do not know anything about remote,
- do not know anything about abstraction

```java
public interface Device {
    void turnOn();
    void turnOff();
    void setVolume(int volume);
    boolean isEnabled();
}
```

#### ✔️ **ConcreteImplemention** : TV

```java
public class TV implements Device{
  //override the methods
}
```

#### ✔️ **Abstraction**: Remote

- `Remote` has `Device` as field
- 👉🏻 `Remote` is dependent on `Device`
- 👉🏻 `Abstraction` is dependent on `Implementation`
- 👉🏻 This is the bridge between `Abstraction` and `Implementation`

```java
public abstract class Remote {
    private Device device; //abstraction is dependent on implementation

    protected Remote(Device device) {
        this.device = device;
    }

    public abstract void power();
}
```

#### ✔️ **RefinedAbstraction**: BasicRemote

```java
public class BasicRemote extends Remote{

    public BasicRemote(Device device) {
        super(device);
    }

    @Override
    public void power() {
        if(device.isEnabled()){
            device.turnOff();
        }else{
            device.turnOn();
        }
    }
}
```

#### ✔️ Client code

```java
Device tv = new TV();
Remote basicRemote = new BasicRemote(tv);
basicRemote.power();
```

## 👍🏻

- can create as many `Abstraction(remote controller)` class without interrupting `Implementation`
- can create as many `Implementation(devices)` class without interrupting `Abstraction`

## 👀 MessageSender exmaple

[![image.png](https://i.postimg.cc/mZQCR9ZB/image.png)](https://postimg.cc/NLj5k5rz)

#### ✔️ **Implementation**: MessageSender

```java
public interface MessageSender {
    void sendMessage(String message);
}
```

#### ✔️ **ConcreteImplemention** : EmailSender, SMSSender

```java
public class EmailSender implements MessageSender{
    @Override
    public void sendMessage(String message) {
        System.out.println("Email");
    }
}

public class SMSSender implements MessageSender{
    @Override
    public void sendMessage(String message) {
        System.out.println("SMS");
    }
}
```

#### ✔️ **Abstraction**: Message

```java
public abstract class Message {
    private MessageSender messageSender; //bridge between abstract, implementation

    protected Message(MessageSender messageSender) {
        this.messageSender = messageSender;
    }

    public abstract void send(String message);
}
```

#### ✔️ **RefinedAbstraction**: TextMessage, EncryptedMessage

```java
public class TextMessage extends Message{
    protected TextMessage(MessageSender messageSender) {
        super(messageSender);
    }

    @Override
    public void send(String message) {
        System.out.println("text message");
    }
}

public class EncryptedMessage extends Message{
    protected EncryptedMessage(MessageSender messageSender) {
        super(messageSender);
    }

    @Override
    public void send(String message) {
        System.out.println("EncryptedMessage");
    }
}
```

#### ✔️ Client code

- `Abstraction` and `Implementation`을 이리저리 갈아끼울 수 있음

```java
public class App {
    public static void main(String[] args) {
        MessageSender email = new EmailSender();
        MessageSender sms = new SMSSender();

        Message textEmail = new TextMessage(email);
        Message encryptedEmail = new EncryptedMessage(email);
        Message textSMS = new TextMessage(sms);
        Message encryptedSMS = new EncryptedMessage(sms);
    }
}
```

## 👍🏻

- 👍🏻 decouple abstract and implementation
- can modify abstract code without modifying concrete implementation
- 👉🏻 open closed principle

## 🛠️

- `JDBC` allows you to use `driver(implemtation)`
- but change of driver will not change `code, database(abstract)`
