---
title: KOCW_Process Management
categories: [Computer Science, Computer Architecture/Operating System]
tags: [] # TAG names should always be lowercase
---

## ✅ Process Creation: fork(), exec()

> 부모 프로세스 `parent process`가 자식 프로세스 `children process`를 생성

- 자식 프로세스는 부모 프레세스의 복사본이다.
- 프로세스의 **트리(계층 구조)** 형성

- 프로세스 생성은 **운영체제**가 담당한다.
  - 운영체제가 프로세스 `PCB`도 만들고 해야 하기 떄문에 사용자 프로세스가 할 수는 없음
- 1️⃣번째로 프로세스를 생성할 때는 **운영체제**가 직접 생성한다.
- 2️⃣번째로 프로세스를 생성할 때는 이미 존재하는 프로세스를 복제하여 생성하게 된다.
- 이미 존재하는 프로세스: `부모 프로세스`, 복제된 프로세스: `자식 프로세스`
- 프로세스 생성은 `system call`을 통해 자식 프로세스 생성을 부탁
- 이 `system call`을 **fork() system call**이라고 부른다.

#### ❓ 왜 프로세스를 복제해서 생성할까?

- 프로세스를 새로 생성하고 새롭게 자원을 할당하는데 오랜 시간이 걸리기 때문이다.
- 따라서 이미 생성된 프로세스부터 자원을 물려받는 복제 형태로 생성

#### ☑️ 부모, 자식 프로세스와 자원

- 프로세스는 자원을 필요로 한다.
- 운영체제로부터 자원을 받는다
- 부모와 공유하기도 한다.
- 원래 프로세스끼리는 자원을 서로 가지기 위해 싸우는데,
- 부모, 자식 프로세스 간에는 공유하기도 한다.
- 🆚 thread 간에 하나의 프로세스 내에서 자원을 공유하는 거랑은 다름

#### ☑️ 부모, 자식 프로세스의 수행 execution

- 부모와 자식 프로세스는 서로 독립적으로,
- 원래는 서로 경쟁해야 하지만
- 서로 `wait(block)`되기를 기다리는 경우도 있다.

#### ☑️ 주소 공간 address space

- 자식 프로세스가 생성되면 독자적인 `address space`를 가지게 된다.
- 자식의 주소 공간은 부모의 `address space`를 그대로 **복제**한다.
- 프로세스 ID를 제외한 모든 정보(커널 정보, 주소 공간 정보)를 그대로 **복사**
- 따라서 자식의 주소 공간은 부모 `code`, `data`, `stack`를 모두 그대로 복사
- 따라서 `현재 부모가 어디까지를 수행했느냐`를 `stack`에 저장하고 있으니, 거기서부터 수행 시작
- 처음부터 수행 시작하는 것이 아님 ❌

#### ❓ 그럼 자식 프로세스에다가 부모와는 다른 프로그램을 돌리고 싶다면?

- 우선 `fork() 시스템콜`을 통해 부모를 복사해 새로운 프로세스를 생성하고
- 그러면 부모를 그대로 복사(`OS data except PID + binary`)
- 자식 프로세스가 다른 프로그램을 수행하기 위해서는 생성된 `address space`위에 새로운 프로그램 주소 공간을 덮어씌워 수행한다.
- `exec() 시스템 콜`을 통해 새로운 프로그램을 메모리에 올린다.

#### fork() system call 🆚 exec() system call

- `fork() system call`: 부모 프로세스를 **복사**해 자식 프로세스 생성
- `exec() system call`: 새로운 프로그램을 메모리에 올림

## 💡 fork()

> process is created by `fork() system call`
> create a child(copy) <br>

- create new adress space that is **duplicate** of the caller
- 생성 후 부모, 자식 중 누가 먼저 CPU를 잡을지는 모름!

#### ❓ 그러면 자식 프로세스와 부모 프로세스를 어떻게 구분하나요?

- 부모 프로세스는 `fork system call`을 하고 나면, 자식의 `PID`를 `return값`으로 가지게 된다.
- `fork 함수`는 부모 프로세스에게는 자식 프로세스의 `PID`를 반환
- 자식 프로세스에게는 0을 반환
- 따라서 부모 프로세스는 **return 값이 양수**
- 반면 자식 프로세스는 `fork의 결과값`를 **0**으로 가지게 된다.

