---
title: KOCW_Memory Management
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ Memory

- memory management는 `하드웨어`가 담당한다.
- memory는 주소를 통해서 접근한다.

- 서로다른 `n`군데를 구분하기 위해서는 `n = 2의 m제곱`했을 때 `m bit`
- `N bit`로 구분 가능한 서로 다른 위치는? `2의 N제곱`개

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
- 운영체제는 주소 바인딩과 무관하다
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
- 프로그램이 *실행되는 시작*되는 시점에 `physical address`부여
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

## 📌 Dynamic Relocation

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
- 현대 메모리에서는 자주 쓰이지 않는 방법

- ✔️ **Noncontiguous allocation**
- 하나의 프로세스가 메모리의 여러 영역에 _분산되어_ 올라갈 수 있음
- 👎🏻 프로세스가 쪼개져서 메모리에 올라가다보니 프로그램 주소변환을 하기가 어려움
- Paging
- Segmentation
- Paged Segmentation

- ✔️ **Internal fragmentation**
- 사용자 프로그램이 분할 `partition`보다 _작아서_
- `partition`이 내부에서 쪼개짐
- 내부조각

<img width="231" alt="Image" src="https://github.com/user-attachments/assets/4ace85f4-8df9-477f-a1a3-ead120d99a1b" />

- ✔️ **External fragmentation**
- 사용자 프로그램이 분할 `partition 1`보다 _커서_
- 해당 `partition 1`에 들어가지 못하고, 다음 `partition 2`에 들어감
- 그러면 에매한 크기의 `partition 1`은 낭비
- 외부조각

<img width="235" alt="Image" src="https://github.com/user-attachments/assets/9500b561-bb93-4533-b51d-7fa93e6c5cf9" />

## ✅ Contiguous allocation

> 프로그램이 **통쨰로** 메모리에 올라감

- ❓ **Contiguous allocation 에서는 프로세스 주소 변환을 어떻게 하나요?**
- 두 개의 register `relocation register`, `limit register` 사용

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

### 💡 Hole

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

### 💡 Compaction

- External fragmentation 문제를 해결하는 방법
- 사용중인 메모리 영역을 한 군데로 몰고,
- `hole`들을 다른 한 곳으로 몰아 아주 큰 `block`을 만든다.

- 👎🏻 아주 비용이 많이 든다
  - 거의 모든 프로그램의 메모리 공간을 바꾸니까
- 👎🏻 최소한의 메모리 이동으로 `compaction`하는 방법은 아주 복잡한 문제

- `compaction`을 하기 위해서는 `execution time binding(run-time binding)`일 때만 가능

## ✅ Noncontiguous allocation

> 프로세스가 여러개로 **쪼개져서** 메모리에 올라가는 방식

### 📍 Paging

- 프로세스의 `virtual memory`를 **동일한 사이즈**의 `page`로 나눔(일반적으로 `4B`)
- `virtual memory`의 내용이 `page`단위로 `Noncontiguous`하게 저장됨
- 일부는 `backing storage(swap)`에, 일부는 `physical memory`에 저장
  <br>

<img width="380" alt="Image" src="https://github.com/user-attachments/assets/0091c36e-ee58-4588-88d3-32fda4f0bb13" />

- `physical memory`도 `page`하나가 들어갈 수 있도록 **동일한** 크기의 `frame`으로 나눔
- `logical memory`를 동일 크기의 `page`로 나눔(`frame`과 같은 크기)
- 모든 가용 `frame`들을 관리
- 💡 **`page table`**을 이용하여 `logical memory adress`를 `physical memory adress`로 변환
- 👎🏻 Internal fragmentation 발생 가능(메모리를 같은 크기의 `frame`로 쪼개다보면 남는 공간 생길 수도 있으므로)
- 👍🏻 External fragmentation 발생 안 함(프로세스가 `frame`보다 크면 쪼개서 들어가면 되니까)
  <br>

