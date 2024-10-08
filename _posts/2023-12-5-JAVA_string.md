---
title: Char/ String
categories: [JAVA, JAVA_Basics]
tags: [char, string, ofvalue, parse, literal, instance, format] # TAG names should always be lowercase
---

## ✅ Char

- one letter
- 16-bit Unicode
- can show letter, number, symbol
- 단일값

## ✅ String

- several letters
- several `chars`
- can be caculated
- 문자들의 연속적인 값

데이터 타입에 지정된 메모리 값이 매번 달라서 정할수가 없음 ➡️ 그래서 특별한 type <br>
class instance와 같은 `reference type` <br>
string의 각 문자도 unicode을 적용받는다. <br>

## 💡 `.equals` method

instance가 같은지 비교하려면 `.equals`method를 사용해야 한다. <br>
`==` 같은 종이인가? 같은 종이에 적힌 같은 글인가? (메모리값 비교) <br>
`equals` 같은 글이 적혀 있는가? (데이터 값 자체를 비교) <br>

## 🆚 Char and String

`char`은 문자, `String`은 문자열이다. <br>

#### **1. 차이점 1**

`char`은 `int`로의 형 변환이 가능하다. <br>
모든 알파벳에는 UNICODE 번호가 있기 때문이다. <br>
**encoding:** 문자 ➡️ 유니코드 값(숫자) <br>
**decoding:** 유니코드 값(숫자) ➡️ 문자 <br>

`char`을 `int`로 형 변환 <br>

```java
//문자 ➡️ 유니코드 값(숫자)
char ch_a1 = 'A';
int int_a1 = (int) ch_a1; //65, explicit casting
//유니코드 값(숫자) ➡️ 문자
int intA= 65;
char charA= (char)intA;
```

그래서 char에다가 `'A'+1;`하면 a보다 1 유니코드 큰 b가 나온다!!! 대박씡기 <br>
하지만 String은 그냥 문자열이니까...A1나온다. <br>
그리고 char에 숫자 더하고 뺄 수도 있음. <br>
char은 숫자이기도 하니 서로 비교도 가능.

```java
        char a = 'A';
        char b= 'A'+1; //'B' 66
        String sString= "A";
        String a1String= "A" +1; //A1

        char ch6 = '가' + 1; //각

        boolean whoIsBigger= 'A' > 'a'; // 65> 90 false
```

#### **2. 차이점 2**

`char`은 empty불가능 <br>
`String`은 가능 <br>

## 🆚 literal and instance

**literal**: Constant Pool에 저장 <br>
**instance**: Heap에 저장 <br>

literal로 생성 시, String Constant Pool이라는 곳에 저장된다. <br>
그리고 같은 문자열이 적혀있으면 같은 곳을 가리키고 있다. <br>

```java
String str1= "Cat" //literal, Constant Pool에 저장
String str2= new String("Cat") //instsance, Heap에 저장
```

```java
//literal로 생성
	String hl1 = "Hello";
        String hl2 = "Hello";
        String wld = "World";

        //  리터럴끼리는 == 을 사용하여 비교 가능
        boolean bool1 = hl1 == hl2; //true
        boolean bool2 = hl1 == wld; //false
```

   <br>
반면, instance로 생성되면 새로 생성되어 각각 자리를 차지한다.    <br>
reference type이기 때문이다.     <br>
그래서 같은 내용이 적혀있다고 하더라도 주소가 다르기 때문에 다르다고 판단된다.    <br>
만약 `hl3 == hl4`한다면, 같은 주소를 가지게 되는 것이다. <br>
그래서 hl3이 바뀌면 hl4도 바뀌는 등 서로 영향을 주고받는다.    <br>

```java
//instance로 생성
        String hl3 = new String("Hello");
        String hl4 = new String("Hello");
        String hl5 = hl4;

        //  💡 인스턴스와 비교하려면 .equals 메소드를 사용해야 함
        //   특별한 경우가 아니면 문자열은 .equals로 비교할 것
        boolean bool3 = hl3 == hl4;  //false

        boolean bool4 = hl1.equals(hl2); //true
        boolean bool5 = hl1.equals(hl3); //true
        boolean bool6 = hl3.equals(hl4); //true
        boolean bool7 = wld.equals(hl2); //false

        //  같은 곳을 참조하는 인스턴스들
        boolean bool8 = hl4 == hl5; //true
```

<img width="506" alt="스크린샷 2023-12-05 오후 11 23 36" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/ddb10a0f-c66e-4bf5-ac3a-32417d33d90e">

## ✅ operator +

```java
        // + 연산자: 이어붙여진 결과를 반환
        String str_b3 = str_b1 + str_b2;
```

### operator +=

이어붙이기 기능 <br>
하지만 -=기능은 없음 <br>
string아닌 값들도 string으로 만들어서 이어붙이기 가능하다. <br>

```java
String stringStick = "Hello" + 123 + 3.14f + true + 'A';
```

## ✅ 형 변환

#### 💡 other data type ➡️ `String.valueOf()`

