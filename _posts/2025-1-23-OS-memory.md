---
title: KOCW_Memory Management
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ Memory

- memory는 주소를 통해서 접근하는 저장장치이다.
- memory management는 `하드웨어`가 담당한다.

- `32bit`주소체계에서는 `2의 32제곱`가지의 서로 다른 메모리 위치를 구분할 수 있다
- `64bit`주소체계에서는 `2의 64제곱`가지의 서로 다른 메모리 위치를 구분할 수 있다
- 컴퓨터에서는 `byte`단위로 메모리 주소를 부여한다
- 메모리는 효율적인 운영을 위해 일련의 영역을 묶어서 사용한다
- 보통 `4KB`(`2의 12byte`)단위로 묶는데, 이를 `page`라고 한다

```
- 서로다른 `n`군데를 구분하기 위해서는 `n = 2의 m제곱`했을 때 `m bit`
- `N bit`로 구분 가능한 서로 다른 위치는? `2의 N제곱`개
```

## ☑️ 주소의 종류

- ✔️ **Logical address(virtual memory)**
- 프로그램이 실행되어 메모리에 적재되었을 때
- 프로그램이 _독자적으로_ 가지는 주소 공간
- `가상 메모리`

- `CPU`는 프로세스마다 독립적으로 가지는 `Logical address`에 근거해 명령을 실행한다

- 프로그램마다 가상 메모리를 가진다.
- 따라서 각 프로세스마다 0번지부터 시작

- ✔️ **Physical address**
- 메모리에 실제로 올라가는 주소
- 보통 물리적 메모리의 낮은 주소 영역에는 `OS`가 올라가고
- 높은 주소 영역에는 사용자 프로세스들이 올라간다

```
프로그램 A가 디스크에 저장되어 있음
프로그램 A 실행 ➡️ 프로세스 A
프로세스 A의 가상 메모리 주소 공간 가지게 됨
가상 메모리 주소 ➡️ 주소 변환 ➡️ 물리적 주소
물리적 주소가 메모리 위에 올라간다
```

## ✅ Address Binding

> `logical address`를 `physical address`로 `mapping`해 주는 것

<img width="417" alt="Image" src="https://github.com/user-attachments/assets/8d0b0cf7-c557-4c41-9a8c-19ae37a77710" />

```
프로그램이 실행되기 위해서는 해당 프로그램이 물리적 메모리에 올라가 있어야 한다

또한 CPU가 기계에 명령을 수행하기 위해서
논리적 주소를 통해 메모리 참조를 하게 되면
논리적 주소가 물리적 메모리의 어느 위치에 매핑되는지를 확인해야 한다

이렇게 프로세스의 logical address를 physical address로 연결시켜주는 작업을
주소 바인딩이라고 한다
```

- 💡 주소 변환은 `하드웨어`가 담당한다.
- 운영체제는 주소 바인딩과 무관하다
  <br>

- 프로그래머가 바라보는 소스코드 메모리 주소: `symbolic address`
- 프로그램마다 독자적으로 가지는 메모리 공간: `logical address`
- 프로그램이 메모리에 올라가 실행되면: `physical address`
- ➡️ 가상 주소와 물리적 주소 간 주소 변환이 필요하다.

## ✅ Types of address binding

> 어떤 시점에 주소 바인딩을 할 것인가? <br>
> logical address가 physical address로 바뀌는 **시점**에 따라 3가지로 구분 <br>

<img width="492" alt="Image" src="https://github.com/user-attachments/assets/af7d8d2d-bc61-4bf3-b3ab-10f8da0e802b" />

#### ✔️ **Compile Time Binding**

- `compile`시 해당 프로그램의 `physical address`가 결정됨
- 프로그램이 절대주소로 적재된다는 뜻에서 `Compile Time Binding`방식은 `absolute code`를 생성한다고 함
- 컴파일러는 절대 코드 `absolute code`생성
- `physical address`가 0번지부터 올라감(원래 OS가 0부터 올라가야 함)

- 👎🏻 비효율적
- 👎🏻 물리적 메모리의 위치/시작 위치 변경하고 싶으면 재컴파일해야 한다
- 👎🏻 컴퓨터에서 단 한 개의 프로그램만 실행된다면 의미가 있으나, 현대 컴퓨터에서는 잘 사용❌
  <br>

#### ✔️ **Load Time Binding**

- 프로그램의 *실행이 시작*되는 시점에 `physical address`부여
- 프로그램 시작과 메모리 부여, 이후 바뀌지 않음
- `Loader`의 책임 하에 `physical address`부여
- 프로그램이 종료될 때까지 물리적 메모리 상에 위치 고정
- 컴파일러가 재배치가능코드`relocatable code`를 생성한 경우에 가능한 바인딩 방식

- 💡 `Loader`: 사용자 프로그램을 메모리에 적재시키는 프로그램
  <br>

#### ✔️ **Execution time binding(=Run time binding)**

- 프로그램이 실행되는 도중에도 그 프로그램이 위치한 `physical address`이 바뀔 수 있는 바인딩 방식
- 수행이 시작된 이후에도 프로세스의 물리적 메모리 상 위치를 옮길 수 있음
- CPU가 주소를 참조할 때마다(메모리에 접근할 때마다) 해당 데이터가 `physical address`의 어느 위치에 있는지 `address mapping table`을 통해 `binding`을 점검해야 한다
- 메모리 위치가 실시간으로 바뀔 수 있으니까
- 하드웨어적인 지원이 필요하다

  - `base register`
  - `limit register`
  - `MMU`

- 🆚 Load Time Binding은 프로세스 실행 중 메모리 상 위치 변경 불가능
  <br>

- ❓ **왜 CPU는 `logical address`를 바라보는가?**
- CPU는 기계어를 실행할텐데,
- 기계어는 `compile`을 통해 만들어짐
- 그리고 `compile`하면 `logical address` 생성
- 그리고 이 `logical address`이 `physical address`안에 들어가서 실행되므로
- CPU는 `logical address`를 바라본다.

## ✅ MMU

> Memory Management Unit <br>
> 주소변환을 하는 하드웨어 장치<br>

- `logical address`를 `physical address`로 매핑해주는 `hardware device`

#### ☑️ **MMU scheme**

- 사용자 프로세스가 CPU에서 수행되며 생성해내는 모든 주소값에 대해 `base register(relocation register)`의 값을 더한다.
- CPU가 특정 프로세스의 `logical address`를 참조하려고 할 때 `MMU`는 그 `logical address`에 `base register(relocation register)`의 값을 더해서 최종 `physical address`를 알아낸다

- ✔️ **Relocation register(base register)**

  - 프로세스의 `physical address` 시작 주소를 가지고 있다

- ✔️ **Limit register**

  - 현재 CPU에서 실행중인 프로세스의 `logical address`의 최댓값
  - 즉 프로세스의 크기를 담고 있다
  - 다른 프로세스 주소 공간에 침범하는 것을 막기 위해 `limit register`사용
  - 자신의 주소 공간을 넘어서는 메모리 참조를 하려고 하는지 체크하기 위해 사용

<br>

- ❓ **`limit register`는 왜 필요할까? 왜 굳이 프로그램의 크기를 알고 있어야 할까?**
- 만약 이 프로그램이 악의적인 프로그램이라서 잘못된 요청을 할 수 있음
- 😠 자신의 주소 공간이 아닌 다른 프로그램의 주소공간을 요청할 수 있음!
- 예를 들어 위 예시에서, `logical address` 5000번을 요청 ➡️ 자신의 주소 범위 3000보다 큼
- 그러한 요청을 차단하기 위해서 프로그램의 크기를 알고 있어야 한다.
  <br>