- ❓ **Paging에서는 프로세스 주소 변환을 어떻게 하나요?**
- `page table`을 이용
- `몇 번 페이지 번호 page` + `페이지 내에서 어디에 위치 frame(변하지 않음)`

### 💡 Page Table

- `page table entry`가 백만개가 넘는 상황이기 때문에, `Contiguous allocation`처럼 `register` 2개에 주소를 집어넣을 수가 없음!
- 따라서 `page table`자체를 만들고 **메모리에** 올린다.
- `page table`은 `main memory`에 상주

- 💡 프로세스마다 `page table`가 있다
- 그래서 `context switching`이 발생하면 `page table`에 따른 `TLB`가 지워지고 새로 만들어저야 하니 `overhead`가 꽤 크다

  <br>

### 💡 Address Translation Architecture

<img width="358" alt="Image" src="https://github.com/user-attachments/assets/a9175922-072f-4867-878e-130085803884" />

- 주소의 두 부분
- 페이지 번호 : `p`, `4kb`
- 페이지 내에서 어디에 위치하는지 나타내는 `offset`: `d`
- 예를 들어 `page 2번` + `page 2번 내의 위치`
- `d`의 값은 변하지 않는다
- 보통 `logical address`는 `32bit`이다
- 👍🏻 `p`, `d`의 값만 알면 바로 주소 구할 수 있음
  <br>

- `logical address` 주소가 `32bit`인 환경에서
- `프로그램 메모리 공간 VM`이 최대 가질 수 있는 크기는 `2의 32제곱`, 즉 `4GB`
- `page`하나는 `4kb`
- 따라서 하나의 `VM`안에는 주소공간이 `1메가, 100만`개 있을 수 있다
- 😱 페이지의 개수가 프로세스마다 `100만`개가 있는 상황
- 😱 따라서 `page table`에는 `1메가`개수 만큼의 `page table entry`가 필요
- 💊 그래서 `page table`이 `main memory`하는 것이다

- `Page-table base register(PTBR)`가 `page table`(`p`)**시작 위치**를 가리킴
- `Page-table length register(PTLR)`가 **테이블 크기**(`d`)를 보관
- `Page-table base register(PTBR)` + `Page-table length register(PTLR)`
  <br>

- 따라서 모든 메모리 접근 연산에는 **2번**의 `memory access`필요

  - 1번: `page table` 접근 1번: 주소 변환을 위해 메모리의 `page table` 접근
  - 2번: `data/instruction` 접근 1번: 실제 데이터 접근 위해 메모리 접근
  - 👎🏻 메모리를 2번 접근해야 하니 속도 저하
  - 💊 `TLB`
    <br>

### 💡 TLB

> Translation Lookaside Buffer

- 💊 주소변환을 전담하는 `cache memory`를 둔다.
- 💊 **가상 메모리 주소를 물리적 주소로 바꾸는 속도 향상을 위해** `cache memory` 즉 `TLB`를 둔다
- `TLB` 탐색 속도 향상을 위해 `associative register` 혹은 `translation look-aside buffer(TLB)`라 불리는 고속의 `lookup hardware cache` 사용
- `TLB`는 **주소 변환을 빠르게 하기 위한** `cache memory`

- `p`번째 페이지에 대한 주소변환 `f`가 _쌍으로_ 저장되어 있다.

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

- 👎🏻 하지만 `TLB`는 `cache memory`이기 때문에 모든 주소를 다 담고 있지는 않음 ❌
- `cache memory` 공간이 한정되어있기 때문에, 일부만 알고 있음
- 👎🏻 그래서 페이지 번호 `p`가 있는지 없는지 `TLB`를 모두 탐색해야 한다
- 💊 그래서 모든 `p`를 `parallel하게, 병렬적으로` 찾는다
- 💊 이 역할을 하는 하드웨어를 `associative register`이라고 한다.

