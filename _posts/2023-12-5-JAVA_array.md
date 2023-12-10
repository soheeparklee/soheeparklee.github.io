---
title: Array
categories: [JAVA, JAVA_Basics]
tags: [array] # TAG names should always be lowercase
---

## ✅ Array

배열이 담는 자료형의 크기만큼 메모리를 차지한다. <br>
따라서 넣은 자료들에 비해 너무 큰 배열을 선언하는 것을 주의할 것. <br>

### how to declare an array

#### with value

```java
String [] students= {"charlie", "jack", "sophie"};
```

#### without value, empty array with just size

new가 필요한 이유: array는 literal이 아니기 때문! <br>

```java
String [] family= new String [6];
family[0]= "mother";
family[1]= "dad";
```

#### array length

```java
int arrayLength= students.length;
```

#### get value

use index

```java
 String who= students[1];
```

#### set value

use index

```java
students[0]= "peter"; //students: ["peter", "jack", "sophie"]
```

#### printArray `Arrays.toString()`/ `Arrays.deepToString()`

array는 reference type이기 때문에 그냥 출력하면 array의 메모리값이 출력된다. <br>

```java
int[] nums= {1,2,3,4,5};
System.out.println(nums);
System.out.println(Arrays.toString(nums));
//result:
// [I@6bdf28bb
// [1, 2, 3, 4, 5]
```

```java
int [] [] IntAry= new int [] [] {
                {1,2,3},
                {4,5},
                {6,7,8}
        };
System.out.println(Arrays.deepToString(IntAry));
```

## ✅ for in array/ foreach

```java
int[] score= {90, 85, 90, 35, 75};

for(int i=0; i<=score.length; i++){
        System.out.println(score[i]);
}
for(int num:score){
        System.out.println(num);
}
```

## ✅ 다중 배열: 배열 안에 또 배열

배열 안에 배열이 있으므로 `IntAry[num]`하면 num번쨰 배열을 받을 것이고, <br>
숫자를 받고 싶다면 `IntAry[num][num]`<br>

#### 2D array

```java
        int [] [] IntAry= new int [] [] {
                {1,2,3},
                {4,5},
                {6,7,8}
        };
        int[] result1 = IntAry[0]; // [1, 2, 3]
        int result2= IntAry [0][1]; // 2
```

#### for in for 사용해서 2D array 프린트

```java
int twoDimensionArray[][] = new int[] []{
                {5, 10, 15, 20},
                {25, 30, 35, 40},
                {45, 50, 55, 60},
                {65, 70, 75, 80},
        };

        for(int row= 0; row< 4; row++){
            for(int col= 0; col<4; col++){
                System.out.printf("%d ", twoDimensionArray[row][col]);
            }
            System.out.println();
        }

// 5 10 15 20
// 25 30 35 40
// 45 50 55 60
// 65 70 75 80
```

#### for in for 사용헤서 두 array 합한 새로운 array

```java
int [][]arr1= new int[] []{
                {5, 10, 15, 20},
                {25, 30, 35, 40},
                {45, 50, 55, 60},
                {65, 70, 75, 80},
        };

int [][]arr2 = new int[] []{
        {1,2,3,4},
        {5,6,7,8},
        {9,10,11,12},
        {13,14,15,16},
};

int[][] arrSum = new int[4][4];

for(int row= 0; row< 4; row++){
        for(int col= 0; col<4; col++){
        int num1= arr1[row][col];
        int num2= arr2[row][col];
        int sum= num1+ num2;

        arrSum[row][col]= sum;
        }
}
System.out.println(Arrays.deepToString(arrSum));
```

## ✅ 배열의 복사

reference type인 array를 원본 따로 복사하고 싶어요

#### for 사용해서 copy

b는 a를 복사한 배열 <br>

```java
int[] a = {1,2,3,4,5};
int[] b= new int[a.length];

    for(int i=0; i<= a.length; i++){
        b[i]= a[i];
    }

//복사한 다음
//a 배열의 값을 바꾸고 출력해보면?
a[0]= 6;
a: [6,2,3,4,5];
b: [1,2,3,4,5];
//b배열은 바뀌지 않았다는 것을 알 수 있다.
```

#### copyOf

```java
int[] a = {1,2,3,4,5};
int[] b= Arrays.copyOf(a, a.length);
```

#### clone

clone은 1차원 array일 떄만 가능하다.

```java
int[] a = {1,2,3,4,5};
        int[] b= a.clone();
```

## ✅ 2D 배열의 복사

```java
int[][] arr = new int[][]{
                {5, 10, 15, 20},
                {25, 30, 35, 40},
                {45, 50, 55, 60},
                {65, 70, 75, 80},
        };

        int[][] arrCopy = new int[4][];
        for(int row=0; row<4; row++ ){
            arrCopy[row]= arr[row].clone();
        }
```
