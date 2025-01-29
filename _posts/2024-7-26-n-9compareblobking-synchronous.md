---
title: Blocking/Non Blocking & Synchronous/Asychronous
categories: [Computer Science, Network]
tags: [] # TAG names should always be lowercase
---

## ✅ Blocking/Non Blocking

> ⭐️ control <br>

- calling method **hands control over** to _called_ method
- **제어권을** 넘겨주는가? <br>

#### ✔️ **Blocking** <br>

<img width="512" alt="Image" src="https://github.com/user-attachments/assets/2cc5f599-4d21-4df8-970a-e92603783370" />

- 제어권을 넘겨준다.
- calling process needs to **wait** for called process to complete before they can continue execution
- user can’t do anything else while waiting on a system call(I/O)
- called method will finish work then hand over control back to calling function

```
- A함수는 B함수를 호출하면서 제어권을 넘겨준다.
- B함수는 제어권을 넘겨 받고, 자신의 작업을 완료하기 전까지 제어권을 돌려주지 않는다.
- A함수는 B함수가 완료될 때까지 제어권을 돌려받지 못하므로 아무것도 못한다. 즉, 대기상태, block 상태가 된다.
- B함수가 완료되면 제어권을 A함수에게 리턴한다.
- 제어권을 다시 돌려받은 A함수는 그 다음 작업을 수행한다.
```

<br>

#### ✔️ **Non Blocking** <br>

- 제어권을 넘겨주지 **않는다**
- 호출된 함수의 작업 완료 여부에 상관없이 제어권을 호출한 함수한테 바로 리턴하여, 호출한 함수가 다른 작업을 할 수 있는 것
- **does not wait**
- calling process can **continue** execution while the called process is in progress
- called process returns immediately when it’s complete
- even if called function did not finish, **hands over control to calling function**

```
- A함수는 B함수를 호출하면서 제어권을 넘겨준다.
- B함수는 제어권을 넘겨받는다. 그리고 자신의 작업 완료 여부에 상관없이
- 제어권을 곧장 A함수에게 다시 넘겨준다.
- A함수는 제어권을 곧장 돌려받고, 다른 작업을 수행할 수 있다.(B함수의 완료와 상관없이)
- B함수의 작업이 완료되면, 그 결과를 A함수에게 통지한다.
```

<img width="545" alt="Image" src="https://github.com/user-attachments/assets/83e775b6-d5ae-4c02-ae45-57af2188b087" />

- 프로세스는 커널을 통해 `I/O` 작업(Read)
- 프로세스는 `I/O` 작업위해 `system call`
- 하지만 `I/O` 기기에서 데이터를 읽기전에 (No datagram ready)
- `EWOULDBLOCK`을 리턴 받는다. (`EWOULDBLOCK`: 아직 작업이 진행 중이란 뜻)
- 즉, `I/O` 작업이 완료되지 않았음에도 불구하고 제어권을 곧장 돌려받아
- 프로세스는 block되지 않는 것이다. (block되지 않는 동안 다른 작업 수행 가능.)

## ✅ Synchronous/Asychronous

<img width="557" alt="Image" src="https://github.com/user-attachments/assets/eebc513d-4252-40bf-a02e-336971fb66a5" />

#### ✔️ **Synchronous** <br>

> ⭐️ need return value of the called function <br>

- calling method needs the return value of called method <br>
- calling method has smth to do with the value of called method <br>
- pay attention to the other method <br>
- called function의 실행과 그 결과를 받을 때까지 기다린다
- 작업의 `요청`과 `결과`가 같은 시점에 일어남

```
- B 함수의 작업 완료는 A함수가 최종적으로 처리한다.
- 즉, A함수는 B함수를 호출하고 B함수의 수행 결과 및 종료를 처리한다.
    - B함수가 완료될 때까지 대기하다가 처리할 수도 있고(blocking-synchronization)
    - B함수가 완료될 때까지 다른 작업을 수행하면서, B작업의 완료 여부를 계속 체크하다가 처리할 수도 있다. B함수의 작업이 완료되었는지 체크하는 와중에 다른 작업 가능 (nonblocking-synchronization)
    - 어쨋든 B함수의 작업이 완료되어야지 A함수가 다른 작업 가능
```

```
Future ft = asyncFileChannel.read(~~~);

while(!ft.isDone()) {
    // isDone()은 asyncChannle.read() 작업이 완료되지 않았다면 false를 바로 리턴해준다.
    // isDone()은 물어보면 대답을 해줄 뿐 작업 완료를 스스로 신경쓰지 않고,
    // isDone()을 호출하는 쪽에서 계속 isDone()을 호출하면서 작업 완료를 신경쓴다.
    // asyncChannle.read()이 완료되지 않아도 여기에서 다른 작업 수행 가능
}

// 작업이 완료되면 작업 결과에 따른 다른 작업 처리
```

- 👍🏻 good for tasks with order
- 👎🏻 less efficient since several request cannot be handled at the same time
- Example: call center employee can only pick up one calls at one time

