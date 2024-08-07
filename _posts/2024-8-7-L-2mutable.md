---
title: Mutable 🆚 Immutable, Final
categories: [JAVA, JAVA_Basics]
tags: [] # TAG names should always be lowercase
---

## ✅ Mutable

> can be modified after initialization <br>
> encapsulate: getter, setter, private, final field <br>
> need to synchronize access for multi thread <br>

- String Builder
- Stirng Buffer
- java.util.Date

## ✅ Immutable

> cannot be modified after initialization <br>
> 힙 영역에 저장된 값을 변경할 수 없는 것 <br>
> preferred in multi threading, as it guarantees thread saftey <br>
> 공유 자원이 Immutable하다면 여러개의 쓰레드가 읽고 써도 안 바뀌니까 safe! <br>

- int
- long
- float
- double
- String
- legacy, wrapper classes

> I changed value from 1 to 3. Does this mean Integer is mutable?

```java
Integer i=1;
i=3;
//바꿨는데요??
// 아님, 힙 영역에 새로운 객체가 생성된 것이다.
```

> > NO. New object in heap created.
> > and Integer with value 1 will be discared by GC
> > <img width="629" alt="image" src="https://github.com/user-attachments/assets/392f71f3-c9d1-4a87-bd28-c93d56fb640b">

## ✅ Final

> 초기화 이후에 값 변경 불가 <br>
> immutable <br>

```java
final Integer i=1;
i=3; //❌ compile error.
```

<https://www.geeksforgeeks.org/mutable-and-immutable-objects-in-java-1/>
