---
title: Operator
categories: [JAVA, JAVA_Basics]
tags: [unary] # TAG names should always be lowercase
---

## ✅ 단항연산자 Unary Operator

### difference between `X++` VS `++X`

둘 다 X의 값을 1씩 증가시키는데, 그 시기가 다르다. <br>
`X++`은 증가시킨 후 그 값을 이후부터 적용, <br>
`X++ 다음부터` <br>
`++X`는 미리 증가시켜서 바로 적용. <br>
`지금 당장 ++X`<br>

```java
        int x1 = 3;
        int y1= 3;

        int x2 = x1++; // x1은 4, x2는 아직 3
        int y2 = ++y1; // y1은 4, y2는 이미 4

        int z1 = (x2 * y2); // 3 곱하기 4= 12
        int z2 = (x2-- * --y2); // 3곱하기 3= 9

```

```java
		int x = 1;

        //  메서드 안으로도 '반환'되어 사용되는 것
        System.out.println(x++); //print 1, 그 다음 코드부터 x는 2가 되었을 것
        System.out.println(++x); // print 3, 위 코드에서 x는 2가 되었는데, 앞에 ++이 붙으면 바로 1씩 증가시켜 적용
        System.out.println(x); //print 3
```

## ✅ 논리연산자

### a `&` b <br>

1&1= 1 <br>
1&0= 0 <br>
0&1= 0 <br>
0&0= 1 <br>

주어진 숫자들의 이진값을 계산

```java
System.out.println(10 & 12);
// 8을 반환합니다.
//10= 1010
//12= 1100
//따라서 1000 = 8
```

### a `&&` b `AND` <br>

a와 b가 모두 true일때만 true 반환 <br>

### a `||` b `OR`

a와 b 중 하나만 true면 true 반환 <br>

```java
boolean eventTime= true;
        boolean instagram= true;
        boolean regram= true;
        boolean comment= true;

        if(eventTime){
            if(instagram){
                if(regram){
                    if(comment){
                        System.out.println("참여 가능");
                    }else{
                        System.out.println("참여 불가능");
                    }

                }else{
                    System.out.println("참여 불가능");
                }

            } else{
                System.out.println("참여 불가능");
            }

        } else{
            System.out.println("참여 불가능");
        }

//이렇게 긴 코드를 논리연산자로 쓰면 다음과 같다.
//boolean있을 때는 논리연산자 사용을 강추!
if(eventTime && instagram && regram && comment){
            System.out.println("참여 가능");
        }else{ System.out.println("참여 불가능");
        }
```

## ✅ short circuit 단축평가

`&&` : 앞이 false이면 뒤에 것을 평가할 필요 없음, 무조건 false <br>
`||`: 앞이 true이면 무조건 true <br>

## ✅ 삼항연산자

- a `?` b `:` c <br>
  - a : 불리언 값 <br>
  - b : a가 `true` 일 때 반환될 값 <br>
  - c : a가 `false` 일 때 반환할 값 <br>

```java
milk= (thereIsAvocado) ? 6:0
//우유의 개수는, 아보카도가 있으면 6개, 없으면 0개
```
