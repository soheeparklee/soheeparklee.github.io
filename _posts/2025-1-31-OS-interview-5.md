---
title: Interview_memory/ paging/ swapping
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅

## Dynamic Relocation 🆚 Dynamic Loading 🆚 Dynamic Linking

- **Dynamic Relocation**: runtime에 `logical address`에서 `physical address`로 `address binding`이 일어나는 것
- D**ynamic Loading**: 프로그램이 실행되면 통째로 메모리에 `load`되는 것이 아니라, 당장 실행에 필요한 부분만 `load`되는 것
- **Dynamic Linking**: 프로그래머가 작성한 코드와 라이브러리가 `link`되어 실행파일이 만들어지는데, 미리 `link`되어 있지 않고, 라이브러리가 호출되면 그 때 `link`되는 것. `stub`라는 코드가 이미 라이브러리가 메모리에 있는지 확인하여 동일 라이브러리의 메모리 중복 적재를 방지한다는 장점이 있다.

## Dynamic Loading 🆚 Overlays

- Dynamic Loading: 프로그램이 쪼개져서 현재 실행에 필요한 부분만 메모리에 올라가는 것
- Overlays: Dynamic Loading과 같이 메모리에 현재 실행에 필요한 프로세스 부분만 올라간다는 점에서 비슷하나, 목적이 다르다. 과거 메모리가 너무 작아 하나의 프로세스조차 올릴 수가 없을 때, 프로그래머가 수동으로 프로세스를 쪼개어 현재 필요한 부분만 메모리에 올리곤 하였음. 현대에는 쓰이지 않음.

## ✅ Linking이란?

- 라이브러리와 개발자가 만든 코드를 `link`해 실행파일을 만드는 과정
- Static Linking: 프로그래머다 작성한 코드 + 라이브러리 코드 모두 합쳐서 실행파일 생성
- 👎🏻 동일 라이브러리가 메모리에 여러번 적재, 비효율적인 메모리 사용
- Dynamic Linking: `link`를 `execution time`까지 미루고, 라이브러리가 실행되면 그제서야 `link`
- `stub`이라는 코드가 있어 메모리에 라이브러리가 이미 적재되어 있는지 확인, 없으면 불러옴.
- 👍🏻 동일 라이브러리는 메모리에 한 번만 적재

## ✅ 절대 주소 지정과 상대주소 지정의 차이점은 뭘까요?

- 절대 주소 지정: 물리적 메모리의 실제 주소를 할당해주는 방법
- 낮은 주소에 `OS`가 올라가고, 위에는 사용자 프로세스들이 적재됨

- 상대주소 지정: 프로세스마다 독자적으로 가지는 `logical address`를 할당해주는 방법
- 프로세스마다 독자적으로 가지기 때문에 0에서부터 시작

## ✅ 메모리 분할에 대해 설명해주세요.

- 메모리 분할은
- 여러 프로세스가 동시에 메모리에 적재되는 `multiprogramming`환경에서
- 메모리에 여러 프로세스를 적재하기 위해 메모리 공간을 나누는 것

- `continuous allocation`: `fixed-size partition allocation`, `variable-size partition allocation`
- `non-continuous allocation`: `paging`, `segmentation`, `paged-segmentation`

## ✅ Dynamic storage allocation problem (메모리 배치 기법 또는 메모리 관리 전략)에 대해 설명해주세요.

- in variable size partition allocation
- where to allocate memory in different sized partitions

- **First fit**: 가용 공간을 살펴보다 적재될 수 있는 공간이 있으면 즉시 `load`
- **Best fit**: 가용공간을 모두 살펴보고 사이즈에 제일 유사한 공간에 `load`
- 👍🏻 제일 유사한 공간 사이즈
- 👎🏻 시간 오래 걸림
- 👎🏻 작은 `hole`들이 많이 생길 수 있음

- **Worst fit**: 가용공간을 모두 살펴보고 제일 큰 공간에 `load`
- 👎🏻 작은 `hole`들이 많이 생겨 나중에 큰 사이즈의 프로세스가 왔을 때 공간 없음

## ✅ 외부 단편화와 내부 단편화의 차이가 뭔가요?

- **external fragmentation**: 새로 온 프로세스의 크기가 **커서** 처음 비어있는 `hole`에 들어가지 못하고, 다음 사이즈의 `hole`에 들어감
- 처음 비어있는 `hole`은 비어있게 됨
- **internal fragmentation**: 새로 온 프로세스의 크기가 **작아서** `hole`이 쪼개짐

