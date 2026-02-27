---
title: Behavioral_Command Pattern
categories: [JAVA, GoF]
tags: [] # TAG names should always be lowercase
---

## ✅ Command Pattern

- encapsulate the request
- decouple `invoker(호출자)` and `reciever(수신자)`
- 👍🏻 when request logic changes, `invoker` code will not change

## ✅ Diagram

[![Screenshot-2026-02-27-at-08-14-45.png](https://i.postimg.cc/qv9TWZy1/Screenshot-2026-02-27-at-08-14-45.png)](https://postimg.cc/yDXtZjfR)

## 👀 Command pattern example

#### ✔️ Invoker class

- the invoker does not know the logic behind the commands
- even if command changes, just have to `press` the button (`invoke`)
- and the changed logic will run
- without having to change `invoker` code

```java
//Invoker code will never change even if command changes
public class Button {
    private Command command;

    public Button(Command command) {
        this.command = command;
    }
    public void press(){
        command.execute();
    }

    // main class
    public static void main(String[] args) {
        Button button1 = new Button(new LightsOnCommand(new Light()));
        button1.press();

        Button button2 = new Button(new GameStartCommand(new Game()));
        button2.press();

    }
}
```

#### ✔️ Command interface

```java
public interface Command {
    void execute();
}
```

#### ✔️ concrte command interfaces

```java
public class LightsOnCommand implements Command{
    private Light light;

    public LightsOnCommand(Light light) {
        this.light = light;
    }

    @Override
    public void execute() {
        light.on();
    }
}

public class LightsOffCommand implements Command{
    private Light light;

    public LightsOffCommand(Light light) {
        this.light = light;
    }

    @Override
    public void execute() {
        light.off();
    }
}

public class GameStartCommand implements Command {
    private Game game;

    public GameStartCommand(Game game) {
        this.game = game;
    }

    @Override
    public void execute() {
        game.start();
    }
}

public class GameFinishCommand implements Command {
    private Game game;

    public GameFinishCommand(Game game) {
        this.game = game;
    }

    @Override
    public void execute() {
        game.start();
    }
}
```

#### ✔️ reciever classs

- has the specific logic to run
- when command is called

```java
public class Light {
    public void on(){
        //specific logic
    }
    public void off (){
        //specific logic
    }

}

public class Game {
    public void start(){
        //specific logic
    }
    public void finish(){
        //specific logic
    }
}
```

## ✅ Using stack with command pattern ➡️ undo

- can `stack` the commands
- and call on `undo`
- 실행취소 구현하기

```java
public class Button {
    private Stack<Command> commands = new Stack<>();

    public void press(Command command){
        command.execute();
        commands.push(command);
    }

    public void undo(){
        if(!commands.isEmpty()){
            Command command = commands.pop();
            command.undo();
        }
    }

    public static void main(String[] args) {
        Button button1 = new Button();
        button1.press(new LightsOnCommand(new Light()));
        Button button2 = new Button();
        button2.press(new GameStartCommand(new Game()));

        button1.undo();
        button2.undo();

    }
}
```

## 👍🏻👎🏻

- 👍🏻 can create new command without modifying invoker
- 👍🏻 even when command logic changes, invoker will not change
- 👉🏻 Open Closed principle

## 🛠️

- `Executor`: library to create thread to run asynchronized
- `Runnable`
- `SimpleJDBCInsert`

#### 1️⃣

#### 2️⃣

#### 3️⃣

#### 4️⃣

- 1️⃣
- 2️⃣
- 3️⃣
- 4️⃣
  👍🏻
  👎🏻

```
⭐️⭐️⭐️ EXAM ⭐️⭐️⭐️
❓
👉🏻
```
