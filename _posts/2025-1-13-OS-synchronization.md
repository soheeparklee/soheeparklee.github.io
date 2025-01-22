---
title: KOCW_Process Synchronization/Race Condition/Semaphore/Mutex
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ Parallelism

> 병렬성

- 실제로 동시에 작업 처리
- multi processor

## ✅ Concurrency

> 병행성

- 동시에 작업이 처리되는 것처럼 보이게 해 주는 것
- 한 개의 `CPU`가 다수의 프로세스 번갈아 수행 ➡️ `inter living`
- 매우 빠른 `CPU`처리 속도로 `inter living`이 빠르게 이루어짐
- 사용자 입장에서는 여러 프로그램이 동시작동하는 것처럼 느낀다

<br>

- 👎🏻 **Problems of Concurrency**
- 👎🏻 컴퓨터에서 자주 쓰이는 변수 또는 함수는 모든 프로세스들이 접근 가능한 전역 메모리에 접근해 공유
- 👎🏻 프로세스 간 메모리 공유는 문제 야기 가능

```
프로세스 P1: echo 함수 호출 ➡️ getchar 함수 호출 ➡️ x 입력받음 ➡️ out 변수에 저장
프로세스 P2: P1을 선점하여 CPU를 빼았음
프로세스 P2: echo 함수 호출 ➡️ getchar 함수 호출 ➡️ y 입력받음 ➡️ out 변수에 저장
프로세스 P1: 다시 CPU할당받음, 이전에 수행중이던 부분부터 이어서 수행
⚠️ 그러나 out 변수에는 이제 y가 저장되어 있음
⚠️ x가 유실되었음

이 문제의 원인: 두 개의 프로세스가 하나의 전역변수 out 변수를 공유했기 때문이다.
```

- 💊 특정 시점에 오직 하나의 프로세스만이 echo 함수 호출이 가능해야 한다.
- 💊 따라서 **공유 데이터에 대한 접근 제한**필요, **프로세스 동기화**필요

## ✅ 데이터의 접근

- 읽고
- count 연산
- 저장
- 이 과정은 `atomic`하게 실행될 수가 없다
- 이 도중에 `Race Condition`발생 가능

## ✅ Race Condition

> 다수의 프로세스나 쓰레드가 공유 자원을 **동시에** 읽거나 쓰려고 하는 상태 <br>
> 여러 프로세스들이 **동시에** 공유 데이터에 접근하는 상황

- ⚠️ 여러 프로세스들이 **동시에** 공유 데이터에 접근하면
- 마지막에 공유데이터를 다룬 프로세스가 누구인지에 따라 결과가 최종연산결과가 달라진다.

<br>

- 데이터 접근이 `atomic`하게 실행되지 않아 발생
- 여러 프로세스들이 동시에 공유 데이터를 접근하는 상황에서
- 데이터 최종 연산 결과가 마지막에 그 데이터를 쓴 프로세스에 따라 달라지는 문제

<br>

- 💊 to prevent `race condition`, `concurrent processes` needs to be `synchronized`

## ✅ Race Condition이 언제 발생하는가

- 분명 프로세스 간에는 `memory address space`를 공유하지 않는다고 했는데
- 왜 `Concurrency problem`, `Race Condition`이 발생하나요?

#### 1️⃣ **kernel 수행 중 인터럽트 발생 시**

> kernel mode 도중 interrupt

- `프로세스 A`가 커널모드 실행중이었는데 **인터럽트**가 발생해 `인터럽트 처리루틴`이 실행됨
- 그러면 `프로세스 A`, `인터럽트 처리루틴 ISR(Interrupt Service Routine)`도 커널 코드이므로
- 공유데이터: `kernel address space`공유
- 따라서 커널모두 수행 중 interrupt가 발생하면 `kernel address space` 공유 데이터에 동시(중복) 접근 발생
- ➡️ race condition

<img width="425" alt="Screenshot 2025-01-14 at 00 36 01" src="https://github.com/user-attachments/assets/ab3c8b6b-f006-4463-bc1f-7fb99fc99c76" />

- 💊 프로세스가 `kernel mode`에서 실행중일 때는 인터럽트를 `disable`시키고
- `kernel mode` 끝나면 인터럽트 `enable`시킨다.

#### 2️⃣ **프로세스가 system call로 kernel 수행 중 context switch가 일어나는 경우**

> preempt a process running in kernel <br>

