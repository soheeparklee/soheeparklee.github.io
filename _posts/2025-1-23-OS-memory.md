---
title: KOCW_Memory Management
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ Memory

- memory는 주소를 통해서 접근한다.

#### ☑️ 주소의 종류

- ✔️ **Physical address**
- 메모리에 실제로 올라가는 주소

- ✔️ **Logical address(virtual memory)**
- 프로그램이 실행되었을 때 프로그램이 _독자적으로_ 가지는 `가상 메모리`
- 프로그램마다 가상 메모리를 가진다.
- 각 프로세스마다 0번지부터 시작
- `CPU`가 보는 주소는 `Logical address`

```
프로그램 A가 디스크에 저장되어 있음
프로그램 A 실행 ➡️ 프로세스 A
프로세스 A의 가상 메모리 주소 공간 가지게 됨
가상 메모리 주소 ➡️ 주소 변환 ➡️ 물리적 주소
물리적 주소가 메모리 위에 올라간다
```

## ✅ 주소 바인딩

> `logical address`를 `physical address`로 `mapping`해 주는 것

- 💡 주소 변환은 `하드웨어`가 담당한다.
  <br>

- 프로그래머가 바라보는 소스코드 메모리 주소: `symbolic address`
- 프로그램마다 독자적으로 가지는 메모리 공간: `logical address`
- 프로그램이 메모리에 올라가 실행되면: `physical address`
- ➡️ 가상 주소와 물리적 주소 간 주소 변환이 필요하다.

#### ☑️ 어떤 시점에 주소 바인딩을 할 것인가?