## ✅ `external fragmentation`이 발생하는 이유

- `frame`의 크기가 균일하지 않기 때문
- segmentation

## ✅ 메모리 배치 기법중 하나인 colaescing(통합)에 대해 설명해주세요.

- external fragmentation을 보완하기 위한 방법으로,
- 인접한 두 `hole`을 합쳐 큰 `hole`을 만듬
- 그래서 큰 프로세스가 들어갈 수 있도록 함

## ✅ 메모리 배치 기법중 하나인 compaction(압축)에 대해 설명해주세요.

- colaescing를 했는데도 불구하고 프로세스가 들어가지 못할 때
- 모든 `hole`을 한쪽으로 몰고, 프로세스는 반대쪽으로 모아
- 아주 큰 하나의 을 만듬
- 👎🏻 거의 모든 프로세스의 주소 공간을 바꾸어야 하기 떄문에 오버헤드 비용이 크다

## ✅ 메모리 배치 기법중 하나인 버디 시스템에 대해 설명해주세요.

- `fixed-size partition allocation`의 내부 단편화, `variable-size partition allocation`의 외부 단편화를 보완하기 위한 방법
- `buddy`라는 블록들을 2의 제곱 크기로 나누었다, 합쳤다 하면서 제일 비슷한 크기의 블록에 프로세스 할당
- 메모리 공간이 다 쓰이고 해제되면 공간 합치기 가능

## ✅ 가상 주소와 물리 주소(실주소)에 대해 설명해주세요.

- `logical address`: 프로그램이 독자적으로 가지는 `virtual memory`의 주소
- `physical address`: 물리적 메모리에 실제 `load`된 주소

## ✅ 가상 주소를 물리 주소(실주소)로 어떻게 변환할까요?

- `address binding`이라고 함
- `MMU`라는 하드웨어가 담당
- `MMU`는 `base register(relocation register)`, `limit register`을 가지고 있음
- `limit register`을 통해 `address binding`요청이 내 주소공간 내에 있는 요청인지 확인
- 적합한 요청이면 `base register(relocation register)`에 `logical address`를 더해서 `physical address`를 구한다.

## ✅ Types of address binding?

- `address binding` 시점에 따라 구분
- **compile time**: absolute code
- **load time**
- **runtime(execution time)**: `swapping`, `dynamic relocation`, `compaction`

## ✅ address binding은 누가 담당하나요?

- 하드웨어 `MMU`
- 운영체제는 `address binding`에 관여하지 않음

## ✅ `MMU`의 기능과 가지고 있는 register에 대해 설명해주세요

- Memory Management Unit
- `address binding`을 담당하는 하드웨어
- `base register(relocation register)`: `physical memory`에서 프로세스가 시작하는 위치
- `limit register`: 프로세스의 크기

## ✅ 왜 `MMU`는 `limit register`를 가지고 있어야 할까?

- 프로그램이 잘못된 `address binding` 요청을 하는 경우
- (자신의 주소공간을 넘어선 `address binding` 요청을 하는 경우)
- (각 프로세스는 자신의 주소공간만 접근할 수 있음)
- 요청을 차단하기 위해서

## ✅ CPU가 바라보고 실행하는 주소는 어떤 주소일까요?

- `logical address`
- CPU는 `compile`된 기계어를 실행
- 그리고 `compile`하면 `logical address`를 생성

## ✅ Swapping이란 무엇인가요?

- 중기 scheduler이 메모리가 꽉 차면 `Multi Programming Degree`를 유지하기 위해 프로세스를 `backing store/swap area`로 쫒아냄
- 메모리에 올라온 프로세스의 주소 공간 전체를 디스크의 스왑 영역에 일시적으로 내려놓음
- 👍🏻 메모리에 올라온 프로세스의 수 조절

## ✅ Swapping의 과정을 설명해 주세요.

- 1. 중기 scheduler이 쫒아낼 프로세스 선정
- 2. 프로세스의 메모리 주소 공간을 통째로 `backing store/swap area`로 쫒아냄

## ✅ Swapping의 장단점을 설명해 주세요.

- 👍🏻 메모리에 올라온 프로세스의 수 조절
- 👍🏻 실제 물리 메모리보다 더 많은 프로세스를 수용할 수 있도록 물리 메모리가 초과 할당될 수 있음
- 👎🏻 `backing store/swap area`는 `DISK`공간이기 때문에 `I/O`가 느리다

