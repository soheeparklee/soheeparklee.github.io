---
title: for/ for-each/ while/ do whlie
categories: [JAVA, JAVA_Basics]
tags: [] # TAG names should always be lowercase
---

## ✅ for

### if(변수 초기화, 루프 조건, 루프 끝나면 이행할 내용)

```java
for (int i=0; i<10; i++){
            System.out.println(i);
        }
//똑같은 코드
for (int i=0; i<10;){
    System.out.println(i);
    i++;
}
```

### for문 안에 string이 들어갈 수도 있다.

```java
for (String s = ""; s.length() < 11; s += s.length()) {
            System.out.println(s);
        }

//result
// 0
// 01
// 012
// 0123
// 01234
// 012345
// 0123456
// 01234567
// 012345678
// 0123456789
```

### 💡 쉼표로 구분하여 여러 변수 사용 가능

```java
for (byte a = 0, b = 10; a <= b;) {
    System.out.printf("a: %d, b: %d%n", a++, b--);
    }

```

## ✅ for in array

```java
//  4의 배수 차례로 10개 배열에 담기
        int count = 10;
        int[] multiOf4 = new int[count];

        for (int i = 1, c = 0; c < count; i++) {
            if (i % 4 == 0) {
                multiOf4[c++] = i;
            }

        }
//multiOf4 배열= [4, 8, 12, 16, 20, 24, 28, 32, 36, 40]
        for (int n= 0; n<multiOf4.length; n++){
            System.out.println(multiOf4[n]);
        }
//4 8 12 16...한 줄 씩 띄어가며 print
```

## 💡 for-each

array에서 하나하나 돌며 각각의 index를 건드리는 방법 ➡️ `foreach` <br>

```java
for (int n= 0; n<multiOf4.length; n++){
            System.out.println(multiOf4[n]);
        }
//이 방법을 foreach로 쓰면 다음과 같다.
for (int num: multiOf4){
    System.out.println(num);
}
//num은 multiOf4배열안에 있는 요소들을 하나하나 1씩 늘려가며 건드림.
//multiOf4의 배열 길이....또 n이라는 변수...이런거 다 필요 없이 foreach만 있으면 됨.
//multiOf4 배열= [4, 8, 12, 16, 20, 24, 28, 32, 36, 40] 이렇게 생겼으니까 4 8 12 16...한 줄 씩 띄어가며 print

```

💡 `for-each`사용하여 배열 안 숫자 다 더하기 <br>

```java
int sumOfArray = 0;
for (int num : multiOf4) {
    sumOfArray += num;
}
```

## ✅ for in for 중첩 루프

### 구구단 만들기

```java
for(int i=1; i<10; i++){
            System.out.printf("-----%d단-----%n", i);
            for(int j=1; j<10; j++){
                int result= i * j;
                System.out.printf("%d * %d = %d%n", i, j, result);
            }

        }
```

## 🛑 continue, break

for문을 멈추기

### continue

한 루프만 건너뜀, 그 조건 만족하는 루프만 건너 뛰기 <br>

```java
for (int i = 0; i < 100; i++) {
            //  💡 continue : 한 루프만 건너뜀
            if (i % 3 == 0) continue;
            System.out.println(i);
        }
// 1 2 4 5 7 8 10 11....98까지 출력
//100까지의 수 중에서 3의 배수만 출력하지 않음, 뛰어 넘었으니까
```

### break

for문 블록 전체를 종료하고 나와버림. <br>

```java
for (int i = 0; i < 100; i++) {
            //  💡 break : 블록 전체를 종료
            if (i == 10) break;
            System.out.println(i);
        }
//1 2 3 4 5 6 7 8 9
//i가 10되면 끝
```

## ✅ while

조건이 `true`일 동안 실행 <br>

```java
int i= 0; //변수 초기화

while(i < 10){ //while 실행될 조건
    System.out.println(i);
    i++; //루프 한 바퀴 돌 때마다 변화시킬 변수
}
```

## ✅ do while

일단 실행하고 while 조건을 본다. <br>

```java
int x = 1; // 10 이상으로 바꿔서 다시 실행해 볼 것
int y = x;

while (x < 10) {
    System.out.println("while 문: " + x++);
}

do {
    System.out.println("do ... while 문: " + y++);
} while (y < 10);
// x, y모두 10보다 작을 때는 순서대로 while문, do...while문 print
// 하지만 x=11로 설정하면 x의 while문은 전혀 프린트 되지 않음,
// 그런데 y는 do...while문이기 때문에 한번 실행되어서 "do ... while 문: 11" 프린트 되고 그제서야 "앗 조건 만족 안하넹" 하고 멈춤.
```

## ✅ while in while 중첩 while

```java
final int LINE_WIDTH = 5;

        int lineWidth = LINE_WIDTH;

        while (lineWidth > 0) {
            int starsToPrint = lineWidth--;
            while (starsToPrint-- > 0) {
                System.out.print("*");
            }
            System.out.println();
        }

// *****
// ****
// ***
// **
// *

```

💡for문으로 다시 작성하면? <br>

```java
for (int i = LINE_WIDTH; i > 0; i--) {
            for (int j = i; j > 0; j--) {
                System.out.print("@");
            }
            System.out.println();
        }
```