- 커널 내부 데이터를 접근하는 루틴들 간에 발생
- `프로세스 A`, `프로세스 B`의 각 `memory address space` 간 `data sharing`이 없음!
- `프로세스 A`가 `system call`을 하고 `kernel address space`의 `data`를 `access/share`하고 있음
- 이 작업 중간에 `프로세스 B`가 CPU를 `preement`
- 그리고 `프로세스 B`가 `system call`을 하고 `kernel address space`의 `data`를 `access/share`
- 예를 들어 `timer`
- ➡️ 그러면 `race condition` 발생
- 커널의 데이터를 건드리던 도중에 프로세스가 바뀌어 다른 루틴 실행

<img width="423" alt="Screenshot 2025-01-14 at 00 31 14" src="https://github.com/user-attachments/assets/c5e8af0d-168b-41e2-a011-707553a64d35" />

<br>

- 💊 프로세스가 `kernel mode`에서 실행중일 때는 CPU를 `preement`하지 않는다.
- `kernel mode`에서 `user mode`로 돌아갈 때 `preement`한다.
- `preement disable/enable`

#### 3️⃣ `Multi processor system`**, CPU가 여러개 있는 상황**

- `shared memory`내의 `OS kernel data`
- 공유 메모리를 사용하는 프로세스들
- `memory address space`를 공유하는 `CPU process`가 여럿 있는 경우 `race condition`의 가능성이 있다.
- 여러개 CPU 프로세스가 동시에 `OS kernel data`에 접근한다
- `Multi processor system`의 경우 `interrupt disable/enable`로 해결되지 않음
  <br>

- 💊 방법 1: 한번에 하나의 CPU만이 `kernel`에 들어갈 수 있게 허용
  - 운영체제 **전체에** `lock`을 걸어서 하나의 CPU만 독점해서 쓰기
  - 👎🏻 여러개 CPU 중 하나만 `kernel mode`에 들어갈 수 있게 하면 나머지 CPU는 기다리느라 오버헤드가 크다
- 💊 방법 2: 커널 내부에 있는 각 공유 데이터에 접근할 때마다 그 데이터에 대해 `lock/unlock`
  - 운영체제 `kernel`의 **각 데이터마다** `lock`을 걸어서 사용
  - 👍🏻 그 데이터를 건드리지만 않는다면 다른 CPU가 `kernel`쓰고 있어도 나도 사용 가능

#### 4️⃣ **공유메모리를 사용하는 프로세스 사이에서 발생**

## ✅ Process Synchronization

> 🟰 concurrency control 병행 제어 <br>
> 프로세스 간 실행 순서 정해주기 <br>

- ⚠️ 공유 데이터`shared data`의 동시 접근`concurrent access`은
- 데이터 불일치 문제`inconsistency`를 발생시킬 수 있음
- 💊 공유데이터의 `consistency`유지를 위해
- 협력 프로세스`cooperating process`간의 실행 순서 `orderly execution`을 정해주는 메커니즘 필요

## ✅ Critical Section Problem

- ✔️ **Critical Resource**
- 두 개 이상의 프로세스가 동시에 사용할 수 없는 공유자원

- ✔️ **Critical Problem**
- 공유자원에 접근하는 프로그램 코드
- `n`개의 프로세스가 공유 데이터를 동시에 사용하기 원하는 경우
- 각 프로세스의 `code segment`에는 공유 데이터에 **접근하는 코드** `critical section`이 존재

<img width="378" alt="Screenshot 2025-01-14 at 00 55 11" src="https://github.com/user-attachments/assets/f5154ac1-02b4-47e8-bc86-d929fcb61656" />

- 💊 하나의 프로세스가 `critical section`에 있을 때 다른 모든 프로세스는 `critical section`에 **들어갈 수 없어야** 한다.
- 💊 예를 들어 `critical section`에 들어가기 전에 `lock`을 걸고, 나올 때는 `lock`을 풀기

<img width="127" alt="Screenshot 2025-01-14 at 11 43 43" src="https://github.com/user-attachments/assets/9d883220-564c-4fbf-81e3-9164afe92c0c" />

## ✅ Mutual Exclusion

> 상호 배제
> 특정 시점에 하나의 프로세스만이 `critical section`에 접근할 수 있도록 한다.

- 다수의 프로세스가 동작하는 `concurrent system`에서
- 어떤 프로세스가 공유 데이터에 접근하고 있으면
- 다른 프로세스는 그 공유데이터에 접근할 수 없도록 하는 방법

## ✅ Mutual Exclusion Solutions

- ✔️ **SW solutions**
  - Dekker’s algorithm (Peterson’s algorithm)
  - Dijkstra’s algorithm, Knuth’s algorithm, Eisenberg and McGuire’s algorithm, Lamport’salgorithm

<br>

- ✔️ **HW solution**
  - TestAndSet(TAS) instruction

<br>

- ✔️ **OS supported SW solution**
  - Spinlock
  - Semaphore
  - Eventcount/sequencer

<br>

- ✔️ **Language-Level solution**
  - Monitor

