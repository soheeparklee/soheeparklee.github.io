---
title: String Method
categories: [JAVA, JAVA_Basics]
tags: [
    length,
    isempty,
    isblank,
    trim,
    chatat,
    indexof,
    equals,
    contains,
    startwith,
    matches,
    compareto,
    touppercase,
    concat,
    methodchaining,
    repeat,
    substring,
    replace,
    tochararray,
    join
    split
  ] # TAG names should always be lowercase
---

## ✅ String is immutable

reference type, 값을 바꿔도 저장한 다른 값에 영향을 미친다. <br>

## 💡 `length()` 문자열 길이 반환

```java
String str= "Hello"
int int1 = str.length(); //int1= 5;

int int2= "World".length(); //int2= 5;
```

## 💡 `isEmpty()`, `isBlank()`

`isEmpty()`는 길이가 0인가? <br>
`isBlank()`는 글자라고 칠 만한 것이 있는가? <br>

```java
	String str1 = ""; //진짜 아무것도 없음
        String str2 = " \t\n"; //enter, tab, spacebar있음.

        int int1 = str1.length(); //int1= 0;
        int int2 = str2.length(); //int2= 3;

        //  💡isEmpty : 문자열의 길이가 0인지 여부
        boolean bool1 = str1.isEmpty(); //int1은 0이니까 true
        boolean bool2 = str2.isEmpty(); //int2는 3이니까 false

        //  💡isBlank : 공백(white space)을 제외한 문자열의 길이가 0인지 여부
        boolean bool3 = str1.isBlank(); //str1안에 글자 없음 true
        boolean bool4 = str2.isBlank(); //str2안에도 글자는 없음, true
```

## 💡 `trim()`

글자만 남기고 공백 제거, 글자 사이 공백은 여전히 남아 있음. <br>
그리고 trim해도 원본은 바뀌지 않음. <br>
만약 원본도 바꾸고 싶다면...원래 변수에 바꾼 변수 다시 대입해 주기 <br>

```java
String str4 = str3.trim(); //str3 공백 지워서 str4에 저장, str3은 바뀌지 않았음.
str3 = str3.trim(); //원본도 바꾸기
```

## 💡 `charAt()`

`charAt()`는 **char**을 반환 <br>

```java
String str = "도레미파솔라시";
char ch = str.charAt(0); //도

//가장 마지막 글자
char chLast= str.charAt(str.length() -1); //시
```

## 💡 `indexOf()`

어느 위치에 있는가? <br>
`indexOf()`는 **int**를 반환 <br>
💡 만약 찾고자 하는 문자가 포함이 안 되어 있다면? **-1 반환** <br>

```java
String str= "도레미파솔라시도"

int int1 = str.indexOf('레'); //1;
int int2 = str.indexOf('솔', 4); //index4 이후에 솔 찾음
```

## 💡 `lastIndexOf()`

언제 마지막으로 이 문자 또는 문자열이 등장하는가? <br>

```java
int  int3 = str.indexOf("도"); //7
```

## 💡 `equals()`, `equalsIgnoreCase()`

`equals()`: 대소문자 **구분하여** string 똑같은지 비교 <br>
`equalsIgnoreCase()`: 대소문자 **무시하고** string 똑같은지 비교 <br>

```java
String str_a1 = "Hello World";
String str_a2 = "HELLO WORLD";

boolean bool_a1 = str_a1.equals(str_a2) //false
boolean bool_a2 = str_a1.equalsIgnoreCase(str_a2); //true
```

## 💡 `contains()`

찾는 문자가 포함되어 있는가? <br>

## 💡 `startsWith()`, `endsWith()`

이 문자로 시작하는가? 끝나는가? <br>

```java
 String str_b1 = "옛날에 호랑이가 한 마리 살았어요.";
boolean bool_b5 = str_b1.startsWith("호랑이", 4);
//ture
//4번째 index부터가 "호랑이"로 시작하는지 확인함.
```

## 💡 `matches()`

특정 형식을 유지하는지 확인(이메일, 비밀번호 등) <br>
exmaple: 비밀번호에는 특수문자 1개, 대문자 1개 들어가야 함~ <br>

```java
//이게바로 이메일 형식 확인하는 코드임.
String emailRegex = "^[\\w-\\.]+@([\\w-]+\\.)+[\\w-]{2,4}$";

String str_c1 = "yalco@yalco.kr"
String str_c2 = "yalco.yalco.kr";

boolean bool_c1 = str_c1.matches(emailRegex); //true
boolean bool_c2 = str_c2.matches(emailRegex); //false
```

## 💡 `compareTo()`, `compareToIgnoreCase()`

