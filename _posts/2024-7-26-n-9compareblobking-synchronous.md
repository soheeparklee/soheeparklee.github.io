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

## ✅ Situations

went to order sandwich

- Blocking/Synchronous

```T
customer: one sandwich please
manager: wait one second
---- make sandwich ----
customer: curious about sandwich, pays attention, but cannot ask
```

- Blocking/Asynchronous

```T
customer: one sandwich please
manager: wait one second
---- make sandwich ----
customer: does not pay attention to manager, just wait
```

- NonBlocking/Synchronous

```T
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

```T
customer: one sandwich please
manager: wait one second
---- make sandwich ----
customer: work on his stuff, not interested in making sandwich
```