## ✅ Process Synchronization 문제를 풀기 위한 조건

> 🟰 Mutual Exclusion를 위한 조건

- ✔️ **Mutual Exclusion**
- 프로세스가 동시에 `critical section`에 들어가면 안 된다.
- 하나의 프로세스가 `critical section`에 진입해서 작업을 실행중이면
- 다른 모든 프로세스들은 `critical section`에 들어가면 안 된다.

<br>

- ✔️ **Progress**
- `CS`에 진입한 프로세스가 없고, `CS`에 진입하려는 프로세스가 있으면 `CS`진입을 허용한다.
- 아무도 `critical section`에 들어가 있지 않은 상태에서
- `critical section`에 들어가고자 하는 프로세스가 있으면
- `critical section`에 들어가게 해 주어야 한다.

<br>

- ✔️ **Bounded Waiting**
- 프로세스가 `critical section`에 들어가려고 기다리는 시간이 *유한*해야 한다.
- 즉, starvation이 발생하면 안된다.
- 특정 프로세스만 `critical section`에 영원히 못 들어가는 문제가 생기면 안 된다.
- 프로세스가 `critical section`에 들어가려고 요청한 순간부터 그 요청이 허용될 떄가지 다른 프로세스들이 `critical section`에 들어가는 횟수가 *제한*되어야 한다.

<br>

- ✔️ **동일 속도**
  - 모든 프로세스의 수행 속도는 0보다 크다
  - 프로세스 간의 상대적인 수행 속도는 가정하지 않는다

## 💡 Process Synchronization Algorithm 1

- `turn 변수`: 프로세스의 번호, `CS`진입 차례 표시
- `turn 변수`로 내 차례인지 확인하고
- 내 차례가 아니면 기다리고
- 내 차례면 `critical section` 실행
- 나올 때 상대방 차례로 바꿔주기

```
int turn;
turn = 0; //0번 프로세스가 while문 탈출해 CS진입 가능

do{
  while(turn !=0 ); //my turn? 내 차례인가?
  critical section
  turn = 1; //now it is your turn 상대방 차례로 바꿔주기
  remainder section
} while(1);
```

- `Mutual exclusion` ⭕️
- `Progress` ❌

- 👍🏻 둘 이상의 프로세스가 `critical section`에 들어가는 일은 없다
- 👎🏻 **과잉양보**: 특정 프로세스가 `critical section`에 더 자주 들어가야 한다면 문제 발생

  - 왜냐하면 반드시 한번씩 교대로 들어가야만 하기 때문 `swap turn`
  - 상대가 `turn 변수`를 내 값으로 바꿔줘야만 내가 들어갈 수 있음
  - 특정 프로세스가 `critical section`에 더 빈번하게 들어가야 한다면?
  - 또는 상대방이 `critical section`에 안들어가면, 영원히 내 차례는 안 온다.

- 💡 따라서 이 알고리즘은 `Progress`를 만족하지 못했음 ❌
- `CS`에 진입중인 프로세스가 `turn`을 바꿔줘야지만 다른 프로세스의 `CS` 진입 허용이 되기 떄문이다

## 💡 Process Synchronization Algorithm 2

- `boolean flag`: 프로세스가 `CS`에 진입하겠다는 의사 표현
- initially `flag[모두] = false;` 아무도 `CS`에 없음

- `프로세스 i`가 `CS` 들어가고 싶으면 깃발 `flag`를 든다 `flag[i]==true`
- 그리고 다른 프로세스의 `flag`를 확인해야 한다.
- `프로세스 j`의 `flag`가 올려져있다면, 이미 `프로세스 j`가 `CS`에 진입한 것이다
- `프로세스 i`는 `while`문에서 `busy waiting`
- `프로세스 j`가 `CS`에서 나오면서 `flag[j] = false;`로 깃발을 내리면
- 그제서야 `프로세스 i`는 `while`문에서 나오면서 `CS`진입

```
boolean flag[2];

do{
  flag[i]=true; //나 CS들어갈래 깃발 들기, 의사표현
  while (flag[i]); //너도 들어가고 싶니? 그럼 나 기다릴게
  critical section
  flag[i] = false; //나 이제 나왔으니 깃발 내림
  remainder section
} while(1);
```

- `Mutual exclusion` ⭕️
- `Progress` ❌
- `Bounded Waiting` ❌
- 👎🏻 두 개 프로세스가 2행까지 수행 후 끊임없이 양보하는 상황 발생
- 2행에서 프로세스가 `CS`는 들어간게 아니라 의사표현만 한건데, 들어간 것으로 생각하고 눈치만 보다가 아무도 `CS`에 못 들어감
- 👎🏻 모든 프로세스의 `flag`가 올라가 있다면 모든 프로세스는 `while`문에서 무한 대기