## ✅ 메모리 배치 기법중 하나인 페이징에 대해 설명해주세요.

- noncontinuous하게 프로세스를 메모리에 같은 크기의 `page`에 적재
- 논리적 메모리, 물리적 메모리를 동일 크기의 `page frame`으로 나누고
- `page table`로 `address translation`

- 👍🏻 `external fragmentation`발생하지 않음
- 👎🏻 `internal fragmentation`발생
- 👎🏻 메모리를 2번 접근해야 한다
  - `address translation`위해 메모리의 `page table`접근
  - 실제 데이터 접근
  - 💊 속도 향상 위해 `TLB`

## ✅ 왜 `page table`은 메인 메모리에 올라가 있나요?

- `page table`은 각 프로세스마다 만들어져야 하고,
- `32bit`환경에서 저장해야 하는 데이터가 많기 때문에 메모리에 올린다

## ✅ `page table`에는 무엇이 저장되어 있나요?

- 페이지 번호와
- 물리적 메모리의 몇 번째 프레임에 페이지가 들어있는지에 대한 정보

- `PTBR`: base register, 메모리 내 `page table`위치
- `PTLR`: length register, `page table`의 크기

## ✅ `page table`의 길이는 왜 알고 있어야 할까요?

- 각 프로세스는 자신의 주소공간만 접근 가능
- 내 `page table`을 넘어서는 요청하면 ➡️ TRAP

## ✅ 페이징에서는 가상 주소를 물리 주소(실주소)로 어떻게 변환할까요?

- `page table`사용
- `logical address`은 `p`, `d`로 이루어져있고

  - `p`: page 번호
  - `d`: page내에서 얼마나 떨어져 있는지 offset

- `page table`에서 `p`를 찾아 `f`를 얻고
- `f`: 물리적 메모리에서 페이지 시작 위치
- `f`에 를 더해서 `physical memory address`를 얻는다

## ✅ `TLB`의 목적은?

- 페이징 기법에서 `address translation`위해 `page table`을 접근하는데 시간 걸림
- 따라서 일종의 `cache`인 `TLB`에 주소를 저장하고, 속도 향상

- `TLB`에는 `p: page number`, `f: 물리적 메모리에서 페이지 시작 위치`가 저장되어 있음
- 👎🏻 `cache`이기 때문에 `context switching`일어나 프로세스 바뀌면 다 바꾸어야 함
- 👎🏻 `cache`이기 때문에 모든 주소 저장은 불가, index없어서 다 찾아봐야 함
- 💊 associative register 사용: parallel search

- `TLB hit`일 수록 `address translation time` 효율적

## ✅ `Two level page table`란 무엇인가요?

- `page table`이 메모리에서 많은 부분을 차지하고, 심지어 `page table`이 다 쓰이는 것도 아님
- 이를 해결하기 위해 `page table`을 `page`로 만든다
- 두 개의 `page table`을 두고 `outer page table`, `inner page table`
- 사용되지 않는 값에 대해서는 `null`값으로 설정

- 👍🏻 메모리 공간 효율성
- 👎🏻 주소변환까지 포함해 메모리 3번 접근해야

## ✅ `page table`의 `valid, invalid bit`이란?

- `valid`: 현재 요청하는 `page`가 물리적 메모리에 올라와 있다
- `invalid bit`: 물리적 메모리에 올라와 있다 OR 프로스램이 사용하는 메모리가 아니다

## ✅ `Inverted page table`이란?

- 물리적 주소에 대해 `page table`을 만들어서
- `system-wide`하게 `page table`이 하나만 존재

## ✅ `Shared Pages`란?

- 프로세스들이 공유하는 `code`부분에 대해서는 물리적 메모리에 한 번만 적재
- 이를 달성하기 위해서는
  - 1️⃣ 논리적 주소도 같아야 한다
  - 2️⃣ `read-only`만 가능해야 한다

## ✅ 메모리 배치 기법중 하나인 세그멘테이션에 대해 설명해주세요.

- 프로세스를 분할해서 메모리에 올리는데, 의미 단위인 `segment`로 분할
- `code`, `data`, `stack`
- `segment`의 크기는 모두 다르다

- `logical address` = `s` + `d`
  - `s`: segment 번호
  - `d`: segment내에서 얼마나 떨어져 있는지
- `segment table`에는 `limit`, `base`저장

  - `limit`: segment의 길이
  - `base`: 물리적 메모리에서 segment시작 위치