> logical address`가 `physical address`로 바뀌는 **시점**에 따라 3가지로 구분

<img width="492" alt="Image" src="https://github.com/user-attachments/assets/af7d8d2d-bc61-4bf3-b3ab-10f8da0e802b" />

- ✔️ **Compile Time Binding**
- `physical address`가 `compile`시 알려짐
- 시작 위치 변경시 재컴파일
- 컴파일러는 절대 코드 `absolute code`생성
- `physical address`가 0번지부터 올라감(원래 OS가 0부터 올라가야 함)
- 👎🏻 비효율적
- 👎🏻 컴퓨터에서 단 한 개의 프로그램만 실행된다면 의미가 있으나, 현대 컴퓨터에서는 잘 사용❌
  <br>

- ✔️ **Load Time Binding**
- 프로그램이 실행되는 시작되는 시점에 `physical address`부여
- 프로그램 시작과 메모리 부여, 이후 바뀌지 않음
- `Loader`의 책임 하에 `physical address`부여
- 컴파일러가 재배치가능코드`relocatable code` 생성한 경우 가능
  <br>

- ✔️ **Execution time binding(=Run time binding)**
- 프로그램이 실행되는 도중에도 `physical address`이 바뀔 수 있음
- 수행이 시작된 이후에도 프로세스의 메모리 상 위치를 옮길 수 있음
- CPU가 주소를 참조할 때마다(메모리에 접근할 때마다) `binding`을 점검한다. (`address mapping table`)
- 메모리 위치가 실시간으로 바뀔 수 있으니까
- _하드웨어적인 지원이 필요하다_(예시: `base and limit registers`, `MMU`)
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
> 주소변환을 하는 하드웨어 <br>

- `logical address`를 `physical address`로 매핑해주는 `hardware device`

- ✔️ **MMU scheme**
- 사용자 프로세스가 CPU에서 수행되며 생성해내는 모든 주소값에 대해 `base register(relocation register)`의 값을 더한다.

- ✔️ **user program**
- `logical address`만을 다룬다.
- 실제 `physical address`를 볼 수 없으며 알 필요도 없다

#### ☑️ Dynamic Relocation

- 프로그램이 실행되면 통째로 메모리에 올라간다고 가정

<img width="480" alt="Image" src="https://github.com/user-attachments/assets/a967632e-597d-4ae5-9702-ee02ed8845f0" />

- CPU가 `logical address` 346번을 요청
- `process P1`을 `physical address`에서 찾아보니 14000에서 시작, 17000까지임
- `virtual memory`에 보니 346번은 `0+346`번 자리에 있음
- `register`: `relocation register`, `limit register`
- `relocation register`: 이 프로그램의 물리적 메모리 시작 위치, `14000`
- `limit register`: 논리적 주소의 범위(이 프로그램의 크기 3000)
- 따라서 `physical address`는 `14000+346 = 14346`
  <br>

- ❓ `limit register`는 왜 필요할까? 왜 굳이 프로그램의 크기를 알고 있어야 할까?
- 만약 이 프로그램이 악의적인 프로그램이라서 잘못된 요청을 할 수 있음
- 😠 자신의 주소 공간이 아닌 다른 프로그램의 주소공간을 요청할 수 있음!
- 예를 들어 위 예시에서, `logical address` 5000번을 요청 ➡️ 자신의 주소 범위 3000보다 큼
- 그러한 요청을 차단하기 위해서 프로그램의 크기를 알고 있어야 한다.
  <br>

<img width="484" alt="Image" src="https://github.com/user-attachments/assets/b901362a-225b-44ae-ba83-9c3d072c3e37" />

- CPU가 `logical address`를 요청
- `MMU`는 `limit register`를 사용해 요청이 내 주소공간 내에 있는지를 확인
- 만족한다면 `relocation register ➕ logical address` 🟰 `physical address`
- 만족하지 않는다면 trap ➡️ CPU가 운영체제에게 넘어간다.

- ✔️ **Relocation register(base register)**
- ✔️ **Limit register**

## 📌 Dynamic Loading

- 프로세스 전체를 메모리에 한번에 다 올리는 것이 아니라❌
- 해당 루틴이 불려질 때 **그때그때** 메모리에 `load`
- 프로그램 중 **현재 실행되는 부분만** 메모리에 `load`
  <br>

- ❓ **Dynamic Loading은 누가 해주는 걸까?**
- 운영체제
- 원래는 운영체제의 특별한 지원 없이도 가능했음

<br>

- 👍🏻 `memory utilization`향상
- 👍🏻 가끔씩 사용되는 많은 양의 코드인 경우 유용(매번 사용되지 않는 코드: 오류 처리 루틴)
- 👍🏻 운영체제의 특별한 지원 없이 프로그램 자체에서 구현 가능(OS는 라이브러리 통해 지원 가능)
- 💡 `load`: 메모리에 프로그램을 적재하는 것

## 📌 Overlays

- 메모리에 프로세스 부분 중 **실제 필요한 정보만을** 올림
- 👍🏻 프로세스의 크기가 메모리보다 클 때 유용하다
- 운영체제 지원 없이 사용자에 의해 구현
- 예전에는 메모리 공간이 매우 작았음!
- 그래서 작은 공간의 메모리를 사용하던 *초창기 시스템*에서 수작업으로 프로그래머가 구현하곤 했음
- 👎🏻 manual overlay
- 👎🏻 프로그래밍 매우 복잡

- 🆚 Dynamic Loading과 비슷하나, Overlays는 프로그래머가 수작업으로 구현

## 📌 Swapping

#### ☑️ Swapping

- 프로세스를 일시적으로 메모리에서 `backing store`로 쫒아내는 것
- 프로세스를 **통째로** 쫒아낸다.
- (🆚 현대 운영체제에서는 일부만 메모리에 올리고 일부만 쫒아냄, swapping 원조랑은 다름)

#### ☑️ Backing store(swap area)

- 디스크로 쫒아낸다
- 많은 사용자의 프로세스 이미지를 담을 만큼 충분히 빠르고 큰 저장 공간

#### ☑️ Swap in/Swap out

- 일반적으로 `중기 스케쥴러`(`swapper`)에 의해 `Swap out`할 프로세스 선정
- 프로세스가 `Swap out`되면 `suspended`상태가 된다.
  <br>

- CPU에서 우선순위가 낮은 프로세스를 `Swap out`
- **Priority based CPU scheduling algorithm**
  - priority가 낮은 프로세스 `Swap out`
  - priority가 높은 프로세스는 메모리에 올려 놓음

<br>

- `compile time` 또는 `load time binding`에서는 *원래 메모리 위치*로 `swap in`해야 함(메모리 주소가 바뀌면 안 되니까!)
- `execution time binding(run-time binding)`에서는 추후 _빈 메모리 영역 아무 곳에나_ 올릴 수 있음
- 따라서 `Swap out`은 `execution time binding(run-time binding)` 일 때 제일 효율적

- `swap time`은 대부분 `transfer time`(`swap`되는 양에 비례하는 시간)

## 📌 Dynamic Linking

> linking을 실행 시간(execution time)까지 미루는 기법

#### ☑️ **linking**:

- 프로그램은 `compile`, `linking`을 통해 실행 파일이 만들어진다.
- `linking`: 라이브러리와 내가 만든 코드를 연결하는 과정
  <br>

#### ☑️ **Static Linking**

- **static library**
- 라이브러리가 프로그램의 실행 파일 코드에 **포함됨**
- 실행 파일의 크기가 커짐!
- 👎🏻 동일한 라이브러리를 각각의 프로세스가 메모리에 올림
- 메모리 낭비
  <br>

#### ☑️ **Dynamic Linking**

- **shared libary**
- 라이브러리가 프로그램의 실행 파일 코드에 _포함되지 않고_ 있다가
- 라이브러리가 **실행시** `link`됨
- 실행하다가 라이브러리를 찾아야 함 ➡️ `stub` 필요
- 라이브러리 호출 부분에 라이브러리 루틴의 위치를 찾기 위한 `stub`이라는 작은 코드를 둔다.
- 라이브러리가 이미 메모리에 있으면 ➡️ 그 위치로 가고
- 없으면 ➡️ 디스크에서 읽어옴
- 운영체제의 도움 필요
- 👍🏻 동일 라이브러리는 프로세스가 공유

## ✅ Allocation of Physical Memory

> 물리적 메모리에 주소가 어떻게 할당되는가?

- 메모리는 일반적으로 두 영역으로 나뉘어 사용
  - **OS상주 영역**: `interrupt vector`와 함께 낮은 주소 영역 사용
  - **사용자 프로세스 영역**: 높은 주소 영역 사용

<img width="81" alt="Image" src="https://github.com/user-attachments/assets/ff1ff427-469f-4954-beac-e6fd82293681" />

#### ☑️ 사용자 프로세스 영역 할당 방법

- ✔️ **Contiguous allocation**
- 각각의 프로세스가 메모리의 _연속적인_ 공간에 적재되도록 하는 것
- 프로그램이 쪼개지지 않고, 통째로 올라감
- 👍🏻 프로그램 주소변환이 비교적 간단(`relocation register`, `limit register`)
- Fixed-partition allocation
- Variable partition allocation
- 👎🏻 메모리를 할당하다가 `hole`들이 너무 작게 쪼개지면 아무런 프로세스를 올리지 못하는 문제 발생 가능

- ✔️ **Noncontiguous allocation**
- 하나의 프로세스가 메모리의 여러 영역에 _분산되어_ 올라갈 수 있음
- Paging
- Segmentation
- Paged Segmentation

- ✔️ **Internal fragmentation**
- 사용자 프로그램이 분할 `partition`보다 _작아서_
- `partition`이 내부에서 쪼개짐
- 내부조각

- ✔️ **External fragmentation**
- 사용자 프로그램이 분할 `partition`보다 _커서_
- 해당 `partition`에 들어가지 못하고, 다음 `partition`에 들어감
- 그러면 에매한 크기의 `partition`은 낭비
- 외부조각

## ✅ Contiguous allocation

### 📍 Fixed-partition allocation

> 물리적 메모리를 몇 개의 영구적 분할 `partition`으로 **미리** 나눔

<img width="225" alt="Image" src="https://github.com/user-attachments/assets/9f41e313-1125-447d-aab6-b48e12d238f5" />

- 분할의 크기가 `1. 모두 동일한 방식`과 `2. 서로 다른 방식`이 존재
- 각각의 분할 당 하나의 프로그램 적재
- 👎🏻 융통성이 없다.
- 동시에 메모리에 `load`되는 프로그램 수가 고정됨
- 최대 수행 가능 프로그램 크기 제한
- 👎🏻 Internal fragmentation 발생
- 👎🏻 External fragmentation도 발생

```
프로그램A는 분할1에 잘 들어감
프로그램B는 분할2보다는 크고 분할3보다는 작다
그래서 분할3에 들어감
- 분할2: External fragmentation
- 분할3: Internal fragmentation
```

### 📍 Variable partition allocation

<img width="240" alt="Image" src="https://github.com/user-attachments/assets/3bd65d27-4a09-4840-be47-96b39a53ec91" />

- `partition`을 미리 나눠놓지 말고,
- 프로그램의 크기를 고려해서 할당
- 분할의 크기, 개수가 동적으로 변한다
- 기술적 관리 기법 필요
- 👎🏻 External fragmentation 발생

```
프로그램B가 끝나고 메모리가 비게 되었음
그러나 프로그램D는 그 메모리 분할에 들어가기에는 큼
현재 연속할당이므로, 프로그램은 쪼개져서 들어갈 수 없음
프로그램D는 더 큰 메모리 분할을 할당받고,
프로그램B 메모리 공간은 External fragmentation
```

### 📍 Hole

> 가용 메모리 공간

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
- 👍🏻 비교적 맞춤형 사이즈의 `hole`을 할당해줄 수 있음
- 👎🏻 `hole`들의 리스크가 크기순으로 정렬되지 않은 경우 모든 `hole` 리스트를 돌면서 탐색해야 함
- 👎🏻 많은 수의 아주 작은 `hole` 생성

- ✔️ **Worst Fit**
- 가장 큰 `hole` 할당
- 👎🏻 마찬가지로 모든 `hole` 리스트를 탐색해야 함
- 상대적으로 아주 큰 `hole`들 생성
- 👎🏻 나중에 진짜 큰 프로세스 오면 할당해 줄 공간이 없음

- 💡 `First Fit`과 `Best Fit`이 `Worst Fit`보다 속도과 공간 이용률 측면에서 효과적인 것으로 판면

### 📍 Compaction

- External fragmentation 문제를 해결하는 방법
- 사용중인 메모리 영역을 한 군데로 몰고,
- `hole`들을 다른 한 곳으로 몰아 아주 큰 `block`을 만든다.

- 👎🏻 아주 비용이 많이 든다
  - 거의 모든 프로그램의 메모리 공간을 바꾸니까
- 👎🏻 최소한의 메모리 이동으로 `compaction`하는 방법은 아주 복잡한 문제

- `compaction`을 하기 위해서는 `execution time binding(run-time binding)`일 때만 가능

## ✅ Noncontiguous allocation

## ✅

## ✅

## ✅

## ✅

#### ☑️

- ✔️
- ✔️
- ✔️
- ❓