## 💡 Peterson's Algorithm

> use both `boolean flag` and `turn` for synchronization

- 깃발을 사용해 `CS`에 들어가고자 하는 의사표현
- 상대 프로세스가 `CS`에 들어갔는지 확인
- 동시에 두 프로세스가 깃발을 들면, _깃발을 든 프로세스끼리_ `turn`을 확인해 번갈아 들어감

```
do{
  flag[i]==true; //나(i) CS들어가고 싶다고 깃발 들기
  turn = j; //turn을 상대 프로세스 차례로 바꾼다
  while (flag[i] && turn == j ); //상대방이 깃발을 들었고, turn이 j번 프로세스이므로
                                //내 차례 아님, while문에서 busy waiting
  critical section
  flag[i] = false; //나 이제 나왔으니 깃발 내림
  remainder section
} while(1);
```

- `Mutual exclusion` ⭕️
- `Progress` ⭕️
- `Bounded waiting` ⭕️

- 👎🏻 Busy waiting(Spin lock)

## ⚠️ Busy waiting(Spin lock)

- 내가 `CS`에 못 들어가는 상황에도
- `while문`을 돌며(`spin`하면서) `while문`에서 반복대기
- 👎🏻 계속 `CPU`와 `memory`를 쓰면서 기다린다
- 💊 semaphore, block, wakeup

## 💡 Synchronization Hardware TAS

> Test and Set <br>
> Synchronization을 도와주는 `Hardware`가 있으면 `race condition`문제를 쉽게 해결할 수 있다. <br>

- 복잡한 알고리즘 코드 대신
- 하드웨어 적으로 `Test & Modify`/`read & write`를 `atomic`하게 수행할 수 있도록
- 지원하는 경우 `race condition`문제를 간단히 해결할 수 있다.

```
--- Test & Modify 🟰 Test And Set ---

- lock변수값을 읽어가고 read: CS에 누가 있는지 확인하고
- lock변수값을 true로 만든다 write: lock을 건다, set lock
이 두 동작을 atomic하게 실행한다.
👍🏻 간결하게 프로세스 동기화 구현
```

```
Synchronization variable:
boolean lock = false; //아무도 CS에 안 들어갔다
                      //lock = true 누군가 CS에 들어갔다

do{
  while(Test_and_Set(lock)) //만약 lock이 0이었다면  => CS로 들어가며 lock을 1로 세팅
                            //CS 진입 전에 lock을 걸고, CS수행 후 lock을 풀고
  critical section
  lock = false; //lock을 풀어주기
  remainder section
}
```

## 💡 Semaphore

> synchronization을 도와주는 추상자료형

- synchronization문제를 해결하기 위해
- Semaphore 라는 변수를 두고
- 자원의 개수를 count하며 synchronization문제를 해결

<br>

- counting semaphore
- 도메인이 0 이상인 임의의 정수값(자원이 **여러개**)
- 주로 resource counting에 사용

- 앞의 방식들을 추상화시킴, _추상자료형_
- 자원의 개수를 `count`하고
- 남아있는 자원이 있는지 없는지 확인하기 위해
- `semaphore 변수 S`를 사용한다

<br>

- ✔️ **Semaphore 변수 S**
  - 변수값은 정수로 정의된다. `S = integer variable`
  - 이는 자원의 개수 표현

<br>

- 아래의 두 가지 `atomic 연산`에 의해서면 접근 가능
  - `P`: 자원을 *획득*하는 과정, lock을 거는 과정, `S--`
  - `V`: 자원을 *반납*하는 과정, lock을 풀어주는 과정, `S++`
- 이 `P`연산과 `V`연산이 `atomic`하게 실행된다고 **가정**, `Synchronization Hardware`사용

```
// Synchronization variable
semaphore S; // 1로 초기화 한다. 즉, 1개의 프로세스가 CS에 진입할 수 있다.

//자원을 획득하는 과정
//lock을 거는 과정
P(S): while (S =< 0) do no-op; //자원이 있는지 없는지 체크,
                               //자원이 없으면 wait,
                               // ⚠️ Busy waiting(Spin lock)
      S--; //자원 감소
      critical section 자원 쓰는 코드

//자원을 반납하는 과정
//lock을 풀어주는 과정
V(S): S++;
```

- 예를 들어 `S = 5`, 자원이 5개라는 의미
- `P연산`이 실행되면 자원 획득, 이제 여분 자원은 4개 남음
- 자원을 쓰는 코드는 `P연산`과 `V연산`사이에 있을 것
  <br>

