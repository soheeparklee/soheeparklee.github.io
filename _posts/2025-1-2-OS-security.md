---
title: KOCW_Memory / Security
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ 저장장치의 구조

<img width="449" alt="Screenshot 2024-12-31 at 16 50 55" src="https://github.com/user-attachments/assets/7c8d675f-ec2b-4e6f-bc2c-5baf38814ddf" />

- ✔️ **주기억장치**
- volatile, primary(CPU executable), fast, expensive, small capacity
- register: CPU내부에 존재
- cache memory:
- main memory:

---

- ✔️ **보조기억장치**
- nonvolatile, secondary(CPU NOT executable), slower, cheaper, bigger capacity
- CPU에서 직접 실행 불가, primary에 올려놓고 실행해야 함
- 목적 1️⃣: 전원이 나가도 유지할 정보를 파일 형태로 보조기억장치에 저장
- 목적 2️⃣: 메모리는 한정되어 있으므로, 메모리 공간이 부족한 경우 필요한 부분만 메모리에 올려놓고, 아닌 부분은 `swap`에 올리기
- 디스크에 내려 놓는 일을 `swap out`이라고 한다.
- magnetic disk:
- optical disk:
- magnetic tape:

## ✅ Hardware Security

- 우리가 사용하는 운영체제는 여러 프로그램이 동시에 실행되는 `multi programming`환경
- 따라서 각 프로그램의 완전한 실행/ 프로그램간 충돌을 막기위해 `하드웨어 보안`이 필요
- ⚠️ 모든 사용자 프로그램이 디스크 파일에 자유롭게 접근할 수 있다면 보안상 문제가 발생할 수 있음
- 자신의 소유가 아닌 파일에도 접근할 수 있으므로
- 💊 `하드웨어 보안`을 위해 커널모드, 사용자 모드 필요

- ✔️ **커널 모드**
- CPU가 제어권을 가지고 운영체제 코드를 실행하는 모드
- 모든 종류의 명령을 다 실행할 수 있음
- 중요한 정보에 접근해 위험한 상황을 초래할 수 있는 연산은 `kernel mode`에서만 실행 가능
- 시스템에 중요한 영향을 미치는 연산은 `kernel mode`에서만 가능
- 모든 `I/O`는 특권명령으로, 커널모드에서만 실행 가능하다.
- `modebit 0`
- 👍🏻 보안 유지

- ✔️ **사용자 모드**
- 일반적인 연산, 사용자 프로그램
- 제한적인 명령만 수행 가능
- `modebit 1`

## 💡 System Call, Interrupt, Kernel mode

- 사용자 프로그램 실행 중 하드웨어 접근 등 보안이 필요한 중요한 명령을 실행해야 함
- 사용자 프로그램이 `System call`을 통해 운영체제가 대신해 줄 것을 요청 ➡️ `Interrupt`
- CPU제어권은 운영체제로 넘어감
- 사용자 프로그램의 `modebit`은 `0`으로 변경
- 이제 `kernel mode`에서 모든 종류의 명령 실행 가능
- 끝나면 `modebit`을 `1`로 변경하여 다시 사용자 프로그램에게 CPU넘겨주기

## ✅ Memory Security

- 여러 프로그램이 메모리에 동시에 올라가서 실행되기 때문에,
- `하나의 사용자 프로그램`이 `다른 사용자 프로그램`, `운영체제 메모리 영역`을 침범할 위험이 있음

- 💊 2개의 레지스터를 사용해 프로그램이 접근하려는 메모리 부분이 합법적인지 확인할 수 있다.
- ✔️ **Base register, 기준 레지스터**: 프로그램이 합법적으로 접근할 수 있는 가장 적은 주소 보관
- ✔️ **Limit register, 한계 레지스터**: 프로그램이 접근할 수 있는 메모리의 범위
- 사용자 프로그램은 `base register`부터 `+ limit register`값 사이의 주소 영역에만 접근 가능
- 접근하려는 주소가 이 범위 사이에 없으면 `exception`발생 ➡️ `interrupt` 발생
- CPU제어권이 운영체제에게 넘어감
- 운영체제는 해당 프로그램을 `block`
- `base register`, `limit register`값을 세팅하는 건 특권 명령으로, `kernel mode`에서만 이루어질 수 있다.

## ✅ CPU Security

- CPU가 하나의 프로그램에 의해 독점되는 것을 막기위해 💊 `timer`사용
- `timer`는 정해진 시간이 지나면 `interrupt`발생시킴
- 운영체제가 일정 시간 후에는 CPU의 제어권을 획득할 수 있도록 한다.
- 따라서 운영체제가 특정 프로그램으로부터 CPU를 뺏을 수 있게 한다.

## ✅ System Call and I/O

- I/O명령은 모두 특권명령
- `사용자 프로그램`이 실행할 수 없다.
- 따라서 `사용자 프로그램`은 운영체제에게 `system call`을 통해 I/O를 요청해야 한다.
- `system call`은 일종의 소프트웨어 `interrupt`
