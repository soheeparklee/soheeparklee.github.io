---
title: Optional
categories: [JAVA, JAVA_Basics]
tags: [optional] # TAG names should always be lowercase
---

## ✅ NPE(= Null Point Exception)

Java reference type은 모두 Null 로 초기화되어 있다.
따라서 NPE는 언제 어디서나 발생 가능

### NPE 발생하는 경우

1. null로 된 값의 메소드나 필드 참조 시 NPE 발생
2. String array의 기본값이 null이라서 NPE 발생

### NPE 해결 방안

1. NPE 발생 시, catch문 사용자 정의 예외 던지기
2. NPE 발생 시, catch 문 기본값 사용하기
3. JAVA optinal: null방지 메소드를 지원하는 wrapper 클래스
   wrapper 클래스: 기본 클래스 호환 + 특정한 기능을 지원하는 클래스

## ✅ JAVA optinal의 메소드

### 💡 ElseThrow

```java
import java.util.Optional;

public class OptionalThrowTest {
    public static void main(String[] args) {
        String str= "abc";
        Optional<String> stringOptional= Optional.ofNullable(str);

        //null이면 throw
        int length= stringOptional.orElseThrow(() -> { throw new CustomException("CustomerException occured"); } ).length();

        System.out.println(length);
    }
}
//3
//String str= null; 이면 0출력
```

### 💡 ElseGet

```java
import java.util.Optional;

public class OptionalDefaultTest {
    public static void main(String[] args) {
        String str=null;
        Optional<String> optionalS= Optional.ofNullable(str);
        //null이면 기본값인 ""의 길이 0을 출력하게 된다.
        int length= optionalS.orElseGet(()->"")
                .length();
        System.out.println(length);
    }
}
//0
```
