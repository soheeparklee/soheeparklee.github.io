---
title: if/ else/ switch
categories: [JAVA, JAVA_Basics]
tags: [if, else, switch, break] # TAG names should always be lowercase
---

## ✅ if: boolean값으로 판단

```java
//빈 string안에다가 점점 추가할 수도 있다.
        boolean wantCoffee= true;
        boolean likeMilk= false;
        boolean coldWeather = true;
        boolean likeSweet= false;

        if(wantCoffee) {
            String toOrder = "";

            toOrder= likeMilk ? "latte": "americano"; //삼항연산자
            if(coldWeather) toOrder= "hot " + toOrder;
            if(likeSweet) toOrder += "sweet";

            System.out.printf("Give me a %s, please", toOrder);
        }
//Give me a hot americano , please
```

## ✅ else if

**else if :** 첫 if문이 false일 때 다른 조건을 연속 사용 <br>
이거 아니면 그 다음 줄 else if, 모든 조건 다 아니면 else <br>
조건을 만족하면 나간다. <br>

```java
		int score = 85;

        //  💡 else if : 첫 if문이 false일 때 다른 조건을 연속 사용
        //  else만 사용하는 것은 맨 마지막에
        if (score = 100) {
            System.out.println('A');
        } else if (score > 90) {
            System.out.println('B');
        } else if (score > 80) {
            System.out.println('C');
        } else {
            System.out.println('F');
        }

```

💡 더 효과적인 방법은 계속 **if**로 코드를 짜는 것이다. <br>
아래 코드는 위 코드와 같은 내용을 출력함. <br>
**if**로 코드를 짜는 것이 더 좋은 이유는, else if는 하나의 메소드로 중첩, <br>
**if**는 메소드 실행해보고 안 되면 바로 return, 더 깔끔한 코드 가능. <br>
**return**: 메소드를 종료하고 빠져나옴. <br>

```java
int score = 85;

        //  ⭐ 보다 가독성 좋은 방식
        //  return문: 해당 메소드를 종료하고 빠져나옴

        if (score = 100) {
            System.out.println('A');
            return;
        }
        if (score > 90) {
            System.out.println('B');
            return;
        }
        if (score > 80) {
            System.out.println('C');
            return;
        }
        System.out.println('F');

```

## ✅ switch: switch안에 다양한 datatype 올 수 있음

🆚 if : if문은 Boolean
switch: boolean말고 다양한 데이터타입

### switch & case & break& default

#### **case**

case 안에는 받을 datatype과 같은 datatype이 들어가 있어야 함. <br>
가능한 자료형: byte, short, int, char, String <br>
이 case아니면 다음 case로 넘어가, 통과! <br>

```java
//변수가 string이면 case도 string
String howManyFingers = "2";

switch (howManyFingers) { //괄호 안에 기준이 될 변수를 받음.
    case "2":

//변수가 int이면 case도 int

int howManyFingers = 2;

switch (howManyFingers) { //괄호 안에 기준이 될 변수를 받음.
    case 2:

```

#### **break:**

내가 원하는 것 찾았으면 switch문 종료, 찾은 부분 뒷 부분은 실행하지 않음 <br>

#### **default:**

해당하는 case가 없을 때, 마지막에 작성 <br>

```java
        String howManyFingers = "2";
        String hand;

        switch (howManyFingers) {
            case "0":
                hand = "rock";
                break;
            case "2":
                hand = "scissors";
                break;
            case "5":
                hand = "paper";
                break;
            default:
                hand = null;
        }

        System.out.println(
                hand != null ? hand : "너 아무것도 안 냈어!"
        );
```

### 여러개의 case도 가능함

```java
//예를 들어 7월이면, case7에 가서 통과, break; 없으니 case8로 갔다가 결국 break, 여름이 됨.
        int month = 7;
        String season;

        switch (month) {
            case 3:
            case 4:
            case 5:
                season = "봄";
                break;
            case 6:
            case 7:
            case 8:
                season = "여름";
                break;
            case 9:
            case 10:
            case 11:
                season = "가을";
                break;
            case 12:
            case 1:
            case 2:
                season = "겨울";
                break;
            default:
                season = null;
        }

        System.out.println(
                season != null
                        ? "지금 계절은 %s입니다.".formatted(season)
                        : "1년 중 %d월은 없습니다.".formatted(month)
        );
```
