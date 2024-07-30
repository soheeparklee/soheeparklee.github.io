---
title: Serialization
categories: [JAVA, JAVA_Basics]
tags: [] # TAG names should always be lowercase
---

## ✅ Serialization

> converting the state of an object into a `byte` stream <br>

- all PCs would have different virtual memory according to their OS
- so `reference types` cannot travel across a network, need to be serialized
- transmit object data in forms of address❌ byte⭕️
- `serialized data` becomes `primitive data`

👍🏻 Save/persist state of an object. <br>
👍🏻 Travel an object across a network. <br>

<img width="487" alt="Screenshot 2024-07-30 at 10 51 12" src="https://github.com/user-attachments/assets/ed8f576b-d570-4015-a✔️8a0-ef3eabc73e4f">

## 🛠️ How to serialize

- implement `java.io.Serializable` interface

## ✔️ SerialVersionUID

> version number of serialization <br>
> used during Deserialization to verify that sender and receiver of a serialized object have loaded classes for that object which are compatible with respect to serialization <br>

## 💡 Reference

<https://soheeparklee.github.io/posts/JAVA_4serverClient/>