- 👎🏻 하지만 이 코드도 **Busy waiting(Spin lock)** 문제를 해결하지 못함
  - `while (S =< 0)`으로 `critical section`에 들어갈 수 있는지 없는지 계속 체크
  - 내가 `critical section`에 못 들어가는 상황이면
  - 들어갈 수 있는지 없는지 계속 체크하는게 아니라
  - 체크 후 `lock` 해버리는 방법은 없을까?
  - 💊 Block/Wakeup Implementation

#### ❓ 자원의 개수를 세는 걸 굳이 semaphore변수로 하는 이유는?

- semaphore에서는 `P`연산과 `V`연산이 `atomic`하게 실행된다고 **가정**하기 때문이다
- `P`연산과 `V`연산이 `atomic`하게 실행하기 위해서는 `Synchronization Hardware`이 필요하다

## 💡 Semaphore with Block/Wakeup(Sleep lock)

> Semaphore ➕ Spin lock 해결

- `Spin lock`: 계속 `while`문 돌면서 `CS`에 들어갈 수 있는지 확인한다
- `Sleep lock`을 사용하므로써
- 내가 `critical section`에 들어갈 수 있는지 없는지 체크하고
- 들어갈 수 없으면 `lock`을 해버린다.
- 👍🏻 Busy waiting(Spin lock) 문제를 해결한다.
- 👍🏻 무의미한 체크 하는 것을 막는다
  <br>

- semaphore를 일종의 구조체처럼 두고
- semaphore를 `list`처럼 만들고
- 프로세스를 `queue`에 줄을 세운다.
- 기다리는 프로세스는 `block`
- `critical section`에 들어갈 수 있게 되면 `wakeup`

```
typedef struct
{
  int value; //semaphore
  struct process *L; //process wait queue
} semaphore;
```

- **block**과 **wakeup**을 다음과 같이 가정
- ✔️ `block`:

  - 프로세스 `block`: 프로세스가 CPU를 얻어도 소용 없는 상태
  - 커널은 `block`을 호출한 프로세스를 `suspend`
  - 이 프로세스의 `PCB`를 `semaphore`에 대한 `wait queue`에 넣음

- ✔️ `wakeup(P)`:
  - 공유데이터 쓰던 프로세스가 나가서 `critical section`가 비면
  - `queue`에서 기다리던 다음 프로세스 꺠우기
  - `block`된 프로세스 `P`를 `wakeup`시킴
  - 이 프로세스의 `PCB`를 `ready queue`로 옮김

```C
P(S): S.value--; //프로세스가 자원 쓰려고 함
      if ( S.value < 0 ) //남은 자원 없음, CS 못 들어감
      {
        block(); //CS못 들어가는 프로세스를 semaphore wait queue에 추가
      }
V(S): S.value++; //자원 반납
      if( S.value <= 0 )
      {
        wakeup(P); //remove process P from semaphore wait queue, wakeup
      }
```

## Busy wait 🆚 Block/Wakeup

- 어떤 방법이 더 좋은가?
- 일반적으로는
- `Busy wait`은 자원이 소진되고 없는데도 계속 있는지 체크하니 비효율적
- `Block/Wakeup`은 자원이 생겼을 때 `wakeup`해주니 훨씬 효율적
  <br>

- 하지만 만약 `critical section`이 _경합이 없는 상황이라면?_
- `Block/Wakeup`도 `Block/Wakeup overhead`가 발생하므로
- 별로 `CS`에 대한 경쟁이 없는 상황이라면
- `Block/Wakeup overhead`가 `Busy wait overhead`보다 커질 수 있음
  <br>

- 일반적으로는 `Block/Wakeup`이 좋음

#### 👎🏻 Semaphore의 문제점

- 코딩이 어렵다. `P`연산과 `V`연산을 잘 짜야 함
- ⚠️ 잘못짜는 경우 deadlock, starvation 발생 가능
- 정확성(correctness) 입증이 어렵다
- 자발적 협력(voluntary cooperation)이 필요하다
- 한번의 실수가 모든 시스템에 치명적 영향
- 💊 monitor

#### ☑️ Semaphore 종류

- ✔️ **counting semaphore**
  - 도메인이 0이상인 임의의 정수값
  - resource counting
- ✔️ **binary semaphore(mutex)**
  - 0 또는 1값만 가질 수 있음
  - mutual exclusion(lock/unlock)

## 💡 Mutex

> Binary semaphore <br>
> mutual exclusion의 준말 <br>

- 프로세스 **1개만(mutual exclusion)** CS에 들어갈 수 있다
- 이진 세마포어와 비슷

```C
Synchronization variable
semaphore mutex; //initially 1 = 1개가 CS에 들어갈 수 있다.

do{
  P(mutex);
  critical section
  V(mutex);
  remainder section
}while(1);
```

#### Binary semaphore 🆚 Mutex