- ❓ 그러면 `MMU scheme`에서 **CPU 또는 user program**는 어디를 바라볼까?
- CPU 또는 user program은`logical address`만을 다룬다.
- 실제 `physical address`를 볼 수 없으며 알 필요도 없다

## 📌 Dynamic Relocation

> utilize hardware to convert virtual addresses into physical addresses during runtime

- 프로그램이 실행되면 통째로 메모리에 올라간다고 가정
- `MMU scheme`에서는 `context switching`으로 CPU에서 실행중인 프로세스가 바뀔 때만다
- `base register(relocation register)`의 값을 그 프로세스에 해당되는 값으로 **재설정**

<img width="480" alt="Image" src="https://github.com/user-attachments/assets/a967632e-597d-4ae5-9702-ee02ed8845f0" />

- CPU가 `logical address` 346번을 요청
- `process P1`을 `physical address`에서 찾아보니 14000에서 시작, 17000까지임
- `offset`: 물리적 메모리의 시작 위치인 `relocation register`값으로부터 요청된 위치가 얼마나 떨어져 있는지 나타냄(346)
- `virtual memory`에 보니 346번은 `0+346`번 자리에 있음

- `register`:
  - `relocation register`
  - `limit register`
- `relocation register`: 이 프로그램의 물리적 메모리 시작 위치, `14000`
- `limit register`: 논리적 주소의 범위(이 프로그램의 크기 3000)
- 따라서 `physical address`는 `14000+346 = 14346`
  <br>

<img width="484" alt="Image" src="https://github.com/user-attachments/assets/b901362a-225b-44ae-ba83-9c3d072c3e37" />

- CPU가 `logical address`를 요청
- `MMU`는 `limit register`를 사용해 요청이 내 주소공간 내에 있는지를 확인
- 만족한다면 `relocation register ➕ logical address` 🟰 `physical address`
- 만족하지 않는다면 trap ➡️ CPU가 운영체제에게 넘어간다.

## 📌 Dynamic Loading

- MultiProgramming환경에서(여러 프로그램이 메모리에 적재)

- 프로세스 전체를 메모리에 한번에 다 올리는 것이 아니라 ❌
- 해당 루틴이 불려질 때 **그때그때** 메모리에 `load` 적재
- 프로그램 중 **현재 실행되는 부분만** 메모리에 `load`
- 💡 `load`: 메모리에 프로그램을 적재하는 것
  <br>

- ❓ **Dynamic Loading은 누가 해주는 걸까?**
- 운영체제
- 원래는 운영체제의 특별한 지원 없이도 가능했음

<br>

- 👍🏻 `memory utilization`향상
- 👍🏻 가끔씩 사용되는 많은 양의 코드인 경우 유용(매번 사용되지 않는 코드: `오류 처리 루틴`)
- 👍🏻 운영체제의 특별한 지원 없이 프로그램 자체에서 구현 가능(OS는 라이브러리 통해 지원 가능)
- 👍🏻 같은 크기의 `physical memory`에 더 많은 프로그램을 적재할 수 있다

- 🆚 Overlays
- Dynamic Loading은 MultiProgramming환경에서 메모리의 이용률을 향상시키기 위해 프로세스의 주소 공간 중 당장 실행에 필요한 부분만을 그떄그때 메모리에 동적으로 적재

## 📌 Overlays

- 메모리에 프로세스의 주소 공간을 분할해 **실제 필요한 정보만을** 메모리에 올림
- 👍🏻 프로세스의 크기가 메모리보다 클 때 사용했음
- 예전에는 메모리 공간이 매우 작았음!
- 그래서 작은 공간의 메모리를 사용하던 *초창기 시스템*에서 하나의 프로세스조차도 메모리에 다 올릴 수가 없을 떄
- 당장 필요한 일부분만 메모리에 올려 실행하고,
- 해당 부분에 대한 실행이 끝나면 나머지 부분 실행
- 수작업으로 프로그래머가 구현하곤 했음

- 운영체제 지원 없이 사용자에 의해 구현
- 👎🏻 manual overlay
- 👎🏻 프로그래밍 매우 복잡

- 🆚 Dynamic Loading과 비슷하나
- 사용목적이 다르다
- Overlays는 과거 물리적 메모리의 크기 제약으로 인해 하나의 프로세스조차도 메모리에 한꺼번에 올릴 수 없을 때 사용했음
- Overlays는 프로그래머가 수작업으로 구현

## 📌 Linking

- 프로그램은 `compile`, `linking`을 통해 **실행 파일**이 만들어진다.

- `linking`: 라이브러리와 내가 만든 코드를 **연결**하는 과정
- `프로그래머다 작성한 코드`를 `compile`하여 생성된 목적 파일 `object file`과
- 이미 `compile`된 `library file`들을 묶어 하나의 실행파일을 생성하는 과정

#### ☑️ **Static Linking**

- **static library**
- `프로그래머다 작성한 코드` + `라이브러리 코드` 모두 합쳐서 실행파일 생성
- 라이브러리가 프로그램의 실행 파일 코드에 **포함됨**
- 👎🏻 실행 파일의 크기가 커짐!
- 👎🏻 동일한 라이브러리를 각각의 프로세스가 개별적으로 메모리에 올림
- 👎🏻 물리적 메모리 낭비
  <br>

#### ☑️ **Dynamic Linking**

> linking을 실행 시간(execution time)까지 미루는 기법

- **shared libary**
- `library`가 프로그램의 실행 파일 코드에 _포함되지 않고_ 있다가
- `library`가 **실행시** `link`됨
- 즉, 실행 파일에 `library`가 포함되지 않으며
- 프로그램이 실행되면서 `library`함수를 호출하면, 그제서야 `library link`

- Dynamic Linking을 위해 실행파일의 `library` 호출 부분에 `stub`이라는 작은 코드를 둔다
- 실행하다가 라이브러리를 찾아야 함 ➡️ `stub` 호출
- `stub`역할: `library` 호출 부분에 `library` 루틴의 위치를 찾기

```
library호출  ➡️ stub
stub통해 해당 라이브러리가 메모리에 이미 존재하는지 확인
라이브러리가 이미 메모리에 있으면 ➡️ 그 위치로 가고
없으면 ➡️ 디스크에서 동적 라이브러리 파일을 찾아 메모리에 읽어옴, 수행
- 메모리에 적재할 때는 운영체제의 도움 필요
```

- 👍🏻 다수의 프로그램이 공통으로 사용하는 동일 라이브러리는 메모리에 한번만 적재
- 👍🏻 메모리 사용 효율성

## 📌 Swapping

#### ☑️ Swapping

- 프로세스를 일시적으로 메모리에서 `backing store`로 쫒아내는 것
- 원조 Swapping은 프로세스를 **통째로** 쫒아낸다.
- (🆚 현대 운영체제에서는 일부만 메모리에 올리고 일부만 쫒아냄, swapping 원조랑은 다름)

- 👍🏻 메모리에 존재하는 프로세스의 수를 조절한다
- 👍🏻 Swapping을 통해 `multi programming`의 정도를 조절한다
- 너무 많은 프로그램이 메모리에 올라오게 되면 메모리 양이 지나치게 적어져 시스템 성능 저하
- 따라서 Swapping을 통해 몇몇 프로그램을 디스크의 `backing store`로 쫒아내 메모리에 남아있는 프로그램들에게 실행에 필요한 메모리 공간 보장