```java
String str1 = String.valueOf(true); //true를 String으로
String str2 = String.valueOf(123); //123을 String으로

//또는 더 간단하게
//아까 이어붙이기 operator +=할 때 string붙이면 string으로 자동변환해주니, 아무것도 없는 string "" 붙이면 string으로 변환됨.
String str6 = true + "";
```

#### 💡 string ➡️ other data type `parse`

그런데 만약 변환하려는 string값이 그 데이타 타입에 걸맞지 않는다면, 불가능하다. <br>

```java
String str123 = "123";

//  문자열을 정수 자료형으로 변환하기
byte bytNum = Byte.parseByte(str123);
short srtNum = Short.parseShort(str123);
int intNum = Integer.parseInt(str123);
long lngNum = Long.parseLong(str123);
boolean bool1 = Boolean.parseBoolean("true");

boolean bool2 = Boolean.parseBoolean("하나둘셋"); //불가능, 하나둘셋은 참도 거짓도 아니니까
```

## ✅ formatting

#### ⭐️ formatted

```java
String str1 = "%s의 둘레는 반지름 X %d X %f입니다.";

 String circle = "원";
int two = 2;
double PI = 3.14;

String str2 = String.format( "%s의 둘레는 반지름 X %d X %f입니다.", circle, two, PI)
String str2 = String.format(str1, circle, two, PI)

//formatted
//바로 그 배열에다가 변수 집어넣기
String.str3= "%s의 둘레는 반지름 X %d X %f입니다.".formatted(circle, two, PI);
String str3 = str1.formatted(circle, two, PI);
```

#### printf

```java
System.out.printf("%s의 둘레는 반지름 X %d X %f입니다.%n", circle, two, PI);
System.out.println(str1.formatted(circle, two, PI))
//두 print 결과 똑같다
```

#### string %s, %S

```java
String str1= "Happy";

String result;

result= String.format("문자 %s, %S", str1, str1);
System.out.println(result); //result: 문자 Happy, HAPPY
```

#### ⭐️ 다양한 formatting

```java
String[] strFormats = {
                "%s",
                // 1. 기본
                //Hello 하이염
                "%9s",
                // 2. 자리 확보
                //     Hello       하이염
                "%.2s",
                // 3. ~글자만
                //He 하이
                "%9.2s",
                // 4. 9개 자리 만드는데 2개만 보여줘
                //        He        하이
                "%-9s",
                // 5. 왼쪽 정렬
                //Hello     하이염
        };
```

#### Int %d, %05d

```java
int int1= 123;

String result;

result= String.format("숫자 %d", int1);
System.out.println(result); //result: 숫자 123
```

#### ⭐️ %05d: 5자리 숫자로, 부족하면 0넣어서 채워

```java
int int1= 123;

String result;

result= String.format("숫자 %05d", int1);
System.out.println(result); //result: 숫자 00123
```

```java
        String[] intFormats = {
                "%d",
                // 1. 기본
                //12 2345 67890 -1234567
                "%13d",
                // 2. n 자리수 확보, 오른쪽 정렬
                //            12          2345         67890      -1234567
                "%013d",
                // 3. 빈 자리수 0으로 채움
                //0000000000012 0000000002345 0000000067890 -000001234567
                "%+13d",
                // 4. 양수는 앞에 + 붙임
                //           +12         +2345        +67890      -1234567
                "%,13d",
                // 5. 쉼표 사용(3자리수마다)
                //            12         2,345        67,890    -1,234,567
                "%-13d",
                // 6. 자리수 확보, 왼쪽 정렬
                //12            2345          67890         -1234567
                "%+,013d"
                // 7.+000000000012 +00000002,345 +00000067,890 -0001,234,567
        };
```

#### float %f

```java
float myfloat= 123.456789f;

        String result;

        result= String.format("실수 %f, %.1f, %.2f, %.3f", myfloat, myfloat, myfloat, myfloat);
        System.out.println(result); //result: 실수 123.456787, 123.5, 123.46, 123.457
```

#### ⭐️ 다양한 formatting

```java
String[] fltFormats = {
                "%f",
                // 1. 기본 (소수점 6자리, 0으로 메움)
                //1.200000 123.456000 1234.123457 -123.456700
                "%.2f",
                // 2. 소수점 n자리까지
                //1.20 123.46 1234.12 -123.46
                "%13.2f",
                // 3. 13자리 정수자리 확보, 소수자리 제한
                //          1.20        123.46       1234.12       -123.46
                "%,f",
                // 4. 쉽표 붙이기
                //1.200000 123.456000 1,234.123457 -123.456700
                "%+013.2f",
                // 5. 양수 표시하고 13자리 나타내고 모자르면 0붙여
                //+000000001.20 +000000123.46 +000001234.12 -000000123.46
                "%-13.2f",
                // 6. 왼쪽 정렬하고 소수 2자리까지만 나타내
                //1.20          123.46        1234.12       -123.46
        };
```

#### char %c, 줄바꿈 %n
