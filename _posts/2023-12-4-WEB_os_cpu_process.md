---
title: Operating System/ thread/ CPU process
categories: [Computer Science, Operating System]
tags: [backend] # TAG names should always be lowercase
---

## 👿 컴퓨터의 고질적인 문제

1. 저장공간 문제

- 언제: RAM, DISK 용량 부족
- 문제: 성능 저하, 데이터 유실

2. 오버 클락

- 언제: CPU, RAM 과다 사용(여러개의 무거운 프로그램을 한 번에 돌리면)
- 문제: 수명 단축, 시스템 충돌

3. 오버 히팅

- 언제: CPU, RAM
- 문제: CPU에 열을 발생시킴, 쿨링장치 필요

## ✅ Operating System

```
//OS 기본
             -------------------  유저 🙂  -------------------
                   /                                \
        💿 System Software                        💿  Application Software
(실제 내장된 프로그램, 디스크 관리)               (내가 설치한 프로그램, 크롬, 워드, 게임...)
                                   |
                          🏃🏻‍♂️ Operating System
                                   |
                   💾  HardWare(CPU, RAM, Input, Output)
```

### ☑️ Functions of operating system

#### ✔️ 시스템 자원관리

어떤 프로그램을 돌릴 때 CPU의 코어 몇 개 쓸지, RAM은 몇 기가 쓸지 알아서 결정해 줌  
없다면 내가 ppt킬 떄 CPU는 2코어 할당, RAM은 4GB써...이렇게 일일히 통제해야 함.  
우리가 의식하지 않고도 컴퓨터의 하드웨어 알아서 관리함.

#### ✔️ 응용 프로그램 관리

어떤 프로그램을 클릭해 실행할 때 실행 부스터 통제  
새로운 앱을 깔았을 때 위치 정보를 허용할지/안 할지 권한 통제  
만약 없다면, 새로 깐 앱이 우리의 권한을 침범할 수 있음!

#### ✔️ 커뮤니케이션 지원 GIU

아이콘, 마우스를 클릭했을 떄 그 안에서 일어나는 일들 지원  
그래서 유저는 단순히 클릭했을 뿐이지만 그 뒷단 세세한 내용들 실행하는 OS  
유저에게는 편리하고 보기좋은 기능 Graphic User Interface

## ✅ Program? Process? Processor?

### ✔️ Program

프로그램이란, 명령으로 이루어진 총체 <br>
평소 프로그램은 정적으로 죽은 듯 디스크에서 지내다가 <br>
우리가 사용하려고 클릭하면 RAM에 업로드. 실행 준비 <br>
우리가 타자를 치면 CPU가 계산을 하며 실행 <br>

### ✔️ Process

**프로그램이** **RAM**에 올라오게 되면 **프로세스** <br>
실행되고 있는 프로그램

### ✔️ Processor?

프로세서: CPU

### Program 생성

<img width="668" alt="스크린샷 2023-12-04 오후 11 18 39" src="https://github.com/soheeparklee/personal_project_musicApp/assets/97790983/924fcf83-ef63-4035-92b6-05f2c53a700e">
- 준비: 프로세서 할당을 기다리는 상태
- 디스패치: 실제로 CPU랑 상호작용을 하며 돌아가고 있는 상태, 
- 실행: CPU를 점유하며 명령어 실행
- 종료: 
- 대기: 이벤트, 오류가 났을 때
     여기서 해결이 되면 다시 실행, 만약 해결이 안 되어 꺼버리면 종료

#### 💡 dispatch

When the CPU becomes available (either because the current process has finished its execution or due to a time-sharing mechanism), the operating system's scheduler selects a process from the ready queue to be dispatched or assigned to the CPU.  
Dispatching is a crucial aspect of multitasking operating systems, where multiple processes share the CPU in a time-sliced manner. The goal is to efficiently utilize the CPU and provide the illusion of concurrent execution to users and applications.

## ✅ thread

프로세스 내 **동시에 진행되는 작업 갈래**  
하나의 프로세스는 최소 1개 이상의 스레드를 가진다. (main 스레드)  
<br>
JAVA의 `public static void main`이 바로 main thread  
<br>
초기에는 프로세스가 가벼워서 따로 스레드가 없어도 프로세스가 직접 CPU랑 상호작용하며 실행되었는데,  
이제는 프로세스가 너무 무겁고 복잡해져서  
프로세스를 잘개 조개서 관리 => 스레드  
<br>