#### ☑️ Backing store(swap area)

- `backing store`: `swap area`
- 디스크 내에 파일 시스템과는 별개로 존재하는 일정 영역
- 많은 사용자의 프로세스 이미지를 담을 만큼 충분히 빠르고 큰 저장 공간

#### ☑️ Swap in/Swap out

- 일반적으로 `중기 스케쥴러`(`swapper`)에 의해 `Swap out`할 프로세스 선정
- 프로세스가 `Swap out`되면 `suspended`상태가 된다.

- `Swap out victim`으로 선정된 프로세스에 대해서는 현재 메모리에 올라가 있는 `address space`의 내용을 통째로 `swap area`로 `Swap out`시킨다
  <br>

- **Priority based CPU scheduling algorithm**
- CPU에서 우선순위가 낮은 프로세스를 `Swap out`
  - priority가 낮은 프로세스 `Swap out`
  - priority가 높은 프로세스는 메모리에 올려 놓음

<br>

- `compile time` 또는 `load time binding`에서는 *원래 메모리 위치*로 `swap in`해야 함(메모리 주소가 바뀌면 안 되니까!)
- `execution time binding(run-time binding)`에서는 추후 _빈 메모리 영역 아무 곳에나_ 올릴 수 있음
- 따라서 `Swap out`은 `execution time binding(run-time binding)` 일 때 제일 효율적

- `swap time`은 대부분 `transfer time`(`swap`되는 양에 비례하는 시간)

## ✅ Allocation of Physical Memory

> 물리적 메모리에 주소가 어떻게 할당되는가?

- 메모리는 일반적으로 두 영역으로 나뉘어 사용
  - **OS상주 영역**: `interrupt vector`와 함께 낮은 주소 영역 사용, `OS kernel`이 여기에 위치함
  - **사용자 프로세스 영역**: 높은 주소 영역 사용

<img width="81" alt="Image" src="https://github.com/user-attachments/assets/ff1ff427-469f-4954-beac-e6fd82293681" />

#### ☑️ Fragmentation

- ✔️ **Internal fragmentation**
- 사용자 프로그램이 분할 `partition`보다 _작아서_
- 적재를 하였으나, 메모리 공간이 남음
- `partition`이 내부에서 쪼개짐
- 내부조각

<img width="231" alt="Image" src="https://github.com/user-attachments/assets/4ace85f4-8df9-477f-a1a3-ead120d99a1b" />

- ✔️ **External fragmentation**
- 사용자 프로그램이 분할 `partition 1`보다 _커서_
- 해당 `partition`에 적재를 못함
- 해당 `partition 1`에 들어가지 못하고, 다음 `partition 2`에 들어감
- 그러면 에매한 크기의 `partition 1`은 낭비
- 외부조각

<img width="235" alt="Image" src="https://github.com/user-attachments/assets/9500b561-bb93-4533-b51d-7fa93e6c5cf9" />

## ✅ Contiguous allocation

> 프로그램이 **통쨰로** 메모리에 올라감

- 각각의 프로세스가 물리적 메모리의 _연속적인_ 공간에 적재되도록 하는 것
- 프로그램이 쪼개지지 않고, 통째로 올라감
- 👍🏻 프로그램 주소변환이 비교적 간단(`relocation register`, `limit register`)
- 👎🏻 메모리를 할당하다가 `hole`들이 너무 작게 쪼개지면 아무런 프로세스를 올리지 못하는 문제 발생 가능
- 현대 메모리에서는 자주 쓰이지 않는 방법

- ✔️ Fixed-partition allocation
- ✔️ Variable partition allocation

- ❓ **Contiguous allocation 에서는 프로세스 주소 변환을 어떻게 하나요?**
- 두 개의 register `relocation register`, `limit register` 사용

### 📍 Fixed-size partition allocation

> 물리적 메모리를 몇 개의 영구적 분할 `partition`으로 **미리** 나눔 <br>
> 하나의 분할에는 하나의 프로그램만 적재 가능 <br>

<img width="225" alt="Image" src="https://github.com/user-attachments/assets/9f41e313-1125-447d-aab6-b48e12d238f5" />

- 분할의 크기가 `1. 모두 동일한 방식`과 `2. 서로 다른 방식`이 존재
- 각각의 분할 당 하나의 프로그램 적재
- 👎🏻 융통성이 없다.
- 👎🏻 동시에 메모리에 `load`되는 프로그램 수가 `partition` 수로 고정됨
- 👎🏻 최대 수행 가능 프로그램 크기 제한
- 👎🏻 Internal fragmentation 발생
- 👎🏻 External fragmentation도 발생

```
프로그램A는 분할1에 잘 들어감
프로그램B는 분할2보다는 크고 분할3보다는 작다
그래서 분할3에 들어감
- 분할2: External fragmentation
- 분할3: Internal fragmentation
```

### 📍 Variable-size partition allocation

<img width="240" alt="Image" src="https://github.com/user-attachments/assets/3bd65d27-4a09-4840-be47-96b39a53ec91" />

- `partition`을 미리 나눠놓지 말고,
- 프로그램의 크기를 고려해서 할당
- `분할의 크기`, `개수`가 동적으로 변한다
- 기술적 관리 기법 필요

- ✔️ **Variable partition allocation Problem**
- 동적 메모리 할당 문제
- 👎🏻 External fragmentation 발생
- 이미 메모리에 존재하는 프로그램이 종료될 경우 빈 공간이 발생하는데, 이 공간이 새롭게 시작되는 프로그램의 크기보다 작을 경우 외부조각이 된다.

```
프로그램B가 끝나고 메모리가 비게 되었음
그러나 프로그램D는 그 메모리 분할에 들어가기에는 큼
현재 연속할당이므로, 프로그램은 쪼개져서 들어갈 수 없음
프로그램D는 더 큰 메모리 분할을 할당받고,
프로그램B 메모리 공간은 External fragmentation
```

### 💡 Hole

> 가용 메모리 공간

- `가용공간`은 `사용되지 않은 메모리 공간`으로, 메모리 내 여러 곳에 산발적으로 존재할 수 있음
- 다양한 크기의 `hole`들이 메모리 여러 공간에 _흩어져_ 있음
- 프로세스가 도착하면 수용 가능한 `hole`을 할당

- 운영체제는 다음의 정보를 가지고 있어야 함
  - 할당 공간
  - 가용 공간 `hole`

<img width="394" alt="Image" src="https://github.com/user-attachments/assets/0553c266-7f77-4273-8aee-877e9ac717ef" />

### 📍 Dynamic Storage Allocation Problem

> `Variable partition allocation`에서 `size n`인 요청을 만족하는 가장 적절한 `hole`은 누구인가? <br>
> 사이즈를 만족하는 `hole` 중 어떤 `hole`을 할당해 줄 것인가? <br>

- ✔️ **First Fit**
- `size`가 `n`이상인 것 중 최초로 찾아지는 `hole`을 할당한다.
- 👍🏻 비교적 빨리 결정