- 물리적 주소: `base` + `d`

- `STBR`: base register
- `STLR`: length register

- `segment table`에서는 요청이 들어왔을 때 두 가지 확인
- 1️⃣ `d`가 `limit`을 넘어서지 않는지
- 2️⃣ `s`가 보다 작은지

- 👍🏻 의미 단위로 프로세스를 나누기 때문에 페이징보다 `Sharing`, `Protection(read-write)`측면에서 관리 효율
- 👎🏻 allocation 문제(first-fit, best-fit, worst-fit)
- 👎🏻 external fragmentation 문제 발생

## ✅ Paged Segmentation에 대해 설명해주세요

- 프로세스를 `segment`로 나누고 이 `segment`를 `page`로 나누어 메모리 적재
- `segment table`, `page table`모두 필요

- 👍🏻 `Sharing`, `Protection(read-write)`측면에서 관리 효율
- 👍🏻 Allocation, external fragmentation 문제 발생하지 않음

## ✅ `virtual memory`에 대해 설명해주세요.

- 프로세스가 실행되었을 때 독자적으로 가지는 메모리 공간
- 프로세스마다 가상 주소 할당
- 0에서 시작
- `virtual memory`중 일부는 메모리에 적재, 일부는 디스크 `swap area`에 적재

- 물리적 메모리의 연장 공간으로 `swap area`사용 가능
- 👍🏻 프로그램은 물리적 메모리 크기 제약 극복

## ✅ `Demand Paging`이란?

- demand가 있으면 그 페이지를 paging, 즉 메모리에 올리겠다

## ✅ `page replacement`에 대해서 설명해주세요.

- `page fault`가 발생하여 물리적 메모리의 빈 `frame`에 디스크에서 읽어온 값을 저장하려고 하는데
- 빈 `frame`이 없을 때
- 기존 `frame`을 쫒아내어 빈 공간 마련

## ✅ `page fault`란?

- CPU가 참조하려는 `page`가 물리적 메모리에 올라와있지 않은 상황
- 디스크에서 값을 읽어와 메모리의 빈 `frame`에 저장해야 함

## ✅ `page fault`를 최소화하려면 어떻게 해야 하나요?

- `temporal locality`: 최근 참조된 `page`는 또 참조될 가능성이 높다
- `Locality of reference`: 참조되는 `page`에 일종의 예상가능성이 있다

