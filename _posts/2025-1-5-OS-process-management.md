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
  - 운영체제가 프로세스 PCB도 만들고 해야 하기 떄문에 사용자 프로세스가 할 수는 없음
- 프로세스 생성은 `system call`을 통해 자식 프로세스 생성을 부탁
- 이 `system call`을 **fork() system call**이라고 부른다.

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

- 프로세스가 생성되면 독자적인 `address space`를 가지게 된다.
- 자식의 주소 공간은 부모의 `address space`를 그대로 복사한다.
- 따라서 자식의 주소 공간은 부모 `code`, `data`, `stack`를 모두 그대로 복사
- 따라서 `현재 부모가 어디까지를 수행했느냐`를 `stack`에 저장하고 있으니, 거기서부터 수행 시작
- 처음부터 수행 시작하는 것이 아님 ❌

#### ❓ 그럼 자식 프로세스에다가 부모와는 다른 프로그램을 돌리고 싶다면?

- 우선 `fork() 시스템콜`을 통해 부모를 복사해 새로운 프로세스를 생성하고
- 그러면 부모를 그대로 복사(`OS data except PID + binary`)
- `exec() 시스템 콜`을 통해 새로운 프로그램을 메모리에 올린다.

#### fork() system call 🆚 exec() system call

- `fork() system call`: 부모 프로세스를 복사해 자식 프로세스 생성
- `exec() system call`: 새로운 프로그램을 메모리에 올림

## ✅ Process Termination: exit(), abort()

- 1️⃣ 프로세스가 자발적으로 종료하는 경우
- 프로세스 종료를 위해 마지막 명령 수행 후 운영체제에게 이를 알림
- `exit system call`
  - 프로세스 생성은 `계층구조`이므로 자식이 부모보다 먼저 종료됨
  - 자식이 부모에게 `output data`를 보냄 via `wait`
  - 프로세스의 각종 자원들을 운영체제에게 반납

<br>

- 2️⃣ 프로세스가 강제로 종료돠는 경우
- 부모 프로세스가 자식 프로세스의 수행 종료
- `abort system call`
  - 자식이 할당 자원의 한계치를 넘어서거나
  - 자식에게 할당된 태스크가 더 이상 필요하지 않거나
  - 부모가 `exit`하는 경우
    - 원래 프로세스는 자식부터 종료되어야 하는데, 이 경우는 반대
    - 운영체제는 부모가 `exit`하면 자식이 더 이상 수행되도록 두지 않음
    - 단계적인 종료
    - 예를 들어 창을 띄워놓고 그 창 안에서 여러 작업을 하다가 창을 닫으면 ➡️ 그 안에서 돌아가던 작업들이 다 종료되는 것과 마찬가지

## 💡 fork()

> process is created by `fork() system call`

- create new adress space that is duplicate of the caller
- 생성 후 부모, 자식 중 누가 먼저 CPU를 잡을지는 모름!

- ❓ 그러면 자식 프로세스와 부모 프로세스를 어떻게 구분하나요?
- 부모 프로세스는 `fork system call`을 하고 나면, 자식의 `PID`를 `return값`으로 가지게 된다.
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

> process can execute a different program by the exec() system call

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

## 💡

## 💡

## ✅

## ✅

## ✅

## ✅

## ✅

CPU