- ✔️ **Best Fit**
- `size`가 `n`이상인 가장 작은 `hole`을 찾아 할당
- 👍🏻 공간적인 측면에서 효율적
- 👍🏻 비교적 맞춤형 사이즈의 `hole`을 할당해줄 수 있음
- 👎🏻 `hole`들의 리스크가 크기순으로 정렬되지 않은 경우 모든 `hole` 리스트를 돌면서 탐색해야 함
- 👎🏻 많은 수의 아주 작은 `hole` 생성

- ✔️ **Worst Fit**
- 가장 큰 `hole` 할당
- 👎🏻 마찬가지로 모든 `hole` 리스트를 탐색해야 함
- 상대적으로 아주 큰 `hole`들 생성
- 👎🏻 나중에 진짜 큰 프로세스 오면 할당해 줄 공간이 없음

- 💡 `First Fit`과 `Best Fit`이 `Worst Fit`보다 속도과 공간 이용률 측면에서 효과적인 것으로 판면

### 💡 Compaction

- 💊 External fragmentation 문제를 해결하는 방법
- 사용중인 메모리 영역을 한 군데로 몰고,
- `hole`들을 다른 한 곳으로 몰아 아주 큰 `block`을 만든다.

- 👎🏻 아주 비용이 많이 든다
  - 거의 모든 프로그램의 메모리 공간을 바꾸니까
- 👎🏻 최소한의 메모리 이동으로 `compaction`하는 방법은 아주 복잡한 문제

- `compaction`을 하기 위해서는 `execution time binding(run-time binding)`일 때만 가능

### 💡 Colaescing

- 인접한 조각 또는 빈 영역들을 합치는 방법

### 📍 Buddy system

- 👎🏻 `Fixed-partition allocation`은 메모리에 적재할 수 있는 프로세스 수가 고정되어 있고, 내부단편화 발생
- 👎🏻 ` Variable partition allocation`는 외부 단편화가 발생, 이를 해결하기 위해 `compaction`을 수행해야 함

- 💊 이에 대한 절충안으로 `Buddy system`등장

<img width="554" alt="Image" src="https://github.com/user-attachments/assets/7a608068-9642-48b5-96b8-eb8de7237f3e" />

- 초기 블록은 `1MB`크기의 블록
- `프로세스A`는 `100KB`의 공간 요구
- `1MB` 블록은 `512K`인 `두 개의 버디`로 나누어지고,
- 그 중 첫 번째 버디는 또 `256K`인 `두 개의 버디`로
- 또 그 중 첫 번째 버디는 `128K`인 `두 개의 버디`로 나뉘어진 후,
- 그 중 하나가 `프로세스A`에게 할당된다.

- 다음 `프로세스B`는 `240K`의 공간을 요청하므로, `256K`인 버디를 할당한다.
- 할당 과정에서 블록은 필요에 따라 나눠지고, 합쳐진다.

- `프로세스E`가 해제되는 부분을 보자
- `두 개의 128K 버디`는 `256K 한 개`로 합쳐지고
- 또 다시 두 개의 `256K`가 합쳐져 `512K`가 만들어진다.

<img width="529" alt="Image" src="https://github.com/user-attachments/assets/38a06fea-0010-414f-a358-3615575a0d02" />

- 위 그림은 B가 해제된 직후의 버디 할당 모습을 이진 트리로 나타내고 있는 그림이다.
- 말단 노드는 현재 메모리의 분할 상태를 나타낸다.
- 만일 두개의 버디가 말단 노드라면 적어도 하나는 할당이 되었음을 의미한다.
- 그렇지 않다면 둘은 조금 더 큰 블록으로 합쳐졌을 것이다.

## ✅ Noncontiguous allocation

> 하나의 프로세스가 여러개로 **쪼개져서** 물리적 메모리의 여러 위치에 분산되어 올라가는 방식

- 하나의 프로세스가 메모리의 여러 영역에 _분산되어_ 올라갈 수 있음
- 👎🏻 프로세스가 쪼개져서 메모리에 올라가다보니 프로그램 주소변환을 하기가 어려움
- ✔️ Paging
- ✔️ Segmentation
- ✔️ Paged Segmentation

### 📍 Paging

> 하나의 프로그램을 동일한 크기로 나누어 메모리에 올리기

- 프로세스의 `주소공간`을 **동일한 사이즈**의 `page`로 나눔(일반적으로 `4B`)
- `virtual memory`의 내용이 `page`단위로 `Noncontiguous`하게 저장됨
- 일부는 `backing storage(swap)`에, 일부는 `physical memory`에 혼재해 저장 가능
  <br>

<img width="380" alt="Image" src="https://github.com/user-attachments/assets/0091c36e-ee58-4588-88d3-32fda4f0bb13" />

- 페이징 기법에서는 `physical memory`를 `page`하나가 들어갈 수 있도록 **동일한** 크기의 `page frame`으로 미리 나눔
- `logical memory`를 동일 크기의 `page`로 나누고, `physical memory`도 같은 크기의 `frame`으로 나누어짐
- 모든 가용 `frame`들을 관리

- 👎🏻 Internal fragmentation 발생 가능(메모리를 같은 크기의 `frame`로 쪼개다보면 남는 공간 생길 수도 있으므로)
- 👍🏻 Variable partition allocation Problem이 발생하지 않음(프로세스 주소 공간, 물리적 메모리 모두 같은 크기의 페이지 단위로 나뉘어지기 때문)
- 👍🏻 External fragmentation 발생하지 않음(프로세스가 `frame`보다 크면 쪼개서 들어가면 되니까)
  <br>

- `page table`을 이용하여 `logical memory adress`를 `physical memory adress`로 변환
- 특정 프로세스의 몇 번째 `page`가 `physical memory`의 몇 번째 `page frame`에 들어가있는지에 대한 페이지별 주소 변환 정보를 `page table`이 가지고 있음

- ❓ **Paging에서는 프로세스 주소 변환을 어떻게 하나요?**
- `page table`을 이용
- `몇 번 페이지 번호 page` + `페이지 내에서 어디에 위치 frame(변하지 않음)`

### 💡 Page Table

- `page table entry`가 백만개가 넘는 상황이기 때문에, `Contiguous allocation`처럼 `register` 2개에 주소를 집어넣을 수가 없음!

- 따라서 `page table`자체를 만들고 **메모리에** 올린다.
- `page table`은 `main memory`에 상주

- 프로세스마다 `page table`가 있다
- 그래서 `context switching`이 발생하면 `page table`에 따른 `TLB`가 지워지고 새로 만들어저야 하니 `overhead`가 꽤 크다

- `page table`은 프로세스가 가질 수 있는 `page`의 개수만큼 `주소 변환 엔트리`를 가지고 있어야 함
- 하지만 프로그램의 크기가 항상 `page`의 배수가 된다는 보장은 없기 때문에 프로세스의 주소 공간 중 제일 마지막에 위치한 `page`에서는 내부 조각 발생 가능

  <br>

### 💡 Address Translation Architecture

<img width="358" alt="Image" src="https://github.com/user-attachments/assets/a9175922-072f-4867-878e-130085803884" />

- `logical address` 주소는 `p`와 `d`로 이루어져 있음

- `p`: 페이지 번호, `4kb`
- `page table` 접근 인덱스로 사용

- `d`: 페이지 내에서 어디에 위치하는지 나타내는 `offset`
- 하나의 페이지 내에서의 위치 알려줌
- `d`의 값은 변하지 않는다

- 예를 들어 `p: page 2번` + `d: page 2번 내의 위치`