```C
int main()
{
    int pid;
    pid = fork(); //이 순간 똑같은 프로세스 복제 생성
    if(pid == 0) printf("\n I am child process");
    else if(pid > 0) printf("\n I am parent process");
}
```

## 💡 exec()

> process can execute a different program by the `exec() system call` <br>
> overlay new image <br>

- replaces the memory image of the caller with a new program
- 새로운 프로그램으로 덮어씌우는 함수
- 새로운 프로그램의 이름을 따옴표 안에 적고, 전달할 argument 나열, 0포인터 보내기

```C
int main(){
    printf("\n hello");
    execlp("/bin/date", "bin/date", (char*) 0);
    printf("\n bye");
}

// hello는 출력됨
// execlp이 실행되므로 date라는 완전히 새로운 프로그램으로 덮어씌워짐
// 따라서 bye는 출력되지 않음
```

- 부모와 자식 프로세스 생성 후 자식 프로세스는 다른 일 시키기 예시 코드

```C
int main()
{
    int pid;
    pid = fork(); //이 순간 똑같은 프로세스 복제 생성
    // 자식은 새로운 프로세스로 덮어씌우기
    if(pid == 0) execlp("/bin/date", "bin/date", (char*) 0);
    //부모는 하던 프로세스 계속 하기
    else if(pid > 0) printf("\n 나는 부모, 하던 프로세스 계속하기");
}
```

## 💡 wait()

> parent process is `blocked` until the child process **is terminated** by the `wait() system call` <br>
> sleep until child is done <br>

- 자식을 `fork()`를 통해 만든 후,
- 부모가 자식 프로세스에게 `wait()`을 하게 되면
- 부모는 자식이 **종료될 때까지** `block`된다.
  - `block`: I/O작업처럼 오래 기다려야 하는 작업이 있을 때 CPU를 줘봤자 소용이 없으니 프로세스를 `sleep`시키는 프로세스 상태
- 자식 프로세스가 종료되면 부모 프로세스가 CPU를 얻을 수 있게 된다.

#### ❓ 왜 `wait()`을 통해 부모 프로세스를 `block`할까?

- `wait()`을 하지 않으면 부모, 자식 프로세스는 *경쟁 관계*가 된다.
- CPU를 먼저 얻으려고 경쟁
- 따라서 `wait()`을 통해 자식이 먼저 실행되고 ➡️ 부모 실행

## ✅ Process Termination: exit(), abort()

## 💡 exit()

> free all resource, notify parent process

- 프로세스가 **자발적으로** 종료하는 경우
- 프로세스 종료를 위해 마지막 명령 수행 후 운영체제에게 이를 알림
- 마지막 statement 수행 수 `exit()` 시스템 콜 통해 종료
- 프로그램에 명시적으로 적어주지 않아도 `main`함수가 리턴되는 위치에 `컴파일러`가 넣어줌

- 프로세스 생성은 `계층구조`이므로 자식이 부모보다 먼저 종료됨
- 자식이 부모에게 `output data`를 보냄 via `wait`
- 프로세스의 각종 자원들을 운영체제에게 반납

## 💡 abort()

- 프로세스가 **강제로** 종료돠는 경우
- 부모 프로세스가 자식 프로세스의 수행을 강제로 종료

- ❓ 언제 `abort system call`

  - 자식이 할당 자원의 한계치를 넘어서거나
  - 자식에게 할당된 태스크가 더 이상 필요하지 않거나
  - 키보드로 `kill`, `break`하는 경우
  - 부모가 `exit`하는 경우

- 부모가 `exit`하는 경우
  - 원래 프로세스는 자식부터 종료되어야 하는데, 이 경우는 반대
  - 운영체제는 부모가 `exit`하면 자식이 더 이상 수행되도록 두지 않음
  - 단계적인 종료
  - 예를 들어 창을 띄워놓고 그 창 안에서 여러 작업을 하다가 창을 닫으면 ➡️ 그 안에서 돌아가던 작업들이 다 종료되는 것과 마찬가지

