---
title: Collection Framework_Array, Node
categories: [JAVA, JAVA_Basics]
tags: [list, framework, collection] # TAG names should always be lowercase
---

## ✅ Collection Framework

### ✔️ 각 요구상황에 적합한 자료구조는 다르다.

핵심요소: **가장 자주 발생하는 로직**이 어떤 성격인가?
예를 들어, 고객이 줄을 서는 상황(ArrayLsit)과 학생 성적 처리하는 상황(LinkedList)은 필요한 자료구조는 다를 것이다.
고려요소

- 적합한 용량인가?
- 내 의도에 맞게 사용하기 쉬운 구조인가?

### ✔️ java.util 패키지

Collection Framework은 java.util 패키지 안에 속해 있음.

### ✔️ 구성 상위 인터페이스

대부분 **generic programming** 구현한다는 것이 특징

<img width="801" alt="image" src="https://github.com/soheeparklee/sc_project_carrotMkt_improved/assets/97790983/b588ab3c-6f27-4224-91d4-ba697e4ef0d1">

#### ☑️ Collection interface

interface: **collection**, list, set
class: array list, vector, linkedlist, hashset, treeset
인터페이스는 스스로를 객체화하지 못하니 클라스를 통해 객체화

#### ☑️ Map interface

interface: **map**
class: hashtable, properties, hashmap, treemap

## ✅ Collection Framework from computer perspective

### ✔️ Data: RAM을 차지하고 있는 집

Data는 RAM 위에서 주소를 가지고 집을 구성하고 있음.

### ✔️ 자료구조: 특정 규칙으로 묶어놓은 동네

- 🏢 Array 구조: 집을 모아 일렬로 쭉 세운 동네, 이웃집끼리 붙어있는 아파트 같음
- ⛺️ Node 구조: 떨어져있는 집들끼리 연락처 공유해 연결, 유목 민족의 게르같은 동네

### ✔️ RAM에서 Data를 가져온다

집의 주소를 받아온다.
= 택배원이 매우 빠르게 택배를 주고받아 오는 것

## 🏢 Object Array

예를 들어 Array List <br>

각 집: 연속적인 메모리 주소(아파트 이웃처럼)<br>
그래서 내 이웃의 주소도 바로 알 수 있다(+1호 하면 되니까) 물어볼 필요도 없음.<br>
첫 번째 집의 주소만 알아도 다른 집들 주소를 다 알 수 있다.<br>
⬇️<br>
그래서 택배원이 **매우 빠르게** 주소 파악해 데이터 주고받기 가능<br>

#### 👍🏻 Array 구조 데이터 접근 방식: **인덱싱**

인덱싱: array의 index에 접근하는 것
한 아파트의 101호 주소를 아는데, 104호 집 주소를 알아 접근하는 것
인덱싱이 가능하므로 빠르게 인덱스에 접근 가능하다.

#### 👎🏻 Array 구조 데이터 추가 및 삭제 방식

새로운 집들이 입주하거나 퇴거한다면 아파트 공간이 부족해 새로 건설하거나, 공실이 많으면 부수고 작게 **다시 만들어야** 함. <br>재건축.
새로운 인덱스를 추가, 삭제할 때는 비효율적<br>

## ⛺️ Node

예를 들어 Linked List<br>

#### ✔️ pointer: 다른 집 연락처

`Node<E> next;`<br>
각 집이 앞, 뒤의 집 연락처만 소지<br>

#### 👎🏻 Node 구조 데이터 접근 방식

택배원은 모든 집의 주소를 알 수가 없음.<br>
대장집A한테 E집 가고 싶은데요, 그러면 대장집이 먼저 B집 주소 알려줌. <br>
B집한테 가서 물어보면 C집이 알걸? C한테 물어봐. <br>
C는 D주소밖에 모름. D한테 물어보니 마침내 E의 주소 알고 있음. <br>
이렇게 물어물어서 주소를 찾아갈 수 있음. 택배원이 집 찾는데 **상대적으로 느림**<br>

#### 👍🏻 Node 구조 데이터 추가 및 삭제 방식

새로운 집들이 합류, 탈퇴하고자 한다면 고정된 호실이 아니라 연락처만 교환하면 되니 매우 간단하다. <br>

## Array 🆚 Node (Collection의 두 가지 근간 structure)

#### 🏢 Array

👍🏻 빠른 인덱스 기반 접근 가능
👍🏻 메모리 공간 효율성이 높음(따닥따닥 붙어있으니 RAM많이 차지 안함)
👎🏻 크기 조정 어려움
👎🏻 데이터 삽입, 삭제하는데 들어가는 비용 높음

#### ⛺️ Node

👍🏻 동적 크기 조정 가능
👍🏻 삽입 및 삭제가 효율적
👍🏻 구조 변경 용이
👎🏻 링크 필드 참조로 접근해야 한다.
👎🏻 포인터 사용으로 메모리 추가 사용