- `f`: 페이지 인덱스 위치에 있는 엔트리에는 해당 페이지의 물리적 주소상의 기준 주소 `base address`, 즉 시작 위치 저장
- 따라서 `f: 기준 주소 값` + `d: 페이지 내 위치` = `physical address`

- 👍🏻 `p`, `d`의 값만 알면 바로 주소 구할 수 있음
  <br>

### ☑️ 페이지 테이블의 구현

<img width="419" alt="Image" src="https://github.com/user-attachments/assets/849c331b-4888-484e-9b90-ac1000e45484" />

- Page table is a structure for address translation in paging, uploaded on physical memory.

- ❓ **왜 페이지 테이블은 물리적 메모리에 위치하는가?**
- 보통 `logical address`는 `32bit`이다

- `logical address` 주소가 `32bit`인 환경에서
- `프로그램 메모리 공간 VM`이 최대 가질 수 있는 크기는 `2의 32제곱`, 즉 `4GB`
- `page`하나는 `4kb`
- 따라서 하나의 `VM`안에는 주소공간이 `1메가, 100만`개 있을 수 있다
- 😱 페이지의 개수가 프로세스마다 `100만`개가 있는 상황
- 😱 따라서 `page table`에는 `1메가`개수 만큼의 `page table entry`가 필요
- 💊 그래서 `page table`이 `main memory`에 올라가는 것이다

#### ✔️ 페이지 테이블의 두 register

- 현재 CPU에서 실행중인 프로세스의 페이지 테이블에 접근하기 위해 OS는 두 개의 register필요

- `Page-table base register(PTBR)`: 메모리 내에서 `page table`**시작 위치**를 가리킴
- `Page-table length register(PTLR)`: **테이블 크기**를 보관
- `Page-table base register(PTBR)` + `Page-table length register(PTLR)`
  <br>

- 페이징 기법에서 모든 메모리 접근 연산에는 **2번**의 `memory access`가 필요하다

  - 1️⃣ `page table` 접근, 주소 변환을 위해 메모리의 `page table` 접근
  - 2️⃣ `data/instruction` 접근, 변환된 주소에서 실제 데이터 접근 위해 메모리 접근
  - 👎🏻 메모리를 2번 접근해야 하니 속도 저하
  - 💊 `TLB`
    <br>

### 💡 TLB

> Translation Lookaside Buffer

- 💊 주소변환을 전담하는 `cache memory`를 둔다.
- 💊 **가상 메모리 주소를 물리적 주소로 바꾸는 속도 향상을 위해** `cache memory` 즉 `TLB`를 둔다
- 👍🏻 페이지 테이블 접근 오버헤드를 줄이고
- 👍🏻 메모리의 접근 속도 향상
- `page table` 탐색 속도 향상을 위해 `associative register` 혹은 `translation look-aside buffer(TLB)`라 불리는 고속의 `lookup hardware cache` 사용
- `TLB`는 **주소 변환을 빠르게 하기 위한** `cache memory`

- `TLB`에는 빈번히 참조되는 페이지에 대한 주소 변환 정보가 저장되어 있다
- 만약 요청된 페이지 번호가 `TLB`에 있으면 빠르게 `physical address`얻을 수 있음 ➡️ `TLB hit`
- 요청된 페이지의 주소 변환 정보가 없다면 메인 메모리에 있는 `page table`에 가서 물리적 주소를 알아와야 함 ➡️ `TLB miss`

```
- `CPU`안에 `register`이 있고, `CPU`와 `memory`사이에 `cache`가 있다.
- `cache memory`는 메모리와 `CPU`간의 속도 차이를 완충하기 위해 있음
```

<img width="465" alt="Image" src="https://github.com/user-attachments/assets/461bd44c-b7b5-4f33-9f0f-a29c6f21175f" />

```
p: 페이지 번호 p를 주면 page table위에서 p번째에 가서
f: 페이지 frame번호를 얻게 된다
그러면 주소 변환이 끝나서
physical memory의 f번째 프레임에 가서
그 프레임 내에서 d번째 떨어진 위치에 가면
CPU가 메모리에 요청한 내용을 얻을 수 있다

만약 TLB에 요청한 정보가 있다면 cache hit, 빠른 주소 변환
```

- `page table`은 하나의 프로세스를 구성하는 모든 페이지에 대한 주소 변환 정보가 페이지 번호에 따라 순차적으로 들어 있음
- 그래서 페이지 번호가 주어지면 테이블의 시작 위치에서 페이지 번호만큼 떨어진 인덱스에 곧바로 접근해 해당 페이지에 대응되는 프레임 번호를 얻을 수 있었음
- 하지만 `TLB`에서는 프로세스의 모든 페이지에 대한 주소 변환 정보를 가지고 있지는 않기 때문에
- 따라서 이 주소변환이 어떤 `page`에 있는지 알려주는 `frame number`이 필요하다.
- 그래서 `page number`, 이에 대응하는 `frame number`을 _쌍으로_ 가지고 있어야 한다.
- `p`번째 페이지에 대한 주소변환 `f`가 _쌍으로_ 저장되어 있다.

- 👎🏻 `page table`는 프로세스마다 존재하기 때문에
- `context switching`으로 CPU에서 실행되는 프로세스가 바뀌면 `TLB`는 모두 지워버려야 한다.
- 기존 `cache memory`인 `TLB`를 지우고, 새로 만드는 과정에서 `overhead`발생

- 👎🏻 `TLB`는 `cache memory`이기 때문에 모든 주소를 다 담고 있지는 않음 ❌
- `cache memory` 공간이 한정되어있기 때문에, 일부만 알고 있음
- 👎🏻 그래서 페이지 번호 `p`가 있는지 없는지 `TLB`를 모두 탐색해야 한다
- 💊 그래서 모든 `p`를 `parallel하게, 병렬적으로` 찾는다
- 💊 이 역할을 하는 하드웨어를 `associative register`이라고 한다.

- ❓ **`context switching`의 `overhead` 중 메모리와 관련된 대표적인 것으로는 무엇이 있나요?**
- `TLB`를 지우고, 새로 만드는 과정에서 `overhead`가 크게 발생한다

#### `page table` 🆚 TLB

<img width="211" alt="Image" src="https://github.com/user-attachments/assets/1fcbf039-7a81-40c6-b495-6f9aa6b292ae" />

- `page table`: 테이블이기 때문에 `index`가 있어 `p`를 찾을 때 딱 그 부분을 찾을 수 있음
- TLB: `p`가 있는지 없는지 `TLB`를 전부다 탐색해야 한다

- `page table`: 모든 주소를 다 담고 있음
- TLB: `cache memory`이기 때문에 모든 주소를 다 담고 있지는 않음

- `page table`: `p`번째 인덱스에 가면 `f`를 알 수 있음
- TLB: `page number`, `frame number`을 _쌍으로_ 가지고 있어야 한다.

### 💡 Associative register

<img width="159" alt="Image" src="https://github.com/user-attachments/assets/d01d8cc8-6f30-47c8-a595-2d8b1fbdc0d6" />

- `TLB`에서 모든 `p`를 `parallel하게` 찾기 위해 필요한 하드웨어
- 그림에서 화살표가 동시에 여러개 평행으로 그려져 있음
- `TLB`의 `p`탐색 속도 향상

### 💡 Effective Access Time

> 메모리 접근하는 효율적인 시간이란?