- Mutex: `lock`을 설정한 프로세스만이 `unlock`을 할 수 있다.
- Binary semaphore: `lock`을 설정한 프로세스와 `unlock`하는 프로세스가 서로 다를 수 있다.

## ✅ Deadlock and Starvation

- ✔️ **Deadlock:**
- 둘 이상의 프로세스가 서로 상대방에 의해 충족될 수 있는 event를 무한히 기다리는 현상
- 여러 프로세스가 서로 얽혀 진행이 불가한 상태
- ✔️ **Starvation:**
- 🟰 infinite blocking
- 프로세스가 `suspend`된 이유에 해당하는 세마포어 큐에서 빠져나가지 못하는 현상

  <br>

- `S`와 `Q`가 1초로 초기화된 semaphore이라 하자
- 작업은 `S`, `Q`를 동시에 가지고 작업해야 함
- 작업이 끝나야만 자원을 내어놓는다

<img width="719" alt="Image" src="https://github.com/user-attachments/assets/e71acd27-e891-47b6-94d8-9b49034f985f" />

- 💊 자원`S`를 얻어야만 `Q`를 얻을 수 있도록 **자원 얻는 순서**를 정한다.
- 그러면 위 그림처럼 한 자원은 `S`를 가지고, 다른 자원은 `Q`를 가져서
- 서로 자원을 `release`하길 기다리는 문제 발생하지 않을 것!
- 따라서 semaphore을 구현할 때는 여러 가지를 고려해서 구현할 필요가 있다

## ✅ Classical Problems of Synchronization

#### ☑️ Bounded-Buffer Problem(Producer-Consumer Problem)

> producer, consumer프로세스가
> 공유 buffer를 동시접근 하는 상황에서 어떻게 문제를 해결하는가
> bounded buffer = 크기가 유한하다
> synchronization variable(semaphore)이용해 문제 해결

- 프로세스 종류: `Producer` 프로세스 & `Consumer` 프로세스
- ✔️ `Producer` **프로세스: 데이터 생성**
  - 데이터를 생성하여 `buffer`에 집어넣는다.
  - 내용이 비어있는 `buffer`이 자원
  - 만약 `empty buffer`이 없으면 `Consumer` 프로세스가 데이터를 빼어가기까지 기다려야 한다
  - ➡️ 내용이 비어있는 `buffer`, 내용이 들어있는 `buffer`의 개수를 세야 함

<br>

- ✔️ `Consumer` **프로세스: 데이터를 꺼내가기**
  - 내용이 들어있는 `buffer`이 자원
  - 만약 내용이 들어있는 `buffer`이 없으면 `Producer` 프로세스가 데이터 만들어 넣어주기까지 기다려야 한다.
  - ➡️ 내용이 비어있는 `buffer`, 내용이 들어있는 `buffer`의 개수를 세야 함

<img width="484" alt="Image" src="https://github.com/user-attachments/assets/b3288a9f-9512-4cc1-8034-dab11a53d983" />

- 노란색 원: `Producer` 프로세스가 데이터를 넣은 `buffer`
- 비어있는 원: `Producer` 프로세스가 데이터를 넣음
- ⚠️ `Producer` 프로세스가 데이터가 데이터 넣으려고 하는데 `CPU`뺴앗기면?
- 😱 `CPU`뺴앗긴 사이에 또 다른 `Producer` 프로세스가 와서 같은 원에 데이터 넣을 수도 있음!
- 💊 공유데이터에 `lock`을 건다
- 💊 그리고 `다음 노란 원`을 가리키도록 한다.
  <br>

- `Consumer` 프로세스 또한 데이터를 꺼내가기 전에 `lock`을 건다
  <br>

- 💊 binary semaphore: `lock`을 걸고, 풀기
- 💊 counting semaphore: 내용이 비어있는 `buffer`, 내용이 들어있는 `buffer`의 개수를 세기

<br>

- ✔️ **Shared data**

  - 공유 `buffer`
  - `buffer` 조작 변수
  - `empty/full buffer`의 시작 위치

- ✔️ **Synchronization variables**
  - mutual exclusion ➡️ binary semaphore(shared data의 mutual exclusion위해)
  - resource count ➡️ counting semaphore(남은 `full/empty buffer`의 수 표시)

<img width="434" alt="Image" src="https://github.com/user-attachments/assets/44cfa006-b8f3-4eab-861d-f00173b0b694" />

#### ☑️ Readers and Writers Problem

> `read`, `write`프로세스가 `DB`에 동시 접근하는 문제 <br>
> 다른 프로세스가 `write`중일 때는 DB에 접근하지 못하게 한다(배타적) <br>
> 반면 `read`는 동시에 해도 된다. <br>