### single threaded process

- 프로세스는 1개, 바로 main 스레드
- 팔이 2개

### multi threaded process

- main 스레드 + child thread
- 팔이 4개! 효율이 더 좋다.

## ✅ CPU의 process 처리 방법

🤔 요리사가 요리 여러가지 하는 상황을 가정해 보자. <br>
<br>

- CPU가 일을 못한다는 것: **순차적 프로그램** 여러 프로그램을 한꺼번에 실행하려고 하는데, 첫 번쨰 프로그램이 끝날 때까지 나머지는 기다려야...느리고 한꺼번에 여러개를 하려면 속터짐!! <br>
- CPU가 일을 효율적으로 한다는 것: **병행 처리** 여러 프로그램의 과정을 돌며 조금씩 처리, 이것 하다가 조금 짬내서 다른 것도 하고~ <br>

### 👍🏻 병행 처리 concurrency

**Context Switching:** 여러 가지 context를 조금 조금씩 수행한다. <br>
CPU가 여러 가지 일을 조금조금씩 처리 ➡️ 보는 사람 입장에서는 동시에 여러 일을 처리한다고 생각 <br>
프로그램들이 "준비" 상태였다가 CPU을 점유해 "실행" 0.1초 동안 한 후 다음 프로그램에게 CPU주고... <br>
크롬 0.1초 열고, 그 다음 게임 0.5초 실행, 그 다음 음악 앱 0.1초 실행...이런식으로 반복해 비슷한 시간대에 크롬도 열고, 음악앱도 열고 게임도 실행하고. <br>

### 👍🏻 병렬 처리 Parallelism

돈을 더 써서 요리사를 더 많이 고용 ➡️ CPU 코어가 여러개 ➡️ multicore <br>
각 코어가 역할을 하나씩 맡아서 담당. <br>

### 💡 스레드를 이용한 멀티 프로세싱 + 비 순차적 방식

병렬 처리 좋은데, 근데 일 끝내고 쉬고 있는 코어는요? 비효율적이지 않나요? <br>
하나의 코어가 다른 일하는 코어보다 일이 먼저 끝나면, 일하는 코어의 스레드를 가져와서 실행. <br>
크롬 앱 여는 코어 일 끝나면, 윈도우 업데이트 하는 코어의 스레드 가져와서 같이 도와줌. <br>
코어가 스레드를 나누어 가지고, 코어가 적당히 **병행 처리**와 **병렬 처리** 모두 하면서 **스레드** 단위로 일한다. <br>

## ✅ Shell, Terminal

terminal을 통해 shell을 열어 실행시킨다. <br>

## ✅ process 관련 linux 명령어

프로세스들은 커널에 의해 **구조화 된 형태**로 유지되기 위해 **PID**라는 프로세스 ID정보를 가지고 있다. <br>
`ps` 시스템에서 실행 중인 프로세스 출력 <br>
`ps aux` 프로세스 상태를 보기 위해서 <br>

<img width="588" alt="스크린샷 2023-12-04 오후 8 26 57" src="https://github.com/soheeparklee/personal_project_musicApp/assets/97790983/cc80275d-66b5-4215-9007-b7b2e5b0f58e">

`while true; do echo "hello; sleep3; done` 직접 shell 명령어 실행하기 <br>
<br>
`CTRL C` 프로세스 종료 <br>
`CTRL Z` 프로세스 일시 정지 <br>
`fg %1` 프로세스 다시 실행(여기서 1은 프로세스 넘버) <br>
<br>
`jobs` 백그라운드 프로세스 리스트를 모두 출력해준다. 한마디로, 내가 내린 명령어 출력해 줌. <br>

## ✅ terminal 명령어

`pwd` 나 지금 어디 있어? 내 위치 말해줘 <br>
`cd` 나 이동할래 <br>
`cd cd /Users/sohmac/Documents` Documents 로 이동할래 <br>
`ls` 이 폴더 안에 있는 파일 다 말해봐 <br>
`javac HelloWorld.java` HelloWorld.java 컴파일 해 줘, 그 결과 HelloWorld.class 만들어진다. <br>
`java HelloWorld` HelloWorld.class을 실행해줘. <br>
<br>
<img width="546" alt="스크린샷 2023-12-04 오후 9 20 24" src="https://github.com/soheeparklee/personal_project_musicApp/assets/97790983/3c3d0770-1729-402d-8c20-fe8de8b0a649">
