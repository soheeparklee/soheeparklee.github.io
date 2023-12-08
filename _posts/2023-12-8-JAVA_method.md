---
title: method
categories: [JAVA, JAVA_Basics]
tags: [overloading, return, parameter] # TAG names should always be lowercase
---

## ✅ 메소드의 의미

#### 반복을 최소화한다.

한 번 이상 실행할 수 있는 일련의 작업들을 묶는다.

#### return값을 반환한다.

##### ⭐️ 반환이란:

## ✅ 메소드 선언 방법

### ☑️ 문법

![이름 없는 노트북-3](https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/d08c82e4-8115-4ff9-a0b1-7c363b314eb2)

#### return 없다면?

```java
public static void main(String[] args) {

        printWhatISay("I love JAVA");

        }
        //static void
        static void printWhatISay (String a){
            System.out.println(a);
        }
```

### ☑️ 선언 장소

```java
public static void main(String[] args) {
        //이 안에서 메소드 호출
        int resultAdd= add(1,2);
        System.out.println(resultAdd);

        System.out.println(add(1,2));


        }

        //public static void main(String[] args) 밖에다가 메소드 선언
        static int add(int a, int b){
        return a + b;
        }

```

## ✅ 배열을 parameter에 받을 수도 있다.

꼭꼭 항상 datatype정의해 줄 것!

```java
public static void main(String[] args) {
        //메소드 호출
        //인자에 새로운 배열 넣어주어야
        double result= getAverage(new int[] {1,2,3,4,5});
        System.out.println(result);
        }
        //함수 getAverage, parameter로 int배열을 받는다.
        static double getAverage(int nums[]){
        double sum = 0;
        //for each구문
        for(int num : nums){
            sum += num;
        }

        double average = sum / nums.length;
        return average;
        }
```

## ✅ 두 개 이상의 값을 return하고 싶다면? ➡️ 배열 사용

배열을 반환하는 메소드도 가능

```java
 public static void main(String[] args) {
        int[] numbers= new int[] {1,2,3,4,5};
        int minimum= minMax(numbers)[0];
        int maximum= minMax(numbers)[0];

        }
        static int[] minMax(int nums[]){
        int min= nums[0];
        int max= nums[0];
        for (int num:nums) {
            min= min < num ? min: num;
            max= max > num ? max: num;
        }
        return new int[] {min, max};
        }
```

## ✅ ...연산자: parameter 개수를 정하지 않고도 메소드 사용 가능

parameter을 몇 개 받을지 정하지 않고 `int...nums`라고 해서 메소드 선언 가능
그러면 메소드가 자동으로 받은 parameter들을 배열로 묶음.
바로 그냥 배열을 parameter에 넣어도 됨.
물론 하나의 parameter만 넣는 것도 가능.

단, 여러 개의 parameter입력 시 개수가 정해지지 않은 parameter은 맨 마지막으로 받아야 하고
또, 개수가 정해지지 않은 parameter은 한 메소드 당 하나만 있을 수 있음.

```java
public static void main(String[] args) {
        //숫자 여러개, 아무거나 넣어도 배열로 묶어 메소드에 전달
        double result= getAverage(1,2,3,4,5);
        System.out.printf("result: %f%n", result);
        //물론 배열을 넣어도 됨
        //배열을 넣으면 자동으로 퍌쳐져 인식됨.
        int[] numArray= {1,2,3,4,5};
        double resultArray= getAverage(numArray);
        System.out.printf("resultArray: %f%n", resultArray);
        }
        //...연산자: 해당 위치 뒤로 오는 parameter를 배열로 묶어 받음.
        // 다른 정해진 인자들이랑 사용하고 싶으면 맨 뒤에 넣을 것
        //이렇게 값이 정해지지 않은 parameter은 한 메소드 당 한 개만 있을 수 있음.
        static double getAverage(int...nums){
        double average=0.0;
        for(int num:nums){
            average+= num;
        } return average/nums.length;
        }

```

## ✅ 메소드 오버로딩

같은 메소드 이름으로 다른 parameter받기
같은 성질의 작업을 정의하는데(더하기) 서로 다른 자료형의 값들로 할 때(different datatype, different parameter)

```java
public static void main(String[] args) {
        int res1 = add(1, 2); // res1: 3
        int res2 = add(3, 4, 5); //res2: 12
        double res3 = add(1.2, 3.4); //res3: 4.6
        String res4 = add("로보트 태권", 'V'); //res4: "로보트 태권V"
        String res5 = add('X', "Men"); //res5: "XMen"
    }

    //제일 기본 더하기 메소드
    static int add(int a, int b) { return a + b; }

    //  매개변수의 개수가 다름
    static int add(int a, int b, int c) { return a + b + c; }

    //  매개변수의 자료형이 다름, ⚠️ 그래서 아래 return 자료형이 다른 것과는 다르게 실행 가능 ⭕️
    static double add(double a, double b) { return a + b; }

    //  매개변수의 자료형 순서가 다름
    static String add(String a, char b) { return a + b; }
    static String add(char a, String b) { return a + b; }


```

### ⚠️ return 자료형이 다른 것은 오버로딩 안 됨

근데 이 메소드가 문법적으로 틀린 것은 ❌
오버로딩이 안 될 뿐!
만약 이 메소드가 다른 이름으로 정의되었다면 실행되었을 코드임.

```java

public static void main(String[] args) {
        double res5= add(3,4) //res5: 7.0
    }
    static double add(int a, int b) { return (double) (a + b); } //실행 안 됨 ❌

```

## ✅ reference type이 parameter로 왔을 때 원본 바뀌나?

원시형 parameter을 받았을 때는 원본 값이 바뀌지 않는다.
배열의 한 요소를 parameter로 받았을 때도 원본이 바뀌지는 않는다.
모두 원시형이니 **복사본**을 전달해 바꿨으므로 원본이 바뀌지는 않는다.

하지만 reference type을 parameter로 받았을 때는 다르다.
reference type은 주소를 복사해서 알려줘 버리므로
원본 그 자체가 변해버린다.

```java
//옛날옛날에 원시형과 배열(reference type)이 살고 있었어요.
//원시형
int intNum = 3;
//배열의 한 요소 ➡️ 원시형
int oneOfintNums= intNums[0];
//배열 ➡️ reference type
int[] intNums = {1, 2, 3};

//메소드도 있었어요.
//원시형을 parameter로 받는 메소드
static void modifyIntArg (int num) {
        System.out.printf("수정 전: %d%n", num++);
        System.out.printf("수정 후: %d%n", num);
    }

//reference type을 parameter로 받는 메소드
static  void modifyAryElem (int[] ary) {
        System.out.printf("수정 전: %d%n", ary[1]++);
        System.out.printf("수정 후: %d%n", ary[1]);
    }

//각각 다음 코드를 실행한 후 원본을 출력해 봅시다.
modifyIntArg(intNum);  //intNum: 3
modifyIntArg(oneOfintNums); // 그래도 intNums배열 출력해보면 intNums: [1, 2, 3]
modifyAryElem(intNums); //intNums: [1, 3, 3]

//reference type의 경우 원본이 아예 바뀌어 버린 것을 볼 수 있음.

```

```java

```
