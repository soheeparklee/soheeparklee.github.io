---
title: Blocking/Non Blocking & Synchronous/Asychronous
categories: [Computer Science, Network]
tags: [] # TAG names should always be lowercase
---

## ✅ Blocking/Non Blocking

> ⭐️ control <br>

- calling method **hands control over** to _called_ method
- **제어권을** 넘겨주는가? <br>

**Blocking** <br>

- 제어권을 넘겨준다.
- calling process needs to wait for called process to complete before they can continue execution
- user can’t do anything else while waiting on a system call
- wait!
- called method will finish work then hand over control back to calling function

<br>

**Non Blocking** <br>

- 제어권을 넘겨주지 **않는다**.
- does not wait
- calling process can continue execution while the called process is in progress
- called process returns immediately when it’s complete
- even if called function did not finish, hands over control to calling function

## ✅ Synchronous/Asychronous

> ⭐️ wait, need return value of the called function <br>
> 요청을 보내고 실행이 끝나기를 기다리는가/기다리지 않는가 <br>
> = calling method needs the return value of called method <br>
> = calling method has smth to do with the value of called method <br>
> = pay attention to the other method <br>

**Synchronous** <br>

- process is **blocked** until the I/O operation is completed
- calling method **pays attention** to called method, how are you doing?
- 👍🏻 good for tasks with order
- 👎🏻 less efficient since several request cannot be handled at the same time
- Example: call center employee can only pick up one calls at one time

<br>

**Asynchronous** <br>

- performs an operation on some data or resource and returns immediately **without waiting** for a response from another system
- when user does not need constant interaction with application, but wants it done as soon as possible
- called method pay attention to called method itself
- callback to tell calling method how I am
- calling method **does not pay attention** to called method before there is callback
- 👍🏻 efficient as does not have to wait for other task to finish
- 👎🏻 result might be not in order
- Example: email. We can send email without having to wait for reply

## ✔️ 비동기처리, Asynchronous processing

- 프로그램이 여러 작업을 동시에 처리하도록 설계된 방식
- 작업이 독립적으로 실행 => 이전 작업 안 끝나도 다른 작업 시작 가능
- 병렬적으로 운영(Non-blocking)
- 프로그램의 효율성⬆️

- 예를 들어,
- 파일을 업로드하는데 동기 방식이면, 지금 파일이 업로드 완료된 후에야 다른 작업 가능(blocking, 작업 중단)
- 비동기 방식이면 파일 업로드가 진행되는 동안에도 사용자가 애플리케이션의 다른 부분 사용 가능

- A synchronous process is a process that can be executed **without interruption** from start to finish.
- An asynchronous process is a process that the Workflow Engine cannot complete immediately because it contains activities that **interrupt** the flow.

✔️ **구현 방법** <br>
자바스크립트와 같은 프로그래밍 언어에서 콜백 함수, 프로미스(Promise), async/await와 같은 기능을 통해 구현 <br>

- DOM event handler
- Timer function(setTimeout, setInterval)
- Ajax

## ✅ Blocking, Synchronous used together

![Screenshot 2024-07-27 at 10 12 34](https://github.com/user-attachments/assets/f39c0392-390b-4fdb-80c7-9525a5017073)

- Blocking/Synchronous
  제어권 넘기고 끝날때까지 기다림(리턴값 필요함) <br>
  `A함수`는 `B함수`의 리턴 값을 필요로 한다. (Synchronous) <br>
  따라서 `A함수`는 `B함수`에게 제어권을 넘긴다. (Blocking) <br>
  그리고 `B함수`가 끝날때까지 기다린다. (Synchronous) <br>

- Blocking/Asynchronous
  제어권 넘기지만 기다리지 않음 <br>
  잘 볼 수 없는 경우이다. <br>
  `A함수`는 `B함수`의 리턴값을 필요로 하지 않는다. (Asynchronous) <br>
  그런데 `A함수`는 `B함수`에게 제어권을 넘겼다. (Blocking) <br>
  따라서 `A함수`는 자신과는 관련없는 `B함수`가 끝날때까지 기다려야 한다. <br>

- NonBlocking/Synchronous
  제어권 안 넘기고 기다림(리턴값 필요함) <br>
  `A함수`는 `B함수`의 리턴 값을 필요로 한다. (Synchronous) <br>
  하지만 제어권은 넘기지 않음 (Blocking) <br>
  그래서 `A함수`는 `B함수`한테 "너 끝났어? 끝났으면 리턴값좀"하고 계속 참견한다. (Synchronous) <br>

- NonBlocking/Asynchronous
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
