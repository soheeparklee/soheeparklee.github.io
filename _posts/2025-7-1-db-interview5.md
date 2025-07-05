---
title: Interview_Transaction, ACID, Isolation, Deadlock
categories: [Database, DB]
tags: [] # TAG names should always be lowercase
---

## ✅ What is a DB session?

- ✔️ **DB session**: **logical connection** between user(application) and DB
- DB session starts when user makes the connection
- and ends when user disconnects

- allow DB to track user activity like `queries`

## ✅ What is a connection in the context of databases?

- ✔️ **connection**: acutal network link between user and DB
- enable data exchange

## ✅ What is a transaction in databases?

- ✔️ **Transaction**: group of one or more operations that need to be **executed together** as a **single unit of work**

- all operations must succeed(`commit`) or fail(`rollback`)
- 👍🏻 transactions help keep your data consistent

## ✅ What is a commit in a database?

- ✔️ **Commit**: permanently save changes made in a transaction
- transaction success

## ✅ What is a rollback in a database?

- ✔️ **Rollback**: undo all changes made by current transaction
- restore DB to its previous state
- transaction fail

## ✅ What is Auto Commit in a database?

- ✔️ **Auto Commit**: `Auto Commit` automatically commits each SQL after execution
- in `MySQL`, `Auto Commit` is ON by default
- if you turn it off, you have to save manually yourself

## ✅ Why would you set Auto Commit to false?

- 👍🏻 if you want to group multiple operations into a single transaction
- 👍🏻 reduce unnecessary commits, and improve performance

- instead of saving after each line, save after writing whole paragraph

## ✅ How do developers handle manual commit when Auto Commit is off?

- Manually call `COMMIT` after finishing operation
- use `SpringBoot` annotation such as `@Transactional`

## ✅ What are ACID properties of transactions?

- ✔️ **Atomicity**: transaction should occur in one single work unit, all or nothing
- ✔️ **Consistency**: Even if money moved from A to B, sum should be the same.
- ✔️ **Isolation**: Transaction must not interfere with each other
- ✔️ **Durability**: Once commited, data should remain even if DB fails

## ✅ What is transaction isolation level?

- ✔️ **Transaction Isolation Level**: how transactions interact with each other
- low isolation level: better performance, less safe
- (ex) read uncommited

- high isolation level: more safe, lower performance.
- (ex) serializable

## ✅ What are the problems that can occur due to low isolation levels?

- 💥 **Dirty Read**: read data that has been changed, but not commited
- if data is rolled back, you have read wrong data

- 💥 **Non-repeatable Read**: same query returns different result
- another transaction changes the data

- 💥 **Phantom Read**: new rows appear between reads
- after `INSERT`, `SELECT` would return new results

## ✅ What are the common isolation levels?

- 1️⃣ **READ UNCOMMITED**: read data before commit, if roll-back, you get dirty read

- 2️⃣ **READ COMMITED**: only read commited data

- 3️⃣ **REPEATABLE READ**: same query, same result

- 4️⃣ **SERIALIZABLE**: full isolation, `one-at-a-time`

```
Isolation Strength →
READ UNCOMMITTED < READ COMMITTED < REPEATABLE READ < SERIALIZABLE
          ↑                ↑               ↑                ↑
    High performance   Balanced     Better safety     Best consistency

```

## ✅ What is the default isolation level of major RDBMSs?

- MySQL: REPEATABLE READ
- PostgreSQL: READ COMMITED
- Oracle: READ COMMITED

## ✅ What is the Lost Update Problem? Can you explain with a real-world example?

- ✔️ **Lost Update**: When two transactions read the same data and update, but one update is **overwritten** by the other

```
Two ATM withdrawals happen simultaneously on the same account.

T1 reads balance: $1000
T2 reads balance: $1000
T1 subtracts $200 → writes $800
T2 subtracts $500 → writes $500 (overwrites T1)
Final balance = $500, not correct $300 → T1’s update is lost.
```

- 💊 fix: use **locking** or **atomic updates**

## ✅ What is a Dirty Read? And how can we solve?

- ✔️ **Dirty Read**: read data that is not commited
- if rolledback, the read is invalid

```
T1 updates order status to "Shipped"
T2 reads the status → shows "Shipped" to user

T1 rolls back → status was never really “Shipped”
```

- 💊 fix: use **READ COMMITED**

## ✅ What is an Unrepeatable Read?

- ✔️ **Unrepeatable Read**: when read again with same query, different result
- read same data twice, but see different value
- due to another commited transaction modifying data in between the queries.

```
T1 reads product stock: 50
T2 updates stock to 40 and commits

T1 reads again: now sees 40
```

- 💊 fix: use **REPEATABLE READ**

