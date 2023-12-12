---
title: 2023.DEC.11(MON) JAVA DAY6
categories: [TIL(Today I Learned), SuperCoding_JAVA]
tags: [todayilearned, til, poweroftwo, algorithm]
---

## ✅ Daily Report

### 📌 **TO-DO LIST**

- [x] submit github blog post
- [x] lesson 23, 24, 25, 26, 27
- [x] assigment: 2진법
      <br>
      <br>

## ✅ Today I Learned

### 배열의 길이를 확인해서 2진수이면 그대로, 아니면 더 채워서 이진수 길이 만들기

#### arr length가 2진법인지 확인

확인해서 참이면 array를 return <br>
<https://soheeparklee.github.io/posts/JAVA_operator/>

```java
int arrLength = oldArray.length;
        if ((arrLength & (arrLength - 1)) == 0) {
            return oldArray;
        }
```

#### 우리가 가진 배열의 길이에 가장 가까운 2진수 숫자 구하기

`int targetLength= 1`로 하나 변수 정해서 <br>
이 변수에 계속 2를 곱하고 <br>
우리의 배열 길이랑 비교함. <br>

```java
int newArrLength = 1;
        while (newArrLength < arrLength) {
            newArrLength = newArrLength * 2;
        }
```

#### 가장 근접한 2진수 숫자 구했으면 0 몇개 더해야하는지 구함

추가해야 하는 0의 개수

```java
int[] newArray = new int[newArrLength];
```

#### 0을 추가한 배열 반환

```java
        for (int i = 0; i < arrLength; i++) {
            newArray[i] = oldArray[i];

        }return newArray;
      //새로운 배열 newArr을 만들었음.
      //여기에 arr[i](기존 배열)을 넣을건데, 다 넣고 남은 인덱스는 넣을 것이 없으니 0으로 채워질 것임.
      //arr[i]가 없으면 0이 추가될 것임
```

#### ☑️ final code

```java
import java.util.Arrays;

public class Test {
public static void main(String[] args){
    int[] arr1 = {1, 2, 3, 4, 5, 6};
    int[] result1 = getArray(arr1);
    System.out.println(Arrays.toString(result1));

}
    static int[] getArray(int oldArray[]) {
        int arrLength = oldArray.length;
        if ((arrLength & (arrLength - 1)) == 0) {
            return oldArray;
        }
        int newArrLength = 1;
        while (newArrLength < arrLength) {
            newArrLength = newArrLength * 2;
        }
        int[] newArray = new int[newArrLength];
        for (int i = 0; i < arrLength; i++) {
            newArray[i] = oldArray[i];

        }return newArray;
    }
}
```
