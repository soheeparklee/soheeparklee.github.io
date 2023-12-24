---
title: Collection Framework_Map/ Set
categories: [JAVA, JAVA_Basics]
tags: [] # TAG names should always be lowercase
---

## ✅ Map

어떤 **key**를 기준으로 **value**를 알아내는 것
순서 **고려 안 함**

구조: key-value
용도: key를 기준으로 value검색
구현체:

- HashMap: Array 구조 기반
- TreeMap: Node 구조 기반

## 💡 Map method

```java
public class MapInterfaceTest {
    public static void main(String[] args) {
        //Map 정의
        Map<String, Integer> fruitMap= new HashMap<>();
        //💡put(key, value) 특정 키에 해당하는 값 추가, 이미 키가 존재하면 새로운 값으로 대체, 이전 값은 반환
        fruitMap.put("Banana", 5);
        fruitMap.put("Cherry", 3);
        fruitMap.put("Tangerine", 10);
        fruitMap.put("Grape", 17);

        System.out.println(fruitMap); //{Cherry=3, Tangerine=10, Grape=17, Banana=5}
        //순서 상관 없어서 매번 출력할 때마다 순서 달라진다.

        //💡get(key) 주어진 키에 대응하는 값 반환, 키가 없으면 null
        Integer bananaCount= fruitMap.get("Banana"); //5
        Integer appleCount= fruitMap.get("Apple"); //null

        //💡containsKey(key) 주어진 키가 존재하는지 확인
        Boolean isApple= fruitMap.containsKey("Cherry"); //true
        Boolean isMango= fruitMap.containsKey("Mango"); //false

        //💡remove(key) 제거
        fruitMap.remove("Banana"); //{Cherry=3, Tangerine=10, Grape=17}

        //💡size()
        int mapSize= fruitMap.size(); //3

        //💡keySet() 모든 키들을 set으로 반환, 반환된 set는 Map의 키들의 집합, value는 몰라도 괜찮아
        System.out.println(fruitMap.keySet()); //[Cherry, Tangerine, Grape]
    }
}
```

## ✅ Set(Collection)

**순서는 고려 안하고** 목록을 **중복 없이** 나열해두고 있는지 없는지 확인하기
용도: 고유한 요소 **검색**

구현체

- HashSet: Array구조 기반
- TreeSet: Node 구조 기반

## 💡 Set method

```java
public class SetInterfaceTest {
    public static void main(String[] args) {
        //set interfece
        Set<String> fruitSet= new HashSet<>();

        //💡boolean add(E element) 요소 추가, 성공하면 true, 이미 요소 있으면 false
        //❗️중복 add는 안 된다!
        fruitSet.add("Pear");
        fruitSet.add("Tomato");
        fruitSet.add("Melon");
        fruitSet.add("Watermelon");
        fruitSet.add("Watermelon"); //두 번 추가해도 중복 추가 ❌ List는 중복 추가 가능 ⭕️
        System.out.println(fruitSet);
        //[Pear, Watermelon, Tomato, Melon]
        //순서 상관 없이


        //💡boolean remove(Object element)
        fruitSet.remove("Watermelon"); //[Pear, Tomato, Melon]
        System.out.println(fruitSet);

        //💡boolean contains(Object element)
        boolean isPear= fruitSet.contains("Pear"); //true
        boolean isBanana= fruitSet.contains("Banana"); //false

        //💡int size()
        int setSize= fruitSet.size(); //3

        //💡boolean isEmpty()
        boolean isSetEmpty= fruitSet.isEmpty();

        //💡void clear()
        fruitSet.clear(); // []
    }
}

```

## ✅ Hash

### Hash함수:

임의의 크기를 가진 데이터를 **고정된 크기(길이는 같게)**의 **고유한 값**으로 변환하는 함수

### 사용처

1. 데이터 무결성 검사
2. 데이터 암호화: 비밀번호 암호화
3. 데이터 검색: Hash함수 고유성 사용

```java
// 🔒 hashCode class
// public class HashCode {
//     public static String hashString(String input) {
//         try {
//             // MessageDigest 인스턴스 생성 (해시 알고리즘으로 SHA-256 선택)
//             MessageDigest digest = MessageDigest.getInstance("SHA-256");

//             // 입력 문자열을 바이트 배열로 변환하여 해시 함수에 전달
//             byte[] hashBytes = digest.digest(input.getBytes(StandardCharsets.UTF_8));

//             // Base64로 인코딩하여 해시된 문자열 반환
//             return Base64.getEncoder().encodeToString(hashBytes);
//         } catch (NoSuchAlgorithmException e) {
//             e.printStackTrace();
//             return null;
//         }

//     }
        //💡 hash로 비밀번호 데이터 암호화
    public static void main(String[] args){
        String ps1= "123qwe";
        String hashPS= hashString(ps1);
        System.out.println(hashPS); //+/s4bv6mfoFvLdoKjJSpjrIDdXrrs/VfGDdVoZLURGc=

        //💡 hash로 데이터 검색
        long hashCode= Objects.hashCode(ps1);
        System.out.println(hashCode); //1450636173
        // 언제나 숫자의 정수값을 반환한다.
        // 모든 객체가 고유의 번호를 가지기 위함
        //그래서 객체에 hash적용할 때는 고유의 id값을 준다.
    }

}

```

### 객체에 HASH씌우기

객체에 hash씌우고자 할 때는 그냥 cutomer에 hash씌우면 모든 cutomer이 hash 똑같을 것임
따라서 cutomer마다 고유의 값을 하나 주고(CustomerID) 거기에 대해 hash

```java
@Override
public int hashCode(){
    return Objects.hashChode(this.CustomerID);
}

Customer customer1= new Customer("ID123", "Kim");
Customer customer2= new Customer("ID456", "Lee");
```

## ✅ HashMap, HashSet

1️⃣ Array구조
2️⃣ 객체의 `hashCode()`호출
3️⃣ Array구조 사이즈로 나머지 "%" 적용

<img width="444" alt="스크린샷 2023-12-21 오후 9 28 07" src="https://github.com/soheeparklee/sc_project_carrotMkt_improved/assets/97790983/81a3bb48-3d0d-4232-9e3b-c810ffab697e">

<img width="430" alt="스크린샷 2023-12-21 오후 9 28 33" src="https://github.com/soheeparklee/sc_project_carrotMkt_improved/assets/97790983/a2e31e62-1a18-444b-98f0-ff1343cf814f">

## ✅ TreeMap, TreeSet

### ☑️ 링크필드가 2개인 Node 구조 구현체

한 집당 연락처 2개 가질 수 있는 구조

### ☑️ BST 자료구조 사용(Binary Search Tree)