- 한 프로세스가 `DB`에 `write`중일 때 다른 프로세스는 접근하면 안 됨
- `read`는 동시에 여러 프로세스가 해도 됨
- 💊 `writer`가 `DB`에 접근 허가를 얻지 못한 상태에서는 모든 대기중인 `reader`들은 `DB` 접근 허용
- 이미 `read`있는데 또 `reader`와도 허용
- 💊 `writer`는 대기 중인 `reader`가 하나도 없을 때 `DB` 접근 허용
- 💊 일단 `writer`가 `DB` 접근중이면 `reader`들은 접근 금지
- 💊 `writer`가 `DB`에서 빠져나가야 `reader` 접근 허용

- ✔️ **Shared data**

  - `DB`
  - `read count`: 현재 `DB`에 접근중인 `reader`수

- ✔️ **Synchronization variables**
  - mutex: 공유변수 `read count`를 접근하는 코드(CS)의 mutual exclusion을 위해 사용
  - `db`: `write`중일 때 `lock`을 걸게 도와주는 변수
    - `reader`가 오면 `read count`를 확인, 0보다 크면 접근 허용

<img width="476" alt="Image" src="https://github.com/user-attachments/assets/d1489392-756e-459a-a638-e5706dc41ea3" />

- `reader`가 오면 `read count`를 확인
- `read count == 1` 이면 내가 처음 `DB`접근했으니, `lock`을 걸어서 `writer`접근 제한
- `read count > 1` 이면 `reader`가 이미 있다는 것이니 `reader`는 접근
- `read count == 0` 이면 `reader`가 `DB`를 떠나는 것이니 `lock`을 풀고 `writer`접근 허용
  <br>

- 👎🏻 `writer`에 대한 starvation이 발생할 수 있다.
- `reader`이 실행중이면 모든 `reader`이 수행된 후 `writer`이 실행되므로
- 💊 `reader`이 실행될 수 있는 최대 시간 간격을 두고, 일정 시간 이후에는 `writer`에게 기회 주기

#### ☑️ Dining-Philisophers Problem

- 예를 들어 5명이 밥을 먹는데 `공유데이터가 젓가락 5개`
- 따라서 내가 밥을 먹으면 나의 왼쪽/오른쪽 철학자는 밥을 먹지 못한다.
- 철학자는 굶어죽으면 안된다. `Starvation`
- 만약 모든 철학자가 자기 왼쪽에 있는 젓가락을 잡으면 ➡️ `deadlock`

- 💊 5명 테이블에도 4명의 철학자만이 테이블에 동시에 앉을 수 있도록 한다.
- 💊 왼쪽/오른쪽 젓가락을 동시에 잡을 수 있을 때만 젓가락을 잡을 수 있도록 한다.
- 💊 자원 얻는 순서(비대칭): 짝수 철학자는 왼쪽, 홀수 철학자는 오른쪽 젓가락부터 일단 잡아야 다음 젓가락을 잡을 수 있도록 한다.

## 💡 Monitor

> synchronization 문제를 좀 더 쉽게 해결할 수는 없을까? <br>
> 동시 수행중인 프로세스 사이에서 `abstract data type`의 안전한 공유를 보장하기 위한 `high-level synchronization construct` <br>
> 프로그래밍 언어 레벨에서 제공하는 동기화 수단 <br>

- 모니터 내부에 공유 자원이 있음
- 이 공유 자원에 대한 접근은 `모니터 내부에 정의된 procedure`을 통해서만 가능
- `모니터 내부에 정의된 procedure`는 동시에 실행되지 않고, 동시 접근도 불가
  <br>

- Monitor가 **공유 데이터에 대한 동시접근을 책임**져준다.
  - 모니터 내 함수로만 공유데이터에 접근 가능
  - 모니터 내 실행되는 프로세스는 하나로 제한
  - 공유데이터에 대해 `lock`이 _필요 없음!_
  - `monitor`이 다 책임져주니까
- 🆚 semaphore는 단순 연산 `P`, `V`만 제공해주고 변수 설정만 해줬음, 프로그래머가 `lock`책임져야 함
  <br>

- 모니터 내에서는 **한번에 하나의** 프로세스만이 수행 가능
- 프로세스가 모니터 안에서 _기다릴 수 있도록_ 하기 위해 `condition variable`사용
- `condition x, y`
- `condition variable`은 `wait`, `signal` 연산에 의해서만 접근 가능
- `x.wait`을 `invoke`한 프로세스는 다른 프로세스가 `x.signal`을 `invoke`하기까지 `suspend`
- 자원이 없으면 프로세스를 기다리게/잠들게 한다.
- `x.signal`: 정확하게 하나의 `suspend`된 프로세스를 `resume`
- `suspend`된 프로세스가 없으면 아무 일도 일어나지 않음
  <br>

