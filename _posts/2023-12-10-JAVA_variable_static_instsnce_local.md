---
title: Variable_static/ instance/ local
categories: [JAVA, JAVA_Basics]
tags: [static, instance, local] # TAG names should always be lowercase
---

## Static 🆚 Instance 🆚 Local

```java
public class Variable {
    //static 클래스 변수
    // 프로그램이 처음 시작될 때 생성, 프로그램 끝나고 메모리 해제할 때 소멸
    private static int classVariable;
    //인스턴스 변수
    // 객체에 속한 변수
    // 힙이 생성되고 JVM위에 올라감
    private int instanceVariable1;
    //로컬 변수(지역변수)
    // 메소드에서 쓰이고 사라지는 변수
    // 메소드 안에서만 의미가 있지, 밖에서는 의미가 없음
    public void saySomething(int lcoalVarable){
        int localV= 3;
    }

}
```
