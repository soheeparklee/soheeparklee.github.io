---
title: Blocking/Non Blocking & Synchronous/Asychronous
categories: [Computer Science, Network]
tags: [] # TAG names should always be lowercase
---

![Screenshot 2024-07-27 at 10 12 34](https://github.com/user-attachments/assets/f39c0392-390b-4fdb-80c7-9525a5017073)

## ✅ Blocking/Non Blocking

> calling method hands control over to called method

> Blocking
>
> > calling process needs to wait for called process to complete before they can continue execution <br>
> > user can’t do anything else while waiting on a system call<br>
> > wait!<br>
> > called method will finish work then hand over control back to calling function<br> > > <br>

> Non Blocking<br>
>
> > does not wait<br>
> > calling process can continue execution while the called process is in progress<br>
> > called process returns immediately when it’s complete<br>
> > even if called function did not finish, hands over control to calling function<br>

## ✅ Synchronous/Asychronous

> 동시성
> <br>

> Synchronous <br>
>
> > process is blocked until the I/O operation is completed <br>
> > calling method **pays attention** to called method, how are you doing? <br> > > <br>

> Asynchronous <br>
>
> > performs an operation on some data or resource and returns immediately without waiting for a response from another system <br>
> > when user does not need constant interaction with application, but wants it done as soon as possible <br>
> > called method pay attention to called method itself <br>
> > callback to tell calling method how I am <br>
> > calling method **does not pay attention** to called method before there is callback <br>

✔️ **비동기처리, Asynchronous processing** <br>

프로그램이 여러 작업을 동시에 처리하도록 설계된 방식 <br>
작업이 독립적으로 실행 => 이전 작업 안 끝나도 다른 작업 시작 가능 <br>
병렬적으로 운영(Non-blocking) <br>
프로그램의 효율성⬆️ <br>

예를 들어, <br>
파일을 업로드하는데 동기 방식이면, 지금 파일이 업로드 완료된 후에야 다른 작업 가능(blocking, 작업 중단)<br>
비동기 방식이면 파일 업로드가 진행되는 동안에도 사용자가 애플리케이션의 다른 부분 사용 가능<br>

A synchronous process is a process that can be executed without interruption from start to finish. <br>
An asynchronous process is a process that the Workflow Engine cannot complete immediately because it contains activities that interrupt the flow. <br>

✔️ **구현 방법**
자바스크립트와 같은 프로그래밍 언어에서 콜백 함수, 프로미스(Promise), async/await와 같은 기능을 통해 구현 <br>

- DOM event handler <br>
- Timer function(setTimeout, setInterval) <br>
- Ajax <br>

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