## ✅ 프로세스 간 협력

- ✔️ **독립적 프로세스 Independent process**
- 원칙적으로 프로세스는 독립적, 서로 더 자원을 얻기 위해 경쟁하는 관계
- 프로세스는 각자의 주소 공간을 가지고 수행
- 프로세스는 다른 프로세스의 메모리 공간을 볼 수 없음
- 각자 자신의 `VM`안의 `address space`만 접근할 수 있음!
- 따라서 다른 프로세스 수행에 영향을 미칠 수 없음

- ✔️ **Cooperating process**
- 하지만 협력 메커니즘을 통해 다른 프로세스 수행에 영향을 미칠 수도 있음

- ✔️ **IPC**
- 프로세스 간 협력 메커니즘

## ✅ Inter Process Communication

> IPC: inter process communication <br>
> 프로세스 간 협력을 위해 <br>
> 운영체제게 제공하는 프로세스 간 통신, 동기화 메커니즘 <br>

- 원칙적으로는 하나의 프로세스가 다른 프로세스의 수행에 영향을 미칠 수 없다. ➡️ 독립적
- 하지만 독립적인 프로세스들이 협력할 떄 효율성이 증진될 수 있음
  - (부분적인 처리 결과, 정보 공유, 처리 속도 향상 등)
- 따라서 운영체제는 프로세스 간 `협력 메커니즘`을 제공해 하나의 프로세스가 다른 프로세스 수행에 영향을 미칠 수 있게 한다.
- 이 `협력 메커니즘`을 `IPC`라고 한다.

- `IPC`란 하나의 컴퓨터 안에서 실행중인 **서로 다른 프로세스 간 통신**
- 이러한 통신에서는 **공유 데이터에 대한 동기화**가 필수
- 따라서 `IPC`는 프로세스들 간 **통신**과 **동기화**를 위한 메커니즘

#### ☑️ message passing

> 메세지 전달하는 방식

- 메세지 전달은 `커널`이 담당
- `커널`에게 `system call`을 요청해 메세지 전달
- 메세지 통신을 하는 시스템은 `커널`이 `send()`와 `recieve()`라는 두 가지 연산 제공

  - `send`와 `recieve`를 통해 전달할 메세지를 `OS`에게 `system call`방식으로 요청해 전달
  - 통신을 원하는 두 프로세스는 `커뮤니케이션 링크`를 생성한 후, `send()`와 `recieve()`를 통해 메세지를 주고받는다.
  - 메세지 전달 방식은 직접 통신과 간접 통신이 있다.

- ✔️ **Direct Communication**
  - 직접 통신에서는 통신하려는 프로세스의 이름 _명시_
  - `send(p, message)`: `프로세스 p`에게 메세지 전송
  - `recieve(Q, message)`: `프로세스 Q`로부터 메세지 전달 받음

<br>

- ✔️ **Indirect Communication**
  - 간접 통신은 메세지를 `메일박스` 또는 `포트`로부터 전달받는다.
  - 각 `메일박스`는 `고유 ID`가 있으며 `메일박스`를 공유하는 프로세스끼리만 통신 가능
  - 따라서 간접 통신에서 사용되는 `커뮤니케이션 링크`는 여러 프로세스 간 `메일박스`를 공유하는 경우에만 생성
  - 하나의 링크가 여러 프로세스에게 할당될 수 있고, 각 프로세스의 쌍은 여러 링크 공유 가능
  - `send(A, message)`: `메일박스 A`에게 메세지 전송
  - `recieve(A, message)`: `메일박스 A`로부터 메세지 전달 받음

#### ☑️ shared memory

> 공유 메모리 방식, 주소 공간을 공유

- 공유 메모리 방식에서는 프로세스들이 `address space`의 일부를 공유
- 운영체제는 공유메모리를 사용하는 `system call`을 지원, 주소 공간을 공유할 수 있게 한다.
- 👍🏻 프로세스 간의 통신이 수월해짐
- 👎🏻 데이터 일관성 문제, 동기화 문제
  - 이에 관해서는 커널이 책임지지 않음
  - 프로세스끼리 동기화 문제를 책임져야 한다.

## ✅

## ✅

## ✅

## ✅

CPU