- 👍🏻 프로그래머가 동기화 제약 조건을 책임지고 명시적으로 코딩할 필요 없음 ❌
- 👍🏻 `lock` 같은거 할 필요 없음
- 👍🏻 코드가 훨씬 상식적이고, 비교적 단순(자원이 없으몊 프로세스 잠들게 하기)
- 👎🏻 `monitor`을 지원하는 언어에서만 사용 가능
- 👎🏻 컴파일러가 OS를 이해하고 있어야 한다. (`CS`접근 위한 코드 생성)

### ☑️ Monitor 구조

- ✔️ **Entry queue (진입큐)**
  - 모니터 내의 procedure 수만큼 존재
- ✔️ **Mutual exclusion**
  - 모니터 내에는 항상 하나의 프로세스만 진입 가능
- ✔️ **Information hiding (정보은폐)**
  - 공유 데이터는 모니터 내의 프로세스만 접근가능
- ✔️ **Condition queue (조건큐)**
  - 모니터 내의 특정 이벤트를 기다리는 프로세스가 대기
  - wait() 명령으로 큐에 대기시킬 수 있음
  - signal() 명령으로 큐에서 뺄 수 있음
- ✔️ **Signaler queue (신호제공자 큐)**
  - 모니터에 항상 하나의 신호제공자 큐가 존재
  - signal() 명령을 실행한 프로세스가 임시 대기

### ☑️ Monitor 동기화 예제

<img width="419" alt="Image" src="https://github.com/user-attachments/assets/c7205550-ea9e-4fbb-8223-9250bf38f62c" />

- `R_Available` : 자원
- `requestR()` : 자원을 요청하는 함수
- `releaseR()` : 자원을 반납하는 함수
- `R_Free` : 자원을 할당받기 위해 대기하는 큐
- `signaler queue` : R_Free 큐에서 대기하는 프로세스들을 깨우는 큐

<img width="404" alt="Image" src="https://github.com/user-attachments/assets/8d6f2fbd-d060-4351-a105-2cd1fdb13007" />

- `procedure requestR()`
  - 자원이 있는지 확인한다.
  - 자원이 없으면 R_Free Condition 큐에서 기다리게 한다.
  - 자원이 자원을 받는다. (R_Available에 false 표시)
- `procedure releaseR()`
  - 자원을 반납한다. (R_Available에 true 표시)
  - R_Free Condition 큐에서 기다리는 프로세스를 깨운다.

<img width="419" alt="Image" src="https://github.com/user-attachments/assets/852794b9-65ab-413c-bfe8-b7895c136605" />

- R은 모니터밖에 있다.
- R_Available : 자원의 개수는 1개

<img width="423" alt="Image" src="https://github.com/user-attachments/assets/ccb3bb06-6e32-451a-aa50-e3fcc5bd5a92" />
- 최초에 프로세스 Pj가 requestR entry 큐에 들어온다.
- 현재 모니터에는 프로세스가 없으므로 모니터로 진입한다. (R_Available 표시)
- 프로세스 Pj가 모니터 안에서 자원 R을 요청한다.
- Pj는 모니터밖으로 나와 R을 사용한다.

<img width="417" alt="Image" src="https://github.com/user-attachments/assets/38c21d8b-70a4-4702-8ea5-4991c500521e" />

- requestR entry 큐에 프로세스 Pk가 도착한다.
- 모니터 내부에는 현재 아무도 없으므로(Pj는 모니터 외부에서 자원 R을 사용중)
- Pk는 모니터 내부로 진입하여 requestR() 프로시저를 실행한다.
- 하지만 자원이 없으므로 (R_Available은 0), Pk는 R_Free Condition 큐에 들어가 대기한다.
- Pm도 마찬가지로, 도착했는데, 자원이 없으므로 큐에서 대기한다.

<img width="419" alt="Image" src="https://github.com/user-attachments/assets/a5b48acb-5909-4b86-bfd5-2c81dbd7c6ab" />

- Pj는 자원 R을 다 사용하고 반납하러간다. (releaseR entry큐에 들어간다.)
- 현재 모니터 내부에는 프로세스가 없으므로
- Pj는 모니터 내부로 진입하여 releaseR을 수행한다.
- R_Available은 1이된다.
- 그리고 Pj는 signaler 큐로 들어가고, R_Free에 있는 프로세스를 하나 깨운다.
- 대기하던 Pk는 모니터 내부로 진입하고 requestR 프로시저를 실행한다.

<img width="419" alt="Image" src="https://github.com/user-attachments/assets/81a42d35-b0a4-430b-9ad7-e9656411ac9a" />

Pj가 모니터 안으로 돌아와서 남은 작업을 수행한다.