- Associative register lookup time: `TLB` 접근 시간
- memory cycle time: 메모리 접근하는 시간 `1`
- Hit ratio: `TLB`를 통해서 주소변환이 이루어지는 비율, `TLB hit` 비율

<img width="433" alt="Image" src="https://github.com/user-attachments/assets/e08d78ba-0de0-4782-8dbe-4a40e9dab945" />

- hit: (메모리 접근 시간 + `TLB` 접근 시간) \* `TLB hit` 비율
- miss: (메모리 2번 접근한 시간 + `TLB` 접근 시간, 접근했지만 찾기 실패) + `TLB miss` 비율
- miss: 결국 `page table`에서 주소변환 한 시간

- 결론: `TLB 접근 시간`이 `메모리 접근 시간`보다 훨씬 적으므로 `TLB hit`할수록 `access time`이 효과적이다

### 📍 Two-Level Page Table

- 현대의 컴퓨터는 `address space`가 매우 큰 프로그램을 지원한다
- `32bit address`사용 시: `2의 32제곱(4G)`의 주소 공간을 가지는 프로그램을 지원할 수 있다

  - `page size`가 `4KB`일 시 `1M`개의 `page table entry`필요
  - 각 `page table entry`가 `4byte`일 시 한 프로세스 당 `page table`을 위해 `1M x 4byte = 4MB`의 메모리 필요
  - 👎🏻 그러면 수행중인 프로세스의 수가 증가함에 따라 ⬆️ 전체 메모리의 상당 부분이 주소변환을 위한 `page table`에 할애되고
  - 실제 사용 가능한 메모리 공간이 크게 감소 ⬇️
  - 👎🏻 또한 대부분의 프로그램은 메모리 주소 공간 중 지극히 일부만 사용하므로 `page table`을 위한 메모리 사용은 심각한 공간 낭비이다

<br>

- 그래서 `Paging`은
- 👍🏻 프로그램을 동일한 사이즈의 `page`로 잘라 메모리에 Noncontiguous하게 올리고
- 👍🏻 사용하는 메모리만 올린다는 장점이 있으나
- 👎🏻 `page` 개수가 프로세스마다 백만개가 넘는다
- 게다가 `page table`은 프로세스마다 각각 존재함
- 엄청난 양의 메모리가 주소변환을 위해 쓰이고
- 👎🏻 `page table`을 저장하기 위한 공간 낭비가 심함
- 👎🏻 심지어 다 쓰이지도 않기 때문에 낭비 심함

<br>

<img width="323" alt="Image" src="https://github.com/user-attachments/assets/e105ea66-55a9-4601-9cc9-930215743eaf" />

#### ☑️ Two-Level Paging

<img width="381" alt="Image" src="https://github.com/user-attachments/assets/180c01e5-d07d-4040-9bcf-7e87dca8d32c" />

- 💊 `page table`자체를 `page`로 구성
- `page table` 하나를 더 뒤서 `page table`을 계층적으로 구성(`서울시-양천구-목동` 처럼)

- Two-Level Paging에서는 주소 변환을 위해 `outer page table`, `inner page table` 두 단계에 걸친 `page table`을 사용
- 사용되지 않는 주소 공간에 대해서는 `outer page table`의 엔트리 항목 값을 `NULL`로 설정
- 그래서 여기에 대응하는 `inner page table`은 생성하지 않음

- 👎🏻 주소변환을 위해 메모리를 3번 접근해야 함
- (주소변환 위해 2개의 테이블 접근 ➕ 실제 데이터 접근 위해 메모리 접근)
- 👎🏻 시간상으로 손해
- 👍🏻 하지만 `page table`에 사용되는 메모리 공간 낭비를 줄여 **공간상으로는 메모리 낭비를 줄일 수 있다**.

### 💡 Address Translation Scheme in Two-Level Page Table

> 2단계 페이지 테이블에서의 주소 변환 과정

<img width="393" alt="Image" src="https://github.com/user-attachments/assets/67b6028b-ae2e-4772-9745-dfdc8a05d761" />

- `logical address`(`32bit`)를 3부분으로 나눈다
  - `p1`: outer page table index, `10bit`
  - `p2`: page of table table index, `10bit`
  - `d`: page offset, 페이지 안에서 얼마나 떨어져 있는가 `12bit`
  - 논리적 주소를 이와같이 세 부분으로 나누어 <p1, p2, d>의 형태로 표시

<img width="481" alt="Image" src="https://github.com/user-attachments/assets/0bdc0a6b-4a9a-4985-86a2-4b46c532c7b3" />

- 먼저 `outer page table`로부터 `p1`만큼 떨어진 위치에서 `inner page table`의 주소를 얻는다
- 다음으로 `inner page table`로부터 `p2`만큼 떨어진 위치에서 요청된 페이지가 존재하는 `frame`의 위치를 얻는다
- 마지막으로 해당 `frame`으로부터 `d`만큼 떨어진 곳에서 원하는 정보에 접근할 수 있다

- 만약 `p1`이 `NULL`이다 ➡️ 저장된 내용 없음
- `p1`가 `NULL`이 아니다 ➡️ `두번째 테이블`의 시작 위치를 가지고 있다.
- `p2`: `두번째 테이블`에서 얼마나 떨어졌는지(`frame`위치)
- `d`: 해당`frame`에서 `d`만큼 떨어진 곳에 물리적 주소로 변환한 결과

### 📍 Multilevel Paging and Performance

- 만약 `address space`가 더 커지면 `Multilevel Paging table`필요
- 👍🏻 프로세스 주소공간을 많이 줄일 수 있다.
- 👎🏻 각 단계의 `page table`이 메모리에 존재하므로, `logical address`의 `physical address`변환에 더 많은 메모리 접근 필요 ➡️ 메모리 접근 횟수 증가
- 💊 `TLB`를 통해 접근 속도 줄일 수 있음

### 💡 Valid, Invliad Bit in a Page Table

<img width="373" alt="Image" src="https://github.com/user-attachments/assets/78fe045a-8621-492a-a893-ce5581c555c9" />

- `bit`가 있어서 이 페이지가 `page table`에 올라가 있는지, 없는지 확인 가능
- `page table`의 `frame number`이 사실은 `물리적 메모리`에 안 올라가 있고 디스크에 내려가 있을 수도 있으니까, 또는 프로그램이 그 메모리를 사용하지 않는 경우도 있으니까
- 진짜 `물리적 메모리`에 있는지 확인하는 `valid-invalid bit`

- `물리적 메모리`에 안 올라가 있고 디스크로 쫒겨나 있는 경우 `invalid`
- 프로그램이 그 메모리를 사용하지 않는 경우 `invalid`
- (프로그램이 그 메모리를 사용하지 않는 경우에도 `page table`에 올라가야 함)

### 💡 Memory Protection

> `page table`의 각 `entry`마다 `Bit`를 둔다.

- ✔️ **protection bit**
- `page`에 대한 접근 권한(`read/write/read-only`) 보호
- 각 `page`가 자신의 `page table`에 대해 어떤 권한을 가지는지 설정

- ✔️ **valid-invalid bit**
- `valid`는 해당 주소의 `frame`에 그 프로세스를 구성하는 유효한 내용이 있음을 의미(잡근 허용)
- `invalid`는 해당 주소의 `frame`에 유효한 내용이 없음을 의미
  - 프로그램이 그 주소 부분을 사용하지 않는 경우
  - 해당 페이지가 메모리에 올라와 있지 않고 `swap area`에 있는 경우

