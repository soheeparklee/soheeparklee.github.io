---
title: Interview_concurrency, multi thread, synchronized, volatile, visibility, atomic
categories: [JAVA, JAVA_Basics]
tags: [] # TAG names should always be lowercase
---

## ✅ concurrency과 parralelism의 차이

- concurrency: single core, multi thread, process takes turn
  - looks like several jobs are done at the same time, but actually one job is done at once
- parrellelism: multicore, several CPU

## ✅ Thread-Safe하다는 것이 무슨 의미인가요?

- shared data is accessed and modified safely by multiple threads without causing **inconsistent** or unexpected behavior.
- data consistency, integrity is maintained

## Data consistency 🆚 integrity

- Data consistency: data state is correct(I moved $100 from A to B, but the sum is consistent)
- Data integrity: data accuracy and validity(birthday `2033-13-99` violates data integrity)

## ✅ ACID of reliable database transactions

- A: Atomicity
- C: Consistency
- I: Isolation, transactions are independent
- D: Durability, once transaction is commited, changes are permanent, write DB to non-volatile storage(even if I restart database)

## ✅ Thread-Safe 구현방법

- 1️⃣ use `synchronized` keyword

```java
public class Counter {
    private int count = 0;

    public synchronized void increment() { //synchronized
        count++;
    }

    public synchronized int getCount() {
        return count;
    }
}
```

- 2️⃣ use `java.util.concurrent` Package
- `reentrantLock`: more granular lock
- `AtomicInteger, AtomicBoolean`: lock-free thread safe variable
- `ConcurrentHashMap`: thread safe collection
- concurrent: happening at the same time

```java
public class Counter {
    private AtomicInteger count = new AtomicInteger();

    public void increment() {
        count.incrementAndGet();
    }

    public int getCount() {
        return count.get();
    }
}
```

- 3️⃣ Thread safe collections
- `ArrayList` ➡️ `CopyOnWriteArrayList`
- `HashMap` ➡️ `ConcurrentHashMap`
- `Queue` ➡️ `ConcurrentLinkedQueue`

- 4️⃣ use Immutable
- immutable is thread safe as it cannot be changed after construction

```java
public final class User {
    private final String name;
    private final int age;

    public User(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

//only constructor, getter
//no setter
```

- 5️⃣ use Volatile
- volatile: varible that can be accessed by multiple thread, ensuring **visibility** of changes
- any write of this variable is immediately visible
- read of this varible is done **directly by main memory**, not from cache
- always read the latest, updated value
- ⭐️ **force memory sync**
- 👍🏻 lighter(no locking)
- 👎🏻 however, atomicity is not guaranteed
- use volatile for simple flags
- cannot use volatile for `count++`(no atomacity) ➡️ use `synchronization` or `AtomicInteger`

```java
public class FlagExample {
    private volatile boolean running = true;

    public void run() {
        while (running) {
            // do something
        }
    }

    public void stop() {
        running = false;
    }
}
```

- **Synchronization 🆚 Volatile**
- Synchronization: visibility, atomacity, but slower
- Volatile: visibility, lighter and fast, but no atomacity

## ✅ Methods to ensure Thread-Safety

- 1️⃣ **mutual exclusion(Locks):** `semaphore(semaphore variable)`, `mutex(0, 1)`
- 2️⃣ **atomic operations:** operation happens or not
- 3️⃣ **thread local storage**: thread has own copy of data, do not share
- 4️⃣ **reentrancy**: make program with no static, no global variables, no shared memory ➡️ only local variables(each thread saves variable on stack, has own copy)

## ✅ What problems can occur in parrallel programming? Mutli CPU?

- visibility problem
- atomacity problem

## ✅ Visibility and Atomicity Problems in Multithreading

- 💣 **Visibility problem**: one thread updates shared variable, but other threads don't see
- threads dont see the latest updated value
- because they are using outdated copy in cache
- 💊 use `volatile`: force memory sync, read and write directly to RAM, not cache
- 💊 use `synchronized`: makes code block execute as one unit, solves both visibility problem and atomacity problem

- 💣 **Atomicity Problem**: thread is interrupted during operation, operation is partially updated
- 💊 use `synchronized`: keyword `synchronized` ensures only one thread at a time executes the code
- 💊 use `AtomicInteger` at `concurrent` package

## ⚠️ Why does concurrency problems occur?

- each CPU has own cache, does not always read from RAM
- and parrallelism

## ✅ 자바의 동시성 이슈를 해결하는 방법을 아는만큼 설명해 주세요.

- 1️⃣ use `Synchronized`: only one thread can access code block
- 2️⃣ use `volatile`: save varible in main memory, other threads can always have updated latest value
- 3️⃣ use `Atomic class`, `concurrent package`: CAS(Compare and Swap) algorithm, guarantee synchronization

