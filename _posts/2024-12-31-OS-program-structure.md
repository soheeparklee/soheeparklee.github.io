---
title: KOCW_Computer System Structure / Kernel / Interrupt / System Call
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

![코딩공책-95](https://github.com/user-attachments/assets/b6987b99-519f-4d1b-8c33-7b78cdcaddf9)

## ✅ 컴퓨터 시스템 구조

- 컴퓨터 부팅
- 운영체제는 메모리에 올라감
- 프로그램은 디스크에 저장되어 있다가 실행되면 메모리에 올라감

- I/O 장치에는 그들만의 CPU가 있는데, 이를 `디바이스 컨드롤러`라고 한다.

- 운영체제가 CPU를 쓸 떄는 문제가 없는데,
- 응용 프로그램이 CPU를 사용할 떄는 문제가 생길 수 있다. (예를 들어 CPU를 계속 잡아먹는 연산을 한다거나..)
- 그래서 운영체제가 CPU를 쓰는건지 🆚 응용 프로그램이 쓰는 건지 구별할 필요가 있다.

## 💡 Device Controller

- 각 하드웨어, I/O 디바이스에 붙어있는 각각의 작은 CPU
- 예시: 메모리에 붙어있는 메모리 컨트롤러, 디스크에 붙어있는 디스크 컨트롤러

- 실제 I/O작업은 Device Controller를 통해서 디바이스에 전달된다.
- 하드웨어
- 제어 정보를 위해 `control register`, `status register`을 가진다.
- `local buffer`을 가진다. (일종의 `data register`, 임시저장)
- `I/O`는 실제 `device`와 `local buffer` 사이에서 일어난다.
- Device Controller는 `I/O`가 끝나면 `interrupt`로 CPU에 그 사실을 알린다.

- Device Controller 안에서 사용되는 명령어는 `firmware`라고 불린다.

### 🆚 Device Driver

> CPU가 device에게 I/O를 부탁할 때 쓰이는 명령어

- CPU가 수행하는 코드

## 💡 Mode bit

> CPU를 운영체제가 쓰는 건지, 응용 프로그램이 쓰는건지 **구별하기** 위한 장치

- 사용자 프로그램의 잘못된 수행으로 다른 프로그램/운영체제에 피해가 갈 수 있다.
- 그래서 운영체제가 CPU를 쓰는건지 🆚 응용 프로그램이 쓰는 건지 구별을 해야 함
- 이 장치가 바로 `mode bit`

- `mode bit`을 통해 하드웨어적으로 두 가지 모드의 operation 지원

  - `0`: 모니터 모드(커널 모드, 시스템 모드), OS코드 실행
  - `1`: 사용자 모드, 사용자 프로그램 수행

- 보안을 해칠 수 있는 중요한 명령어는 `0, 모니터 모드`에서만 수행 가능
- `interrupt`, `exception` 발생 시 `0, 모니터 모드` 로 변경
- 사용자 프로그램에게 CPU를 넘길 때는 `1, 사용자 모드`로 modebit을 바꿔서 넘긴다.

<img width="420" alt="Screenshot 2025-01-01 at 12 14 44" src="https://github.com/user-attachments/assets/fae20ad1-2e6f-4552-ab96-17c865062465" />

## 💡 Program Counter

- `Program counter, PC`: CPU가 실행할 명령의 메모리 주소를 담고 있는 레지스터
- 기계어 실행 후에는 다음 위치를 가리키고 ➡️ 또 다음 위치

## 💡 Timer

> 운영체제와 협력해 특정 프로그램의 CPU 독점을 막기 위한 장치

- 어떤 응용 프로그램이 CPU를 오랫동안 독식하며 다른 프로그램에 피해👎🏻
- 이 때 운영체제가 CPU를 다시 돌려달라고 빼앗아와야 함
- 하지만 운영체제는 CPU를 주는 건 마음대로 할 수 있어도,
- 혼자 힘으로 빼앗아 올 수는 없음!
- 이 때 필요한 것이 `timer`

- `timer`는 일정시간마다 `interrupt`를 발생시킨다.
- 운영체제가 응용 프로그램에게 CPU를 넘길 때, `timer`를 맞추고 넘겨준다.
- 그래서 일정 시간이 지나면 운영체제에게 `interrupt`가 발생하게 됨 ➡️ 응용 프로그램의 CPU독점을 막음

## ✅ CPU 연산과 I/O연산

- **컴퓨터가 데이터를 읽는 과정**
- ➡️ 외부 장치(I/O)
- ➡️ `local buffer` 임시저장
- ➡️ 메모리
- ➡️ CPU

## ✅ 컴퓨터 시스템의 작동 개요

- CPU는 매 시점 메모리의 특정 주소에 존재하는 명령을 하나씩 읽어와 수행한다.
- 이 때 CPU가 수행해야 할 **메모리 주소를 담고 있는 레지스터**를 프로그램 카운터 `Program counter, PC`라고 한다.
- 즉, CPU는 매번 프로그램 카운터가 가리키는 메모리 위치의 명령을 처리한다.

## ✅ 사용자 프로그램이 사용하는 함수

> 사용자 정의 함수, 라이브러리 함수, 커널 함수

#### ☑️ **사용자 정의 함수**

> 프로그래머가 직접 작성한 함수

- 자신의 프로그램에서 정의한 함수

#### ☑️ **라이브러리 함수**

> 프로그래머가 직접 작성하지는 않았지만, 누군가 작성해 놓은 함수를 호출만 해서 사용하는 것

- 자신의 프로그램에서 정의하지는 않았지만, 내 프로그램에 정의된 함수
- `사용자 정의 함수`와 `라이브러리 함수`는 모두 프로그램의 코드 영역에 기계어 명령 형태로 존재한다.
- 프로그램이 실행될 때마다 `프로세스의 주소 공간`에 포함됨
- 함수 호출 시에도 자신의 `주소 공간`에 있는 `스택` 사용

#### ☑️ **커널 함수**

> 운영체제의 커널 코드에 정의된 함수 <br>
> 커널 함수를 호출하는 것이 바로 `system call`

- CPU제어권을 운영체제에게 넘겨야 한다.
- 커널함수는 `운영체제 커널의 주소 공간`에 `코드` 정의

- ✔️ 커널함수의 두 종류

  - 시스템 콜 함수
  - 인터럽트 처리 함수

- 예를 들어, `삼각 함수 sin()`은 라이브러리 함수
- `printf()` 그 자체로는 라이브러리 함수지만, 궁극적으로 특권 명령인 입출력을 수반하므로 `printf()` 내에서 커널 함수를 호출하는 시스템 콜을 동반한다.
- 일반적인 함수 호출 🆚 시스템 콜
  - 일반적인 함수 호출: 사용자 프로그램 내에 존재하는 코드 실행
  - **시스템 콜**: 운영체제라는 별개의 프로그램에 CPU를 넘겨서 실행
    - CPU를 운영체제에게 넘기기 위해서 인터럽트와 통일한 메커니즘, 즉 CPU의 인터럽트 라인을 세팅하는 방법을 사용한다.

## ✅ Virtual Memory 구성 요소

- 컴퓨터 프로그램 내부는 **함수**들로 구성되어 있다.
- 그래서 하나의 함수가 실행되는 와중에 다른 함수를 호출하고, 호출된 함수의 수행이 끝나면 다시 원래 수행하던 함수로 돌아가 프로그램을 계속 실행한다.
- 한편 프로그램이 실행되기 위해서는 `해당 명령을 담은 프로그램의 주소 영역`이 메모리 위에 올라가 있어야 한다.

- `해당 명령을 담은 프로그램의 주소 영역/공간`은 `코드 code`, `데이터 data`, `스택stack`으로 구분된다.

## ✅ 운영체제 kernel구조

- 운영체제도 하나의 프로그램이므로, 운영체제 커널 역시 `주소 공간(코드, 데이터, 스택)`을 가진다.
- 운영체제의 목적은 `1. 아랫단의 하드웨어 자원 효율적 관리`, `2. 윗단의 응용프로그램 및 사용자에게 편리한 서비스 제공`

- ✔️ **kernel** `code`:
  - CPU, 메모리 등 자원 관리 부분 ➕ 사용자에게 편한 인터페이스를 제공하기 위한 부분
  - 또 시스템 콜, 인터럽트 처리 코드
  - 자원 관리 CPU scheduling, memory management위한 코드

<br>

- ✔️ **kernel** `data`:
  - 각 프로세스의 상태, CPU 사용 정보, 메모리 사용정보 등을 유지하기 위한 자료구조 `PCB`를 두고 있다.
  - 하드웨어, 소프트웨어를 포함해 시스템 내 모든 자원을 관리하기 위한 자료구조를 가지고 있다.
  - `PCB`: Process Table and Control Block
  - data structure used by OS to store information about specific process
  - each process has its own PCB, includes details for the OS to manage, control process
  - 현재 프로세스가 10개 실행되고 있다 ➡️ `PCB`도 10개

<br>

- ✔️ **kernel** `stack`:
  - 함수 호출 시 복귀주소 저장
  - 현재 실행중인 프로세스마다 **별도의** 스택을 두어 관리한다.
  - 예를 들어 `프로그램 A`가 실행되다가 운영체제를 호출하면 `stack A`에 `프로그램 A`저장해놓는 식이다

<img width="529" alt="Screenshot 2025-01-04 at 13 01 57" src="https://github.com/user-attachments/assets/ef7c83c0-ccca-4c3c-bc90-3f2f5232ee2b" />

## ✅ 프로세스의 두 가지 실행 상태

- 프로세스 A가 CPU에서 실행되고 있음
- 1️⃣ 일반적인 함수 호출(자신의 주소 공간에 정의된 코드 실행) ➡️ **사용자 모드**
  - 사용자 정의함수, 라이브러리 함수 호출
  - 모드의 변경 없이 `사용자 모드`에서 실행 지속, `modebit 1`
- 2️⃣ 커널의 시스템 콜 함수 실행 ➡️ **커널 모드**
  - `커널모드`로 진입해 커널의 주소 공간에 정의된 함수 실행 `modebit 0`
- 따라서 프로세스 실행은 `사용자 모드`와 `커널모드`를 왔다갔다 하면서 실행

## ✅ 인터럽트

> `Device controller`는 `I/O장치`로부터 `local buffer`로 데이터를 읽어들인다. <br>
> 이 과정이 끝나면 `Device controller`는 CPU에게 "나 끝났어!" 보고하고, 이것이 바로 **인터럽트** <br>

> 인터럽트 당한 시점의 레지스터와 `program counter`를 저장하고, CPU제어를 인터럽트 처리 루틴에 넘긴다.

- CPU 옆에는 인터럽트를 확인할 수 있는 `인터럽트 라인`이 있다.
- 인터럽트가 발생되면, `인터럽트 라인`이 세팅된다.
- CPU는 `Program Counter PC`가 가리키고 있는 지점의 명령을 하나씩 수행하고 나서, 다음 명령을 수행하기 직전에 `인터럽트 라인`이 세팅되었는지 확인한다.
- 만약 인터럽트가 발생했으면(`timer`, `I/O장치`), CPU는 현재 수행하던 프로세스를 멈추고
- 운영체제 커널의 인터럽트 벡터에서 해당 인터럽트에 대한 인터럽트 처리 루틴을 찾느다.
- 운영체제의 인터럽트 처리루틴으로 이동, 인터럽트 처리를 수행한다.
- 인터럽트 처리를 마치고 나면 인터럽트 발생 직전 프로세스에게 CPU의 제어권이 다시 넘어간다.

#### ☑️ 인터럽트의 종류

- ✔️ **하드웨어 인터럽트(외부 인터럽트)**:

  - 하드웨어 디바이스 컨트롤러에서 작업이 끝났을 때(입출력) 인터럽트
  - `하드웨어 인터럽트`는 `하드웨어 device controller`이 `인터럽트 라인`을 세팅한다.
  - `timer`, 하드웨어에 의해 발생

  - 외부 신호 인터럽트: 타이머 인터럽트, 키보드로 인터럽트 키를 눌렀을 때, 외부 장치로부터 인터럽트 요청이 있는 경우
  - 입출력 인터럽트(I/O interrupt): 입출력장치가 데이터 전송 요구, 또는 끝났을 때, 또는 오류 발생 시
  - 전원 이상 인터럽트(power fail interrupt): 정전, 파워 이상 등
  - 기계 착오 인터럽트(machine check interrupt): CPU기능 오류

<br>
<br>

- ✔️ **소프트웨어(내부) 인터럽트** `Trap`:

  - 프로그램에서 자신의 권한 밖의 작업을 수행할 때 운영체제에게 시스템 콜로 인터럽트
  - `소프트웨어 인터럽트`는 소프트웨어가 직접 `인터럽트 라인`을 세팅한다.

  - exception: 프로그램이 오류를 범한 경우
    - `division by zero`, `overflow/underflow` 등 exception
  - system call: 프로그램이 커널 함수를 호출하는 경우
    - 프로그램 A가 권한 밖 일을 하려고 할 때, `modebit`을 `0`으로 설정 후 `system call`

---

- ❓ I/O를 하려면 어떤 인터럽트 종류가 필요한가?
- 하드웨어, 소프트웨어 인터럽트 모두 필요하다.
- 프로그램이 OS에게 `system call`로 인터럽트 요청을 한다. ➡️ 소프트웨어 인터럽트
- I/O장치가 I/O작업이 끝나면 CPU에게 인터럽트를 한다. ➡️ 하드웨어 인터럽트

---

- ❓ 인터럽트 처리 중에 또 다른 인터럽트가 발생하면 어떻게 될까?
- 원칙적으로 인터럽트 처리 중에는 다른 인터럽트가 발생하는걸 허용하지 않는다.
- 이는 **데이터 일관성 유지**를 위함이다.
  - 인터럽트를 처리하면서 커널에 정의된 데이터를 변경하고 있는데, 다른 인터럽트가 발생해 앞선 인터럽트에서 변경중인 데이터를 또 변경하면 의도하지 않은 데이터 값이 나올 수 있음!
- 하지만 예와가 존재한다. **더 높은 중요도를 가진 인터럽트가 발생하면**, 더 낮은 중요도를 가진 인터럽트를 처리하는 와중에 인터럽트 발생을 허용할 수 있다.

#### ☑️ 인터럽트 벡터

> 인터럽트와 인터럽트 처리에 대한 처리루틴 정보를 가지고 있는 일종의 테이블

- 인터럽트가 발생하는 경우는 여러 가지가 있고(하드웨어/소프트웨어/타이머 등)
- 각 경우마다 실행해야 하는 작업이 다르다.
- **해당 인터럽트의 처리 루틴 주소**를 **인터럽트 벡터**라고 부른다.
- 일종의 포인터
- 예시: ~이 경우에는 ~에 있는 주소로 가서 명령어를 살펴봐라

#### ☑️ 인터럽트 처리 루틴(Interrupt Service Routine)

- 인터럽트가 발생했을 떄 CPU가 수행해야 하는 명령어가 바로 `인터럽트 처리 루틴`
- 그 주소로 가서 정말 실행해야 하는 **명령어**
- 해당 인터럽트를 처리하는 커널 함수
- 예시: ~이 경우에는 ~명령어를 실행해라

- `인터럽트 처리 루틴`은 로컬버퍼에 있는 데이터를 메모리로 옮기고, CPU에서 실행할 수 있도록 준비시킨다.
- `인터럽트 처리 루틴`은 운영체제 커널에 포함되어 있다.

#### ☑️ 인터럽트 핸들링

- 인터럽트가 발생했을 때 대응 절차
- CPU는 명령어를 실행할 때 CPU의 내부 임시 기억 장치인 `register`에 저장하거나 읽으면서 한다.
- CPU가 명령 실행 도중 `interrupt`가 발생하면, 새로운 명령어를 실행해야 하므로 `register`에 저장된 기존 데이터를 백업해 둔다.
- 이 때 `PCB`라는 곳에 백업(`register`, 실행 중이던 메모리 주소, 하드웨어 등 저장)

<img width="474" alt="Screenshot 2025-01-02 at 13 49 57" src="https://github.com/user-attachments/assets/3aadcf8f-1aac-4bd7-a9cc-3feae20712af" />

## ✅ 시스템 콜

> 사용자 프로그램이 운영체제의 서비스를 받기 위해 커널 함수를 호출하는 것<br>
> 자신의 주소 공간을 거스르는 영역에 존재하는 함수를 호출하는 것

- 내 권한으로는 실행할 수 없는 명령을(`I/O입출력`)
- 운영체제에게 해달라고 요청
- 예를 들어, 사용자 프로그램 A가 실행되다가, 디스크에서 입출력이 필요함
- ➡️ 프로그램 A는 입출력 권한이 없음(입출력은 운영체제만 가능)
- ➡️ 운영체제에게 디스크 컨트롤러에 입출력 해달라고 부탁
- ➡️ 따라서 프로그램 A가 가지고 있던 CPU를 운영체제에게 넘긴다.
- ➡️ 프로그램 A가 시스템 콜을 해서 인터럽트를 건다.

- 자신의 프로그램에서 함수 호출 ❌
- 커널이라는 다른 프로그램의 주소 공간에 존재하는 함수 호출 ⭕️
- 일반적인 함수 호출: 자신의 스택에 복귀 주소 저장 후, 호출된 함수 위치로 점프
- 🆚 시스템 콜: 주소 공간 자체가 다른 곳으로 이동
- 따라서 프로그램 자신이 인터럽트 라인에 인터럽트 세팅하는 명령을 통해 이루어진다.

## ✅ 인터럽트, 시스템 콜 질문

1. 운영체제한테 CPU가 넘어가는 경우는 어떤 경우가 있나요?

- 모두 인터럽트 라인을 세팅하는 경우
- 하드웨어에서 인터럽트: I/O기기에서 작업을 완료해 CPU에게 완료했다고 알릴 떄 인터럽트
- 사용자 프로그램이 인터럽트: CPU에서 권한 밖의 함수를 호출할 때(예를 들어 I/O) 운영체제 커넬 모드 사용 위해 시스템 콜, 또는 exception이 발생했을 때
- timer에서 인터럽트 할 수도 있음.

2. 사용자 프로그램이 CPU를 빼앗기는 경우

- 사용자 프로그램은 계속 쓰고 싶지만, CPU 독점권을 막으려고 timer에서 타임아웃
- 사용자 프로그램이 I/O가 필요해 기다려야 하는 경우