사전순을 기준으로 양수나 음수를 반환한다. <br>

#### ☑️ 시작하는 값이 같다면, 글자 길이를 파악해서 더 긴지, 짧은지 int반환

```java
	String str_a1 = "ABC";
        String str_a2 = "ABCDE";

        int int_a1 = str_a1.compareTo(str_a1); //똑같은 문자열 비교하니까 0

        int int_a2 = str_a1.compareTo(str_a2); //a1은 3이고, a2는 5니까 a1이 2더 짧음 ➡️ -2

```

#### ☑️ 시작하는 부분 값이 다르다면, 첫 글자의 정수값 차이 반환

숫자가 클수록 사전상 앞에 오는 것이다. <br>

```java
String str_a1 = "ABC"
String str_a4 = "HIJKLMN"

int int_a6 = str_a1.compareTo(str_a4);
// int_a6: -7
//ABCDEFGH 니까 A는 1번, H는 8번.
// 1 - 8 = -7
```

## 💡 `toUpperCase()`, `toLowerCase()`

대문자, 소문자로 반환 <br>
⭐️ 만약 한 String에서 다른 String을 대소문자 상관없이 포함하고 있는지 알고 싶다면? <br>
두 String 모두 `toUpperCase()`한다음 `contains`쓰기 <br>

## 💡 `concat()`

string 뒤로 이어붙여 이어주기 <br>

```java
String str_a1 = "밥 먹고";
String str_a2 = "똥싸고";

String str_a3 = str_a1.concat(str_a2);
```

### `concat()` 🆚 `+`

```java
String str_a3 = str_a1.concat(str_a2);
String str_a4 = str_a1 + str_a2;

boolean bool_b1= str_a3.equals(str_a4);
//true
//그냥 + 로도 문자열 이어붙일 수 있음. concat이랑 같은 기능.

//그러나 concat에는 문자열만 이어붙일 수 있음, 다른 datatype은 ❌
//+는 문자열 아닌 다른 datatype도 이어붙일 수 있음 ⭕️
String str_b1 = "ABC";
String str_b2 = str_b1 + true + 1 + 2.34 + '가';
String str_b3 = str_b1.concat(true); //❌
```

### ⭐️ 메서드 체이닝

여러 메서드를 이어서 사용하는 것 <br> <br>
문자열을 반환하기 때문에 또 그 문자열에 메서드를 사용할 수 있는 것이다. <br> <br>
만약 메서드가 문자열이 아닌 다른 data type을 반환한다면 사용할 수 없는 기능 <br> <br>

```java
String str_a6 = str_a1
                .concat(str_a2)
                .concat(str_a1)
                .concat(str_a2);
//밥 먹고 똥 싸고 밥 먹고 똥 싸고
```

## 💡 `repeat()`

<br> <br>
문자열을 주어진 정수만큼 반복 <br> <br>
<br> <br>

## 💡 `substring()`

~번째 문자부터 (~번째 문자까지) 잘라서 반환 <br> <br>

```java
String str_b1 = "대한민국 다 job 구하라 그래";
String str_b3 = str_b1.substring(7, 10); //job
```

## 💡 `replace()`, `replaceAll()`, `replaceFirst()`

주어진 앞의 문자(열)을 뒤의 문자(열)로 치환 <br>

```java
String str_c3 = "밥 좀 먹자, 응? 야, 밥 좀 먹자고 밥 밥 밥";
String str_c4 = str_c3.replace('밥', '빵');
```

## 💡 `toCharArray()`

문자열을 분할하여 문자의 배열로 반환 <br>

```java
String str1 = "가나다라마";
String str2 = "010-1234-5678";
char[] chAry1 = str1.toCharArray();
//[가, 나, 다, 라, 마]
```

## 💡 `join()`

문자열 배열의 요소들을 주어진 기준으로 하나로 이어 붙임. <br>

```java
String[] strings = {"가", "나", "다", "라", "마"};

String join1 = String.join(", ", strings);
//"가, 나, 다, 라, 마 "
String join2 = String.join("-", strings);
//"가-나-다-라-마"
String join3 = String.join(" 그리고 ", strings);
//"가 그리고 나 그리고 다 그리고 라 그리고 마"
```

## 💡 `split()`

주어진 기준으로 (~개까지) 분할하여 문자열 배열로 반환 <br>

```java
String str1 = "가나다라마";
String str2 = "010-1234-5678";
String[] strAry1 = str1.split("");
//["가", "나", "다", "라", "마"]
String[] strAry2 = str2.split("-");
//"-"을 기준으로 분할해서 배열로 만드세요.
//["010", "1234", "5678"]
```