- 이런것들을 고려해 어떤 페이지를 `replace`할지 잘 생각해야함
- `FIFO`, `LFU`, `LRU`, `clock algorithm`
  `

## ✅ 페이지 교체 알고리즘 FIFO에 대해 설명 해주세요.

- 물리적 메모리에 가장 먼저 올라온 `page`를 `replace`

## ✅ 페이지 교체 알고리즘 LRU에 대해 설명 해주세요.

- 참조 시간이 가장 오래된 `page`를 `replace`
- `temporal locality`반영
- `linked list`로 구현, `O(1)`

## ✅ 페이지 교체 알고리즘 LFU에 대해 설명 해주세요.

- 참조 횟수가 가장 적은 `page`를 `replace`
- `heap`으로 구현, `O(logN)`

- `In-cache LFU`: 물리적 메모리에 올라온 순간부터 참조 횟수 count
- `Perfect LFU`: `page`의 과거 총 참조횟수 count

## ✅ 왜 paging system에서는 LRU, LFU가 불가능한가?

- OS는 `page fault`가 날 때만 관여, 참조 횟수/참조 시간 알 수 있음
- `address translation`에는 `MMU 하드웨어`가 담당, OS는 모름
- 따라서 `page fault`가 발생하지 않으면 OS는 참조 횟수/참조 시간 알 수 없음
- 따라서 OS는 정확한 참조 횟수/참조 시간을 알 수 없기 때문에 LRU, LFU가 불가능

## ✅ 페이지 교체 알고리즘 clock 알고리즘에 대해 설명해주세요.

- Second Chance algorithm(시계 바늘이 다시 올동안 참조되어야 함)
- `Not Recently Used`
- `LRU`를 근사시킨 알고리즘
- 특정 시간동안 참조되지 않은 `page`를 `replace`
- `page`를 원형으로 배치하고
- 프로세스가 참조되면 참조 비트 1
- OS바늘은 참조비트가 1이면 0으로 바꾸고 지나가고
- 참조비트가 0이면 `replace`
- OS바늘이 한 바퀴 도는 동안 참조되지 않은 `page`를 `replace`

## ✅ clock 알고리즘의 개선 방법?

- reference bit(access bit)외에도
- modified bit(dirty bit)을 두어 새로 바뀐 값은 저장하고 `replace`

## ✅ Page Frame Allocation이란? 필요성은?

- 프로세스별로 다르게 `frame`을 할당
- 프로세스 수행에 필요한 최소한의 `frame`이 있기 때문

- equal allocation
- priority allocation
- proportional allocation: 프로세스 크기에 따라 `frame`을 다르게 할당

## ✅ Two types of replacement methods in allocation?

- Global Replacement: 프로세스가 전체 메모리 경쟁, 다른 프로세스의 `frame` 빼앗을 수 있음
- Local Replacement: 각 프로세스에게 일정 `frame`을 할당, 프로세스 내부에서 경쟁

## ✅ Thrashing에 대해 설명해주세요.

- 프로세스가 실행되기 위해 최소 `frame`의 수를 할당받지 못해
- memory에 너무 많은 프로세스가 올라가
- `pafe fault`가 지나치게 많이 발생하여
- `cpu utilization`이 감소하는 것

- `cpu utilization`이 낮으면, OS는 메모리에 프로세스를 더 많이 적재
- 프로세스는 수행을 위해 일정 수 이상의 이 `frame`이 필요한데
- 메모리에 너무 많은 프로세스가 있어 `frame`을 할당받지 못함
- `page fault`계속 발생
- `cpu utilization` 감소

## ✅ 워킹 알고리즘에 대해 설명해주세요.

- `Thrashing`을 보완하기 위한 방법으로
- 프로그램 실행에 필요한 최소 `frame`을 `working set`으로 만들고
- 이 `working set`이 메모리 적재되는 것은 보장해준다
- `working set`이 한꺼번에 올라갈 만큼 메모리에 공간이 없으면 아예 적재하지 않음
- `working set window`는 가변적

## ✅ 페이지 부재 빈도 알고리즘에 대해 설명해주세요.

- `page fault rate`에 상한값, 하한값을 두고
- 상한값을 넘어서면 `frame`을 더 많이 할당
- 하한값보다 떨어지면 `frame`을 빼앗음




절대 주소 지정과 상대주소 지정의 차이점은 무엇일까요
절대주소지정은 주로 어디에서 사용될까요? 
상대주소가 절대주소로 변환되는 과정? Address binding. Mum 라는 하드웨어. 2가지의 레지스터. 프로세스가 어디에서 시작하는지 base 레지스터를 갖고있고. Limit 값을 갖고있음. 논리적 주소에 p와 d 값을 갖고있는데, P 는 페이지번호, d 는 페이지에서 얼마나 떨어져있는지의 offset. 
버디 시스템
고정분할과 변동분할방식을 보완하기위해 나왔음. 하나의 메모리공간을 2^n 으로 나누고, 하나하나를 버디라고 부르고있음. 
장점은 외부단편화, 내부단편화를 줄일수있다.
내부단편화는 어떨때 발생하나요? -> 프로세스 메모리가 빈공간에 들어가려할때, 이 메모리보다 더 커서 조각이 쪼개질때 남은공간. 
외부단편화는 어떨때 발생하나요? -> 외부단편화는 어떤 프로세스가 실행되다가 나갔을때 비어있는곳에 들어가려했는데, 거기보다 작아서 더 큰공간에 들어가야할때
페이징과 세그멘테이션의 차이를 설명해주세요
페이징은 page 라는 동일크기의 분할조각. 세그멘테이션은 어떤 의미단위인 세그먼트로 나누는것. 크기가 동일하지않다 라는 특징. 
어떤 의미단위라는것은? 코드, 데이터, 스택 등, 필요에의히 함수가될수도있고, 공간전체가 될수도있다. 
세그멘테이션에서 발생하는 외부단편화는 어떻게 해결할수있을까요?
통합이나 압축의 개념차이? 
어떤 프로세스가 메모리에 적재되려고할때 인접한 홀을 합쳐서 더 큰 홀을 합치는것. 더 크기가 큰것도 적재될수있음. Compaction 압축은 메모리에 적재되려고하는 프로세스의 크기가 만들어진 홀보다 커서 더 큰 홀이 필요할떄 메모리에 한쪽으로는 모든홀로 몰고, 다른홀로는 프로세스를 몰아서 큰 홀을 만드는것. 
자바의 gc 는 어떻게동작하는가? 
Gc 가 주기적으로 한번씩 사용되지않는 데이터들을 프로그래머가 수작업할필요없이, 한번씩 정리해준다. 한번씩 청소하는것과 부분적으로 정리함

가상메모리는 무엇인가요?
실제론 존재하진않지만, 프로그램이 독자적으로 가지는 공간. 장점은 물리적메모리의 한계를 넘어서서 프로세스에 할당할수있다. 라는 장점이있다. 
단점은 어떤게있을까요?
Process 가 실행됐을때 자기만의주소를 물리적주소로 바꿔야하기때문에 과정이 추가되기때문에 효율적이지않다.
페이지와 프레임의 개념차이를 알고있나요?
페이지는 논리적주소를 쪼갠것. 물리적 메모리에서 동일한 크기로 분할해놓은것을 프레임이라고함. 페이징과 프레임의 크기가 같아서 1:1 매핑함.
페이지 교체란
Page 교체는 메모리에 어떤 프로세스를 오리려는데 메모리가 꽉차서 어떤 프로세스를 쫒아내고, 새로운 프로세스를 올리는것.
페이지 교체 알고리즘은 어떤것들이 있을까요?
Opt ?? Fifo, LRU, LFU, clock 알고리즘
LRU LFU 는 어떻게 차이가있나요?
LRU 가장 오래전에 참조된것. LFU 는 ?? LRU 는 linked list, LFU 는 어떤걸로 heap 으로 구현됩니다.
LRU 와 clock 알고리즘의 차이도 말씀해주세요
가장 오래전에 참조된 페이지, clock 은 최근에 참조되지않은 페이지를 교체하는것.

쓰레싱이란?
CPU 사용율이 낮으면, os 는 메모리에 프로세스가 없다 라고 생각함. 메모리에 프로세스를 계속 올리게됨
쓰레싱은 어떻게 방지할수있나요?
Work set 방식 -> 로컬리티. 프로세스가 한번에 참조하는 메모리의 집합. Worksheet window 라는것. 이 윈도우가 올라가는것을 보장하는 방식. 공간이 확보되지않으면 work set 을 올리지않음. 
계속해서 공간이 확보되지않으면 프로세스는 영원히 실행안되나요? Os 는 어떻게 해결할수있을까요?
Page fault trace 방식 -> 페이지 부재가 발생하는 하한선과 상한선을 정함. 페이지폴드가 상한선을 넘으면 프레임을 할당해주고, 하한선을 넘으면 프레임을 뺏는다
Swapping 의 개념과 장단점
메모리가 꽉찼을때 스왑영역으로 쫒아내는것. 중기스케줄러가 담당함. 다양한 알고리즘을 활용해서 잘 쫒아내야함. 스와핑을 했을때 장점은 물리적메모리보다 넘어서 할당할수있고, 단점으로는 swap out 이 됐을때, Swap in 해야하는 관리포인트가 생김.
스왑영역이란건 어떤 영역을말하나요?
백업공간?? 디스크에 있는공간을 말한다. 
디스크에 있는 페이지를 탐색해야하는데 이때 활용되는 알고리즘은 어떤게 있을까요?

이력서는 간단하게 쓰되, 포트폴리오에서 자세하게 적자 (이력서는 보통 인사팀에서 보는경우가많음)
소규모 회사에는 이력서단계부터 자세하게 쓰
진행했떤 프로젝트의 시;스템 아키텍처를 그릴수있을정도로 공부해야하고
아키텍처마다 각 특징을 잘 알아두셔야함 (route53, ec2, alb, rds 이런 각 component 들 잘. ㅗㅇ부해야하고)
현재 아키텍처의 문제점이나, 개선할점
JPA 를 쓰셨으니까, JPA 의 특징에 대해 자세하게 공부 + 다른 ORM 과의 차이점
실무에서는 join 은 잘 하지않고 어플리케이션 서버에서 필요한 데이터를 긁어와서 처리하거나, 테이블을 역정규화 하는 경우도 있다.
여러테이블을 join 해서 가져오면 성능이 떨어질수있을거ㅏㅌ은데, 이런건 어떻게 대비하고 처리했는지

프로젝트에 대해 해결하고자했던 문제와 어떻게 해결했는지,MVP 는 무엇인지에 대해 자세하게 적기.
구현한 프로젝트의 시스템 아키텍처에 대해 자세하게 공부하기