<br>

#### ✔️ **Asynchronous** <br>

<img width="558" alt="Image" src="https://github.com/user-attachments/assets/6d60591a-cbef-4b74-8982-0f212b2ed463" />

- called method pay attention to called method itself
- 호출된 함수의 수행 결과 및 종료를 호출된 함수가 처리
- performs an operation on some data or resource and returns immediately **without waiting** for a response from another system
- calling method **does not pay attention** to called method

```
- B함수의 작업 완료는 B함수가 직접 혼자 처리한다.
- 즉 B함수는 스스로 수행 결과 및 종료를 처리한다.
- B함수는 작업 수행을 완료하면 그 결과를 A함수에게 알릴 뿐이다.
- A함수는 B함수의 작업 완료를 신경쓰지 않기 때문에 B함수를 호출한후 다른 작업을 수행할 수 있다.
```

- callback to tell `calling method` how I am
- calling method **does not pay attention** to called method before there is callback

- 👍🏻 when user does not need constant interaction with application, but wants it done as soon as possible
- 👍🏻 efficient as does not have to wait for other task to finish
- 👎🏻 result might be not in order
- Example: email. We can send email without having to wait for reply

## ☑️ 비동기처리, Asynchronous processing

- 프로그램이 여러 작업을 동시에 처리하도록 설계된 방식
- 작업이 독립적으로 실행 => 이전 작업 안 끝나도 다른 작업 시작 가능
- 병렬적으로 운영(Non-blocking)
- 프로그램의 효율성⬆️

- 예를 들어,
- 파일을 업로드하는데 동기 방식이면, 지금 파일이 업로드 완료된 후에야 다른 작업 가능(blocking, 작업 중단)
- 비동기 방식이면 파일 업로드가 진행되는 동안에도 사용자가 애플리케이션의 다른 부분 사용 가능

- A synchronous process is a process that can be executed **without interruption** from start to finish.
- An asynchronous process is a process that the `Workflow Engine` cannot complete immediately because it contains activities that **interrupt** the flow.

✔️ **구현 방법** <br>
자바스크립트와 같은 프로그래밍 언어에서 콜백 함수, 프로미스(Promise), async/await와 같은 기능을 통해 구현 <br>

- DOM event handler
- Timer function(setTimeout, setInterval)
- Ajax

## ✅ Blocking, Synchronous used together

![Screenshot 2024-07-27 at 10 12 34](https://github.com/user-attachments/assets/f39c0392-390b-4fdb-80c7-9525a5017073)

- ✔️ **Synchronous/Blocking**
  제어권 넘기고 끝날때까지 기다림(리턴값 필요함) <br>
  `A함수`는 `B함수`의 리턴 값을 필요로 한다. (Synchronous) <br>
  따라서 `A함수`는 `B함수`에게 제어권을 넘긴다. (Blocking) <br>
  그리고 `B함수`가 끝날때까지 기다린다. (Synchronous) <br>

- ✔️ **Asynchronous/Blocking**
  제어권 넘기지만 기다리지 않음 <br>
  잘 볼 수 없는 경우이다. <br>
  `A함수`는 `B함수`의 리턴값을 필요로 하지 않는다. (Asynchronous) <br>
  그런데 `A함수`는 `B함수`에게 제어권을 넘겼다. (Blocking) <br>
  따라서 `A함수`는 자신과는 관련없는 `B함수`가 끝날때까지 기다려야 한다. <br>

- ✔️ **Synchronous/NonBlocking**
  제어권 안 넘기고 기다림(리턴값 필요함) <br>
  `A함수`는 `B함수`의 리턴 값을 필요로 한다. (Synchronous) <br>
  하지만 제어권은 넘기지 않음 (Blocking) <br>
  그래서 `A함수`는 `B함수`한테 "너 끝났어? 끝났으면 리턴값좀"하고 계속 참견한다. (Synchronous) <br>

- ✔️ **Asynchronous/NonBlocking**
  제어권 안 넘기고 안 기다림 <br>
  `A함수`는 `B함수`를 호출한다. <br>
  그러나 제어권은 넘겨주지 않았다. (NonBlocking) <br>
  `A함수`는 `B함수`를 기다리지 않고 자기 일을 한다. (Asynchronous) <br>

## ✅ Situations

went to order sandwich

- Blocking/Synchronous

```
customer: one sandwich please
manager: wait one second
---- make sandwich ----
customer: curious about sandwich, pays attention, but cannot ask
```

- Blocking/Asynchronous

```
customer: one sandwich please
manager: wait one second
---- make sandwich ----
customer: does not pay attention to manager, just wait
```

- NonBlocking/Synchronous

```
customer: one sandwich please
manager: wait one second
---- make sandwich ----
customer: how longer?
manager: not yet
customer: did you do this?
manager: not yet
customer: did you do that?
manager: not yet
```

- NonBlocking/Asynchronous

```
customer: one sandwich please
manager: wait one second
---- make sandwich ----
customer: work on his stuff, not interested in making sandwich
```
