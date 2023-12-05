---
title: Array
categories: [JAVA, JAVA_Basics]
tags: [array, primitivetype, referencetype] # TAG names should always be lowercase
---

## ✅ Array

배열이 담는 자료형의 크기만큼 메모리를 차지한다.  
따라서 넣은 자료들에 비해 너무 큰 배열을 선언하는 것을 주의할 것.

### how to declare an array

#### with value

```java
String [] students= {"charlie", "jack", "sophie"};
```

#### without value, empty array with just size

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

```java
 String who= students[1];
```

#### change value

```java
students[0]= "peter"; //students: ["peter", "jack", "sophie"]
```

## ✅ 다중 배열: 배열 안에 또 배열

배열 안에 배열이 있으므로 `IntAry[num]`하면 num번쨰 배열을 받을 것이고, 숫자를 받고 싶다면 `IntAry[num][num]`

####

```java
        int [] [] IntAry= new int [] [] {
                {1,2,3},
                {4,5},
                {6,7,8}
        };
        int[] result1 = IntAry[0]; // [1, 2, 3]
        int result2= IntAry [0][1]; // 2
```

## 💡 Primitive Type VS Reference Type

### ✔️ Primitive type

primitive type은 값 자체를 바꾼다. 그래서 바꾼 값num2는 num1값인 1이 된다.

####

```java
int num1 = 1;
int num2 = 2;
num2 = num1;
num2 = 3;
```

<img width="230" alt="스크린샷 2023-12-05 오후 8 39 43" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/038461a5-2b41-4764-9ff7-49da0b807e26">

num1의 값은 1이고 num2의 값은 2이다. <br>
num2에 num1의 값을 저장하므로 num1도 1, num2도 1이 된다. <br>
그리고 num1만 3으로 바꾸면, num1의 값은 3, num2의 값은 여전히 1이다. <br>
하나의 변수에 다른 변수의 값을 넣은 다음, 한 변수의 값을 바꿔도 다른 변수의 값은 바뀌지 않는다. <br>
primitive type은 값을 복사해서 넣어준다. 그래서 두 변수의 값은 전혀 다른 값이고, 서로 영향을 주고 받지 않는다. <br>
예를 들어 하나의 종이를 복사해 두 개를 만들었는데, 한 종이에 쓴다고 해서 다른 종이에도 막 쓰여지지는 않는 것처럼. <br>

### ✔️ Reference type

Reference Type은 다르다. <br>
Reference Type은 값 자체를 넣어주는 것이 아니라, 값이 저장되어 있는 장소를 알려준다. <br>

#### 배열이 있는 장소/주소를 알려주는 Reference type

```java
char[] chAry1= {'A', 'B', 'C'}; //[A, B, C]
char [] chAry2= {'L', 'M', 'N'};
chAry2 = chAry1;
chAry1[0]= 'Z';
```

chAry1의 값을 바꾸면 chAry2의 값도 바뀌어버림! <br>
배열에서는 **배열이 있는 어떤 장소/주소**를 가리키고 있는 것이다. <br>
그래서 `chAry2 = chAry1;`한다는 것은, 두 배열이 같은 메모리 장소/주소를 가리키게 되는 것. <br>
두 배열이 같은 집 주소를 가지게 된다. <br>
그래서 그 집을 바꾸게 되면, 같은 집 주소를 가진 두 배열 모두 바뀌게 된다. <br>

##### before

<img width="438" alt="스크린샷 2023-12-05 오후 8 37 53" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/23b2a0ed-c223-4284-b630-6f0b594d7e14">

##### after `chAry1[0]= 'Z'`

<img width="443" alt="스크린샷 2023-12-05 오후 8 38 43" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/0ef1d893-df30-4999-af9a-6a9fd4930d2d">