### 💡 Inverted Page Table

<img width="449" alt="Image" src="https://github.com/user-attachments/assets/e8146b6b-2140-4bf7-a637-257e88eb56c6" />

- 원래 `page table`은 `logical address` ➡️ `physical address`
- 👎🏻 모든 프로세스마다 `page table`이 존재하고
- 👎🏻 모든 프로세스의 모든 `page`에 대해 `page table entry`를 다 구성하다보니 하다보니 메모리 낭비가 너무 심함
- (대응하는 `page`가 메모리에 있든 아니든 간에 `page table`에는 `entry`로 존재)

- 💊 `Inverted Page Table`는 이 문제를 해결하기 위한 대안으로 등장
- `physical address`의 `frame` 하나 당 `page table entity`가 존재(`system-wide`)
- 즉, `logical address`를 보고 `page table`을 만드는 것이 아니라
- `physical address`에 대해 `page table`을 만드는 것

- 각 프로세스마다 `page table`을 두지 않고, 시스템 전체에 `page table`을 하나만 두는 방식(`system-wide`)

- 각 `page table entity`는
- 각각의 물리적 메모리의 `page frame`이 담고 있는 내용 표시
- (`pid`, `process logical address`)
  - 어느 프로세스의: `pid`
  - 어떤 페이지가
  - 어떤 페이지 프레임에 적재되었는지
  - 즉, 그 프로세스 내의 `process logical address page number p`
- 정보를 관리

- 따라서 `Inverted Page Table`은 `physical address`을 보고 `logical address`를 얻어낼 수 있음
- `pid`와 `p`를 통해 프레임 `f`를 찾은 뒤, 거기에 `offset d`를 더하여 물리적 메모리 주소를 알아낸다

- 👎🏻 주소변환을 하기 위해서는 그 주소를 담은 `page`가 `physical memory`에 존재하는지 여부를 판단하기 위해 `page table`을 다 찾아봐야 해서 비효율적

- 👍🏻 시스템에 `page table`하나만 존재하면 된다.
- 하지만 주소변환에는 도움이 안 됨(주소변환 방향은 `la` ➡️ `pa`이니까)

- 👎🏻 주소변환을 하기 위해서는 `페이지 번호` 뿐만 아니라 이 번호가 어떤 프로세스의 번호인지 알려주는 `프로세스 번호 pid`도 같이 가지고 있어야 한다

- 💊 그래서 `Inverted Page Table`은 메모리에 올려두지 않고 parallel search가 가능한 `associative register`사용해 탐색을 빠르게 한다
- 👎🏻 high cost, expensive

### 💡 Shared Pages

<img width="422" alt="Image" src="https://github.com/user-attachments/assets/195c4107-6e14-42e6-a12d-480a3202ea1a" />

- `shared code`: 여러 프로세스에 의해 공통으로 사용될 수 있도록 작성된 코드
- `shared page`: `shared code`를 담고 있는 `page`
- 만약 동일한 프로그램이 프로세스 3개를 만들고 있으면 `code`는 똑같고, `data`는 다르다

- `shared page`는 여러 프로세스에 의해 공유되는 `page`이므로
- `physical memory`에 한 번만 적재
- `shared code`는 똑같은 내용을 여러번 올리지 말고 한번만 올리자

- ❓ `shared code`의 목적?
- 메모리 공간의 효율적인 사용을 위해

- 👎🏻 하지만 `shared page`는 그 페이지를 공유하는 모든 프로세스의 주소 공간에서 동일한 페이지 번호를 가져야 한다.

```
process 1의 ed1은 pagetable에 보니 3번에 있다고 되어 있음
실제로 physical memory 3번을 보면 ed1

process 1, 2, 3은 모두 같은 프로그램이라고 가정하면
ed1은 한번만 physical memory에 올라가면 된다.
```

- ✔️ **Shared code**
- Re-entrant Code(Pure code) 재진입 가능한 코드
- `read-only`만 가능하게 하여 프로세스 간 하나의 `code`만 메모리에 올린다.
- `shared-code`는 모든 프로세스의 `logical address space`에서 동일한 위치에 있어야 함
- `shared page`는 그 페이지를 공유하는 모든 프로세스의 주소 공간에서 동일한 페이지 번호를 가져야 한다.

- Shared code의 조건 2가지

```
1️⃣ 코드는 read-only만 가능하도록 세팅
2️⃣ 동일한 logical address space에 있어야 한다. 즉, `page`번호가 같아야 한다.

```

- 🆚 Inter Process Communication의 shared memory: `IPC`는 프로세스 간 협력이므로 `read-only`외에도 가능

- 🆚 **Private code and data**
- `shared page`와 반대되는 개념으로, 프로세스들이 공유하지 않고 프로세스별로 독자적으로 사용하는 페이지
- 각 프로세스들은 독자적으로 메모리에 올림
- `private data`는 `logical address space`가 달라도 된다.

### 📍 Segmentation

> 하나의 프로세스의 주소 공간을 의미 단위 `세그먼트`로 나누어 물리적 메모리에 올리기

- ✔️ **Segment**
- 주소 공간을 기능 단위 또는 의미 단위로 나눈 것
- 작게는 프로그램을 구성하는 함수 하나하나가 `segment`
- 크게는 프로그램 전체를 하나의 `segment`로 정의 가능
- 일반적으로는`code`, `stack`, `data`를 각각 하나의 `segment`로 정의
- `segment`는 의미를 가질 수 있는 논리적인 단위이기 때문에 크기는 균일하지 않음

```
Segment는 다음과 같은 logical unit이다
main(),
function,
global variables,
stack,
symbol table, arrays
```

- ✔️ **Segmentation**
  > 프로세스를 **의미가 있는 단위**로 잘라서 메모리에 올린다 <br>
  > 예를 들어 `logical memory`의 `code`, `stack`, `data`를 다르게 잘라서 `physical memory`에 올린다 <br>
  > 따라서 `segement`의 크기는 모두 다르다 <br>

<img width="437" alt="Image" src="https://github.com/user-attachments/assets/d8a3ebbb-0dac-47b7-8d41-84de270f3b69" />

- Segmentation에서 `logical address`는 다음의 두 가지로 구성

  - `s`: `segment number` 해당 `logical address`가 프로세스 주소 공간 내에서 몇 번째 세그먼트에 있는가
  - `d`: `offset` 그 세그먼트 시작 시점으로부터 얼마나 떨어져 있는가

- 💡 **Segment table**을 사용해서 주소변환을 한다
- each table entry has

  - `base`: `physical address`에서 `segment`의 시작 위치
  - `limit`: length of the segment
    - `segment`의 크기는 다 다르니까 어디까지인지 알려주는 `limit`이 필요하다

#### ☑️ Segment registers

- ✔️ **Segment table base register(STBR)**
- 현재 CPU에서 실행 중인 프로세스의 `segment table`이 물리적 메모리 어느 위치에 있는지, 그 시작 정보를 담고 있음

- ✔️ **Segment table length register(STLR)**
- 프로그램이 사용하는 `segment`의 수
- 프로세스 주소 공간이 몇 개의 `segment`로 구성되어 있는지 `segment` 개수
- 즉, segment table의 길이
- 이 프로세스가 n개의 `segment`로 구성되었다면, `STLR`은 n
- `segment number s is legal if s < STLR`
- 만약 `segment` 3개로 구성된 `segment table`이 있는데 5번 `segment`를 요청한다? ➡️ 잘못된 접근 ➡️ trap