- 👎🏻 그리고 테이블과 달리 `index`가 따로 없기 때문에
- 이 주소변환이 어떤 `page`에 있는지 알려주는 `frame number`이 필요하다.
- 따라서 `page number`, `frame number`을 _쌍으로_ 가지고 있어야 한다.

- 👎🏻 `page table`는 프로세스마다 존재하기 때문에
- `context switching`으로 CPU에서 실행되는 프로세스가 바뀌면 `TLB`도 바뀌어야 한다.
- 기존 `cache memory`인 `TLB`를 지우고, 새로 만드는 과정에서 `overhead`발생

- ❓ **`context switching`의 `overhead` 중 메모리와 관련된 대표적인 것으로는 무엇이 있나요?**
- `TLB`를 지우고, 새로 만드는 과정에서 `overhead`가 크게 발생한다

#### `page table` 🆚 TLB

- `page table`: 테이블이기 때문에 `index`가 있어 `p`를 찾을 때 딱 그 부분을 찾을 수 있음
- TLB: `p`가 있는지 없는지 `TLB`를 전부다 탐색해야 한다

- `page table`: 모든 주소를 다 담고 있음
- TLB: `cache memory`이기 때문에 모든 주소를 다 담고 있지는 않음

- `page table`: `p`번째 인덱스에 가면 `f`를 알 수 있음
- TLB: `page number`, `frame number`을 _쌍으로_ 가지고 있어야 한다.

### 💡 Associative register

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
- `32bit address`사용 시: `2의 32제곱(4G)`의 주소 공간을 가진다

  - `page size`가 `4K`일 시 `1M`개의 `page table entry`필요
  - 각 `page table entry`가 `4B`일 시 프로세스 당 `4M`의 `page table`필요
  - 👎🏻 그러나 대부분의 프로그램은 `4G`의 주소 공간 중 지극히 일부만 사용하므로 `page table` 공간이 낭비됨

<br>

- **그래서 `Paging`은**
- 👍🏻 프로그램을 동일한 사이즈의 `page`로 잘라 메모리에 Noncontiguous하게 올리고
- 👍🏻 사용하는 메모리만 올린다는 장점이 있으나
- 👎🏻 `page` 개수가 프로세스마다 백만개가 넘는다
- 👎🏻 `page table`에 `4b`짜리가 백만개가 넘음
- 게다가 `page table`은 프로세스마다 각각 존재함
- 엄청난 양의 메모리가 주소변환을 위해 쓰이고
- 👎🏻 심지어 다 쓰이지도 않기 때문에 낭비 심함

<br>

<img width="323" alt="Image" src="https://github.com/user-attachments/assets/e105ea66-55a9-4601-9cc9-930215743eaf" />

- 💊 **2단계 페이지 테이블**
- 💊 `page table`자체를 `page`로 구성
- `page table` 하나를 더 뒤서 `page table`을 계층적으로 구성(`서울시-양천구-목동` 처럼)
- 사용되지 않는 주소 공간에 대한 `outer page table`의 엔트리 값은 `NULL`로 설정

- 안쪽 `page table` 하나가 `4kb`
- 이 안에 `entry`는 `4B`, 따라서 한 개의 `page table`안에 `entry`는 `1K`개

- 👎🏻 주소변환을 위해 메모리를 3번 접근해야 함
- (주소변환 위해 2개의 테이블 접근 ➕ 실제 데이터 접근 위해 메모리 접근)
- 👎🏻 시간상으로 손해
- 👍🏻 하지만 **공간상으로는 메모리 낭비를 줄일 수 있다**.

### 💡 Address Translation Scheme in Two-Level Page Table

> 2단계 페이지 테이블에서의 주소 변환 과정

<img width="393" alt="Image" src="https://github.com/user-attachments/assets/67b6028b-ae2e-4772-9745-dfdc8a05d761" />

- `logical address`: `32bit` 3부분으로 나누어진다.
  - `p1`: outer page table `10bit`
  - `p2`: page of table table `10bit`
  - `d`: page offset, 페이지 안에서 얼마나 떨어져 있는가 `12bit`