## ✅ What is a Phantom Read?

- ✔️ **Phantom Read**: when new rows are added or deleted between two identical queries within same transaction
- read before `INSERT`, so when read `SELECT` different result

```
T1: SELECT * FROM employees WHERE dept = 'IT' → returns 3 rows
T2 inserts a new IT employee and commits

T1 runs same query again → returns 4 rows
```

- 💊 fix: use **SEREALIZABLE**

## ✅ What is Two-Phase Locking (2PL)?

- ✔️ **Two-Phase Locking (2PL)**: concurrency control method
- protocol that ensure serializability
- ensure serializability by divide transaction into two phases

- 1️⃣ **Growing phase**: Transacation can aquire lock, but cannot release any
  - locking only
- 2️⃣ **Shrinking phase**: Transacation can release lock, but cannot aquire any
  - unlocking only
- 👍🏻 ensure transactions do not interfere with one another

- T2 wants to run, but has to wait until T1 finishes
- T1 has to hold all locks until it commits(`Growing phase`)
- when T1 finishes(release lock) has to wait, cannot aquire lock(`Shrinking phase`)

```
A: 500, B: 800
T1: Transfer $100 from A ➡️ B
T2: Transfer $200 from B ➡️ A

T1: Transfer $100 from A ➡️ B
1. Lock A(X-lock)
2. Read A=500
3. Subtract 100, A=400
4. Lock B(X-lock)
5. Read B=800
6. Add 100, B=900
7. Commit
8. Release locks on A and B
T1 holds all locks(cannot release) until commit

T2 must wait if wants to access A or B
so now T2 can start after T1 commits
now start T2: Transfer $200 from B ➡️ A
```

## ✅ What is Serializability?

- ✔️ **Serializability**: result of _concurrent transaction_ should be same to serial(one-by-one) transaction execution
- 두 transaction이 동시에 실행된 결과와, 하나하나 순서대로 실행된 결과가 같아야 함
- so, for _concurrent transactions_, serializability is very important!
- 👍🏻 prevent anomalies like `dirty read`, `lost updates`

- ✔️ Types of serializability
- 🍀 **Conflict Serializability**: convert concurrent schedule into a serial one
- by swapping _non-conflicting_ operations
- **confict**: operations from different transactions conflict if:
  - they access same data
  - at least one is write
  ```
  T1: Read(A) → Write(A)
  T2: Read(A) → Write(A)
  ❌ not conflict serializable, bc T2 would overwrite what T1 did
  ```
  ```
  T1: Read(A) → Write(A)
  T2: Read(B) → Write(B)
  ⭕️ conflict serializable, T1 and T2 access different data
  ```
- 🍀 **View Serializability**: same data reads/writes and final writes, guarantee same final view of the data

## ✅ What are Locking Protocols?

- ✔️ **2PL**: two-phase locking

- ✔️ **Strict 2PL**: locks held until commit

- ✔️ **Timestamp Ordering**:

- 👍🏻 avoid anolmalies like dirty read
- 👍🏻 ensure consistency

## ✅ What is Deadlock?

- ✔️ **Deadlock**: where two transactions wait forever for each other to release resource/lock

## ✅ How can you prevent Deadlocks?

- avoid `no preemption`: if process has to wait, preempt resource
- **Resource ordering**: avoid `circular wait`: resources have order. in order to have 2, need to have 1.
- avoid `hold and wait`: when need resource, free all resource and ask for it
- **Wait-die scheme**: Older transactions wait, newer ones abort
- **No wait**: if lock is unavailable, abort

## ✅ How do you detect Deadlocks?

- use **Wait-For Graph**
- if there is a cycle in the graph, deadlock exists

## ✅ How do you recover from Deadlock?

- ✔️ Process Termination: kill transaction, usually youngest or least cost
- ✔️ Resource Preemption: release locks
- ✔️ rollback and restart

## ✅ What is Cascading Abort?

- If one transaction aborts,
- all the other transactions that **read its uncommited changes** must also abort
- 💊 use Strict Schedule

## ✅ What are Strict Schedules?

- ✔️ **Strict Schedules**: transaction can’t read or write a value until the transaction that wrote it commits
- 👍🏻 prevent cascading abort
- 👍🏻 prevent dirty read

## ✅ What are Recoverable Schedules?

- ✔️ **Recoverable Schedules**: transaction that reads data only commits **after** the other writing transaction commits

```
T1: write data
T2: read data that T1 wrote

T2 will commit
after T1 writes and commits that data
T2 will wait and only commit after T1 commits

if T1 aborts, T2 will also abort
```

- dirty read might happen, but will not be commited
- 👍🏻 ensure correctness in rollback