```
s값을 받아 segment table의 s값에 가서 limit, base를 보고
d라는 base에서 얼마나 떨어진 값에 접근하려고 하는지 알아서
만약 이 값이 limit 보다 작으면 ➡️ 내 주소공간 안의 값 접근 ➡️ 허용⭕️
만약 이 값이 limit을 넘어가면 ➡️ 내 주소공간 밖의 값 접근 ➡️ 잘못된 접근 ➡️ 제한 trap❌
```

#### ❗️ **Segmentation에서 주소변환을 할 때에는 두 가지를 확인한다**

- `logical address`의 `offset`값과 해당 `segment table entry`의 `limit`값

- 1️⃣ 요청된 `segment` 번호가 `STLR`에 저장된 값보다 작은지
  - 해당 `segment table` 길이를 넘어서는 `offset`을 요청하지는 않았는지
- 2️⃣ `logical address`의 `offset`값이 그 `segment`의 길이보다 작은지
  - 이 프로세스가 사용하는 `segment` 개수를 넘어서지는 않는지

<img width="372" alt="Image" src="https://github.com/user-attachments/assets/a16222dd-174a-473a-bece-ac2e16047372" />

```
- segment 0
- base 1400: starts from 1400 on physical memory
- limit 1000: length of this segment is 1000, thus located from 1400 ~ 2400
```

#### ☑️ Protection in segmentation

- `segmentation`기법에서도 `segment table`의 각 엔트리에 `protection bit`, `valid/invalid bit`를 둔다

- 각 세그먼트 별로 protection bit가 있음
- `valid bit` = 0 ➡️ illegal segment
- read/write/exectution `권한 bit`

#### ☑️ Sharing

- `segmentation`기법에서도 공유 `segment`를 지원

- `shared segment`
- `same segment number`
- `shared segment`는 동일한 `logical address`를 가져야 한다.

- 👍🏻 _의미 단위로 해야 하는 일_(`Protection`, `Sharing`)측면에서 `segment`으로 한번에 관리 가능
  - 예를 들어 `code segment`는 코드 관련이니까 주의 필요, 따라서 `Protection`을 `read-only`로 주기, `share`는 가능하게 하기 설정 가능
    - 🆚 `page`는 동일 크기로 나누다보니까 한 개의 `page`에 `code` 부분과 `data`부분이 나뉘어 있으면, `Protection`, `Sharing`은 누구에 맞춰 설정할 것인가? 하는 문제 발생
- 👍🏻 `segment`는 의미 단위이기 때문에 `sharing`, `protection`에 있어 `paging`보다 효과적

<img width="352" alt="Image" src="https://github.com/user-attachments/assets/70d93111-4f1d-47da-b3ef-4918654f3454" />

- `editor`을 `Sharing`으로 설정하고 공유하는 모습
- 여러 프로세스가 공유하기 때문에 모든 프로세스의 주소 공간에서 동일한 `logical address`에 위치해야 한다

#### ☑️ Allocation

- 👎🏻 `segment`는 크기가 다르니 어느 가용 공간에 할당하는지 경정해야 하는 문제 발생
  - `segment`는 크기가 다르니 어디에다가 조각을 넣을 것인가? 결정해야 함
  - `first fit`, `best fit`
- 👎🏻 `segment`는 크기가 동일하지 않다보니 `external fragmentation` 생김

- 🆚 Paging
- `page`가 동일한 크기로 나뉘어져 있음
- `segment`는 크기가 동일하지 않음, 따라서 `segment` 길이를 알려주는 `limit` 필요

- `paging`에서는 `page` 크기가 모두 같으니 어디에 놓을지 allocation 문제가 발생하지 않음
- `segment`는 크기가 동일하지 않다보니 `external fragmentation` 발생

- `page`는 동일 크기로 나누다보니까 `Protection`, `Sharing`설정 문제 발생
- `segment`는 의미 단위로 나뉘니까 각 `segment`에 따라 `Protection`, `Sharing`을 결정하기가 수월

- `page`에서는 각 프로세스마다 `page`가 거의 백만개씩 존재하고, 그래서 주소 공간을 위한 `page table`이 엄청 크고 낭비가 심했음, 이를 보완하기 위해 `다단계 page`등 방법 등장
- 👍🏻 `segment`는 아무리 나눠봤자 `code`, `stack`, `data` 등 `entry`개수가 몇 개 안 됨, 따라서 `segment table`이 비교적 작음
- 현실적인 구현은 `segment`이 수월하나, `segment` 간의 크기 차이 문제도 있고 등등해서
- 실제로는 `page`가 더 많이 쓰인다

### 📍 Paged Segmentation

> semgmentation을 기본으로 하되, 이를 다시 동일 크기 페이지로 나누어 메모리에 올리기

<img width="384" alt="Image" src="https://github.com/user-attachments/assets/94980ac7-007b-4c8e-a530-0504d5a8004b" />

- 프로그램을 의미 단위인 `segment`로 나눈다
- 단, 하나의 `segment`가 반드시 동일한 크기의 `page`의 집합으로 구성되어야 한다
- `segment`가 각각 `physical memory`에 올라가는 것이 아니고 ❌
- `segment`가 여러 `page`로 구성이 되어 `page`가 `physical memory`에 올라간다. ⭕️
- 따라서 `segment`마다 `page table`이 있다

- 즉, `Paged Segmentation`기법에서는 하나의 `segment` 크기를 `page`크기의 배수가 되도록 한다
- `segment`의 크기가 `page`의 배수로 구성
- 따라서 `physical memory`는 동일한 크기의 `page`로 잘려서 구현

- 대신에 의미가 필요한 것들은 `segment table`에서 관리

- 👍🏻 `segment` 단위로 프로세스 간 `Protection`, `Sharing`설정 수월
- 👍🏻 Allocation, `external fragmentation` 문제 발생하지 않음

- `Paged Segmentation`기법에서는 주소 변환을 위해 `외부ㅢ 세그먼트 테이블`과 `내부의 페이지 테이블` 이렇게 두 단계를 둔다
- <`세그먼트 번호 s`, `오프셋 d`>으로 구성된 `logical address`를 물리적 주소로 변환하는 과정

```
1. 먼저 STBR로 메모리에 적재되어있는 Segment Table을 찾는다.
2. 논리적주소의 세그먼트 번호 s를 Segment Table의 인덱스로 사용하여 해당 엔트리를 찾는다. 엔트리에는 해당 세그먼트의 길이와, 세그먼트를 구성하는 Page들의 Page Table의 시작 주소가 들어있다. 만약 세그먼트 길이보다 오프셋 값 d가 크다면 trap에 걸린다.
3. 논리적 주소 d로부터 페이지 번호 p와 페이지 오프셋 d’를 얻어낸다. 페이지 번호를 페이지 테이블의 인덱스로 사용하여 페이지 프레임 번호 f를 얻어낸다.
4. 페이지 프레임 번호 f와 페이지 오프셋 d’를 더해서 물리적 주소를 얻어낸다.
```

- 🆚 `pure segment`과의 차이점
- `segment table entry`가 `segment`의 `base address`를 가지고 있는 것이 아니라
- `segment`를 구성하는 `page table`의 `base address`를 가지고 있음

- ❗️ `segment`가 `page` 몇 개로 구성되는지 길이를 확인하고,
- 그 길이를 넘어서는 요청이 있으면 trap
