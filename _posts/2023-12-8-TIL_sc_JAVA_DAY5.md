---
title: 2023.DEC.08(FRI) JAVA DAY5_별 숫자 늘리고 줄여서 다이아몬드 모양
categories: [TIL(Today I Learned), SuperCoding_JAVA]
tags: [todayilearned, til, method, scanner, algorithm]
---

## ✅ Daily Report

### 📌 **TO-DO LIST**

- [x] submit github blog post
- [x] study yalco method, scanner
- [x] lesson 17, 18, 19, 20, 21, 22
- [x] assigment: make stars into diamond array using for
      <br>
      <br>

## ✅ Today I Learned

#### ✔️ using for in for to increase and decrease the number of stars

### ⭐️ 별 1~5까지 순서대로 내려가기

#### 💡 while 문으로 작성하면? <br>

```java
        int line =0;

        while (line < 5){
            int star= 0;
            while(star <= line){
                System.out.print("*");
                star++;
            }
            System.out.println();
            line++;
        }
```

#### 💡 for문으로 작성하면? <br>

```java
       int max= 5;
        for(int line=0; line < max; line++){
           for (int star=0; star <= line; star++){
               System.out.print("*");
           }
           System.out.println();
       }
```

### ⭐️ 별 5~1로 거꾸로 내려가기

#### 💡 while 문으로 작성하면? <br>

```java
    int line =0;

       while (line > 0) {
           int star = line--;
           while (star-- > 0) {
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

#### 💡 for문으로 작성하면? <br>

```java
for (int i = line; i > 0; i--) {
            for (int j = i; j > 0; j--) {
                System.out.print("@");
            }
            System.out.println();
        }
```

### ⭐️ 별 커졌다가 작아지기

```java
int size= 10;
    for (int line= 0; line <  size; line++){
        for (int star=0; star <= line; star++){
            if(star%2 ==0) continue;
            System.out.print("*");
        }
        if(line%2 ==0) continue;
        System.out.println();
    }
    for (int line= size; 0 <  line; line--){
        for (int star=0; star <= line-3; star++){
            if(star%2 ==0) continue;
            System.out.print("*");
        }
        if(line%2 ==0) continue;
        System.out.println();
    }

// *
// ***
// *****
// *******
// *********
// *******
// *****
// ***
// *

```

### ⭐️ 별 다이아 모양으로 출력

```java
        int size=3;
        for(int line=1; line <= size; line++){
            for(int space= size-line; space >=1; space-- ){
                System.out.print(" ");
            }
            for(int star= 1; star <= 2*line -1; star++){
                System.out.print("*");
            }
            System.out.println();
        }
        for(int line= size-1; line>=1; line-- ){
            for(int space= 1; space<= size-line; space++){
                System.out.print(" ");
            }
            for(int star=1; star<=2*line-1; star++){
                System.out.print("*");
            }System.out.println();
        }

//   *
//  ***
// *****
//  ***
//   *
```

#### how to get input from user using scanner

#### how do declare and use methods in JAVA.