<img width="481" alt="Image" src="https://github.com/user-attachments/assets/0bdc0a6b-4a9a-4985-86a2-4b46c532c7b3" />

- 만약 `p1`이 `NULL`이다 ➡️ 저장된 내용 없음
- `p1`가 `NULL`이 아니다 ➡️ `두번째 테이블`의 시작 위치를 가지고 있다.
- `p2`: `두번째 테이블`에서 얼마나 떨어졌는지(`frame`위치)
- `d`: 물리적 주소로 변환한 결과

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
- `page`에 대한 접근 권한(read/write/read-only) 보호
- 각 `page`가 자신의 `page table`에 대해 어떤 권한을 가지는지 권한 제한

- ✔️ **valud-invalid bit**
- `valid`는 해당 주소의 `frame`에 그 프로세스를 구성하는 유효한 내용이 있음을 의미(잡근 허용)
- `invalid`는 해당 주소의 `frame`에 유효한 내용이 없음을 의미
  - 프로그램이 그 주소 부분을 사용하지 않는 경우
  - 해당 페이지가 메모리에 올라와 있지 않고 `swap area`에 있는 경우

### 💡 Inverted Page Table

<img width="449" alt="Image" src="https://github.com/user-attachments/assets/e8146b6b-2140-4bf7-a637-257e88eb56c6" />

- 원래 `page table`은 `logical address` ➡️ `physical address`
- 👎🏻 하지만 프로세스마다 `logical address`에 대응하는 모든 `page`에 대해 `page table entry`가 존재
- 모든 프로세스마다 `page table`이 존재하다보니 메모리 낭비가 너무 심함
- 또 대응하는 `page`가 메모리에 있든 아니든 간에 `page table`에는 `entry`로 존재

- 💊 `Inverted Page Table`는 `physical address`의 `frame` 하나 당 `page table entity`가 존재(`system-wide`)
- 각 `page table entity`는 각각의 물리적 메모리의 `page frame`이 담고 있는 내용 표시
- (`pid`, `process logical address`)
- 따라서 `Inverted Page Table`은 `physical address`을 보고 `logical address`를 얻어낼 수 있음

- 👍🏻 시스템에 `page table`하나만 존재하면 된다.
- 하지만 주소변환에는 도움이 안 됨(주소변환 방향은 `la` ➡️ `pa`이니까)
- 👎🏻 주소변환을 하기 위해서는 `page table`을 다 찾아봐야 해서 비효율적
- 👎🏻 주소변환을 하기 위해서는 `페이지 번호` 뿐만 아니라 이 번호가 어떤 프로세스의 번호인지 알려주는 `프로세스 번호 pid`도 같이 가지고 있어야 한다

- 💊 parallel search가 가능한 `associative register`사용
- 👎🏻 high cost, expensive

### 💡 Shared Pages

<img width="422" alt="Image" src="https://github.com/user-attachments/assets/195c4107-6e14-42e6-a12d-480a3202ea1a" />

- 만약 동일한 프로그램이 프로세스 3개를 만들고 있으면 `code`는 똑같고, `data`는 다르다
- 따라서 `shared code`는 똑같은 내용을 여러번 올리지 말고 한번만 올리자

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
- Shared code의 조건

  - 1. 코드는 `read-only`만 가능하도록 세팅
  - 2. 동일한 `logical address space`에 있어야 한다. 즉, `page`번호가 같아야 한다.

- 🆚 Inter Process Communication의 shared memory: `IPC`는 프로세스 간 협력이므로 `read-only`외에도 가능

- ✔️ **Private code and data**
- 각 프로세스들은 독자적으로 메모리에 올림
- `private data`는 `logical address space`가 달라도 된다.

### 📍 Segmentation