## ✅ volatile 키워드가 무엇인가요?

- force **memory sync** with main memory
- save variable on main memory, not cache
- guarantee threads read from main memory, reading **latest updated value**
- 👍🏻 solve visibility problem
- 👎🏻 however, does not solve the atomacity problem
- used for flag, simple variables
- cannot use for `count++`, more complex synchronization

## ✅ synchronized 키워드가 무엇인가요?

- ensure **atomacity** of code block with keyword `synchronized`
- ensure synchronization in multi threading environment
- 👍🏻 solve visibility problem, atomacity problem
- mutual lock: only one thread can enter `synchronized` block, method
- ensure visibility
- Reentrancy: thread can enter if it has lock

## ✅ synchronized의 문제점은 무엇이 있나요?

- 1️⃣ Performance Overhead: slow, need to aquire, release lock
- context swithcing, blocking
- 2️⃣ deadlock: two threads ask for same resource without giving up their resource, end up no thread getting resource
- 3️⃣ starvation, inefficient use of CPU: only one thread can access, rest have to wait
- 4️⃣ less flexible

## ✅ How is synchronized implemented in Java?

- use `object monitor lock(monitor)` which is built into JVM
- every object has monitor: speical structure used to control thread access
- JVM manages monitor
- monitor allows one thread at a time to run `synchronized` code

- `Monitor lock`: lock mechanism that control thread access in `synchronized`
- if thread wants to enter `synchronized` code, must aquire monitor lock first
- if lock is available, the thread will enter the `synchronized` block
- if another thread has already entered, has to wait

## ✅ What is Reentrancy?

- thread can **re-enter** a block of code it already has lock, without getting blocked or deadblocked
- this behavior is built into `synchronized` keyword
- Java has an `internal counter` to track reentrant locks

## ✅ atomic하다는 것이 무슨 의미인가요?

- operation will happen, or not happen at all
- if there is a interruption in operation, rollback

## ✅ atomic 타입이 무엇인가요

- atomic type is to ensure atomacity in multi thread environment even without lock
- `AtomicInteger`: ensure atomicity of variable
- `AtomicLong`, `AtomicBoolean`, `AtomicReference`, `AtomicStampedReference`

## ✅ CAS 알고리즘에 대해 설명해 주세요

- CAS: Compare and Swap
- atomic operation in multi thread programming to safely update shared variables **without using lock**
- used in atomic types like `AtomicInteger`

```
Only change the value if it has NOT changed since I last checked it
```

- compare: did it change?
- swap: if it did not change, change to new value
- if it changed, **someone else updated it, so don't change**, try later

- 👎🏻 ABA problem: if value was changed from A ➡️ B ➡️ A, thread will think value did not change
- 👎🏻 if repeated failiure, CPU usage: if fail to swap, keep try again later

## ✅ SynchronizedList와 CopyOnArrayList의 차이를 설명해 주세요

- `SynchronizedList`: only one thread can access list
- 👍🏻 multi thread safe, read and write synchronized
- 👎🏻 not very performant

- `CopyOnArrayList`: when there is write, copy and create new array
- 👍🏻 no locking
- 👎🏻 write is expensive: need to copy whole list, need to increase memory usage

## ✅ ConcurrentHashMap의 동작 과정을 SynchronizedMap과 비교하여 설명해 주세요.

- `SynchronizedMap`: only one thread can access map
- use lock
- 👎🏻 not very performant, slow

- `ConcurrentHashMap`: divide map into segments
- read: non-blocking
- writing: block only small segment of map
- 👍🏻 multi thread safe, fast

## ✅ Vector, Hashtable, Collections.SynchronizedXXX의 문제점은 무엇인가요?

- 👎🏻 global locking: only one thread can write/read
- 👎🏻 same lock for read and write: if one thread is reading, blocking thread is also blocked
- 👎🏻 scalability issue: cannot scale to multi-core systems, create bottleneck
- 🚫 not recommended to use `Vector, Hashtable, Collections.SynchronizedXXX`
- 🍀 instead, use `ConcurrentHashMap`, `CopyOnWriteArrayList`. `concurrent package`

## ✅ 가시성 문제에 대해 조금 더 자세히 설명해 주세요. 여러 스레드가 모두 한 CPU의 캐시 메모리를 읽으면 가시성 문제가 발생하지 않을 것 같은데, 어떻게 생각하시나요?

- 🔶 multi core processor: each CPU has own cache
- 🔶 cache coherence delay: cache copy is not instantaneous, can have delay

- 💊 `volatile`
- 💊 `synchronized`
- 💊 use `final`

## ✅

## ✅
