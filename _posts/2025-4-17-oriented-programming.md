---
title: Object oriented, Procedural Oridented
categories: [JAVA, 김영한]
tags: [] # TAG names should always be lowercase
---

## Procedural Oridented 🆚 Object oriented

- Procedural Oridented: 순서 중요, how, **메소드 분리**
- Object oriented: 객체, what, 객체안에 **메소드 포함**

## ✅ example of procedural programming

- example of Music Player
  <br>

- music player class

```java
public class MusicPlayerData {
    int volume;
    boolean isOn;
}
```

- class with method

```java
public class MusicPlayerMain {
    public static void main(String[] args) {
        MusicPlayerData data = new MusicPlayerData();

        turnOn(data);
        raiseVolume(data);
    }

    static void turnOn(MusicPlayerData data){
        data.isOn = true;
        System.out.println("music player is on");
    }

    static void raiseVolume(MusicPlayerData data){
        data.volume++;
        System.out.println("volume: " + data.volume);
    }
```

- more focused on the **order** (turn on, then raise volume)
- 👎🏻 music player `field` and `method` are in different classes
- one in `music player class` and other in `main class`
- `field` and `method` of music player are very very relevent
- can we find a way to put `field` and `method` in one class?

## ✅ change into OOP

- music player class
- has both `field` and `method`

```java
public class MusicPlayer {
    int volume; //field
    boolean isOn; //field

    void turnOn(){ //method
        isOn = true;
        System.out.println("music player is on");
    }

    void raiseVolume(){ //method
        volume++;
        System.out.println("volume: " + volume);
    }
}
```

- main class
- only create instance, calls the method

```java
public class MusicPlayerMain4 {
    public static void main(String[] args) {
        MusicPlayer player = new MusicPlayer();

        player.turnOn();
        player.raiseVolume();
    }
}
```

- more focused on **how** the music player works

- 👍🏻 `field` and `method` are in one class, easier for the programmer to understand
- 👍🏻 programming looks more like real life
- 👍🏻 easier to change code
  - only has to change `music player class`, `main class` does not change

## ✅

## ✅

## ✅

## ✅

## ✅