- ✔️ **Segment**
- 의미 단위
- 작게는 프로그램을 구성하는 함수 하나하나가 `segment`
- 크게는 프로그램 전테를 하나의 `segment`로 정의 가능
- 일반적으로는`code`, `stack`, `data`를 각각 하나의 `segment`로 정의

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

- `logical address`는 다음의 두 가지로 구성

  - `s`: `segment number` 물리적 메모리 어디에 있는가
  - `d`: `offset` 세그먼트 시작 시점으로부터 얼마나 떨어져 있는가

- 💡 **Segment table**을 사용해서 주소변환을 한다
- each table entry has

  - `base`: starting physical address of the segment
  - `limit`: length of the segment
  - `segment` 크기가 다 다르니까 어디까지인지 알려주는 `limit`이 필요하다

- ✔️ **Segment table base register(STBR)**
- 물리적 메모리에서의 segment table의 시작 위치

- ✔️ **Segment table length register(STLR)**
- 프로그램이 사용하는 segment의 수
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

- ❗️ 따라서 Segmentation에서 주소변환을 할 때에는 요청이 다음과 같으면 제한

  - 해당 `segment table` 길이를 넘어서는 `offset`을 요청하지는 않았는지
  - 이 프로세스가 사용하는 `segment` 개수를 넘어서지는 않는지

<img width="372" alt="Image" src="https://github.com/user-attachments/assets/a16222dd-174a-473a-bece-ac2e16047372" />

```
- segment 0
- base 1400: starts from 1400 on physical memory
- limit 1000: length of this segment is 1000, thus located from 1400 ~ 2400
```

- ✔️ **Protection**
- 각 세그먼트 별로 protection bit가 있음
- each entry:

  - valid bit = 0 ➡️ illegal segment
  - read/write/exectution 권한 bit

- ✔️ **Sharing**
- `shared segment`
- `same segment number`
- _의미 단위로 해야 하는 일_(`Protection`, `Sharing`)은 `segment`으로 한번에 관리 가능
- 예를 들어 `code segment`는 코드 관련이니까 주의 필요, 따라서 `Protection`을 `read-only`로 주기, `share`는 가능하게 하기 설정 가능
- 🆚 `page`는 동일 크기로 나누다보니까 한 개의 `page`에 `code` 부분과 `data`부분이 나뉘어 있으면, `Protection`, `Sharing`은 누구에 맞춰 설정할 것인가? 하는 문제 발생
- 👍🏻 `segment`는 의미 단위이기 때문에 `sharing`, `protection`에 있어 `paging`보다 효과적

<img width="352" alt="Image" src="https://github.com/user-attachments/assets/70d93111-4f1d-47da-b3ef-4918654f3454" />

- `editor`을 `Sharing`으로 설정하고 공유하는 모습
- `logical address`는 똑같다

- ✔️ **Allocation**
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

<img width="384" alt="Image" src="https://github.com/user-attachments/assets/94980ac7-007b-4c8e-a530-0504d5a8004b" />

- 기본적으로 `segment`를 쓰는데,
- `segment`가 각각 `physical memory`에 올라가는 것이 아니고
- `segment`가 여러 `page`로 구성이 되어 `page`가 `physical memory`에 올라간다.
- 따라서 `segment`마다 `page table`이 있다
- `segment`의 크기가 `page`의 배수로 구성
- 따라서 `physical memory`는 동일한 크기의 `page`로 잘려서 구현

- 대신에 의미가 필요한 것들은 `segment table`에서 관리

- 👍🏻 `Protection`, `Sharing`설정 수월
- 👍🏻 Allocation, `external fragmentation` 문제 발생하지 않음

- 🆚 `pure segment`과의 차이점
- `segment table entry`가 `segment`의 `base address`를 가지고 있는 것이 아니라
- `segment`를 구성하는 `page table`의 `base address`를 가지고 있음

- ❗️ `segment`가 `page` 몇 개로 구성되는지 길이를 확인하고,
- 그 길이를 넘어서는 요청이 있으면 trap
