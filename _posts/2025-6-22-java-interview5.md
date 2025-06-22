---
title: Interview_JVM, GC
categories: [JAVA, JAVA_Basics]
tags: [] # TAG names should always be lowercase
---

## ✅ Explain the structure of the JVM

- JVM: runtime engine that enables `Java bytecode` to be executed on any platform
- **ClassLoader**: load `.class` file into JVM
- **Runtime data Area**: memory
- **Execution Engine**: interprete, compile

## ✅ 클래스 로더에 대해 설명해 주세요.

- load `.class` file into JVM
- save `class metadata` and `static` into **method area** in `memory`

- **loading**: load into memory(메모리에 로드)
- **linking**:
  - `verification`: ensure class file format follows JVM style
  - `preparation`: allocate meory for static variables(필요로 하는 메모리 할당)
  - `resolution`: convert symnolic reference into direct reference
- **initialization**: execute static blocks, assign static field
  - static field를 설정한 값으로 초기화

## ✅ 클래스 로더의 종류

- bootstrap ClassLoader: loads java core classes `java.lang.*`
- etension ClassLoader: loads classes from `lib/ext` 확장 라이브러리 로드
- application ClassLoader: loads classes from application `classpath` 사용자 정의 클래스 로드

## ✅ Explain the JVM Memory Structure in detail

- **method area**: class metadata, static, `shared by thread`
  - class field, method
  - has `Runtime Constant Pool`
- **heap area**: new instances, array, GC area, `shared by thread`
- **stack area**: local variables, parameters, `each thread has own stack`
- **PC register**: point to next command to be run, `each thread has own`
- native method stack: cade that is not java, `each thread has own`

## ✅ Why is the Heap divided into Young and Old Generations?

- **Young Generation**: store newly created objects, `for Minor GC`
  - fast GC cycles
  - use COPY as GC algorithm
- **Old Generation**: store long-living objects, `cleaned by Major GC`

  - less frequent, more expensive
  - STW
  - mark-sweep-compact, G!

- most objects in Java die young
- Minor GC is cheaper than Major GC

## ✅ GC(Garbage Collection)란 무엇인가요?

- automatic process of reclaiming memory by removing objects that are no longer referenced

- 👍🏻 prevent memory leak
- 👍🏻 manage heap memory

## ✅ GC의 장단점을 설명해 주세요.

- 👍🏻 automatically manage memory
- 👍🏻 prevent memory leak

- 👎🏻 application pause, Stop-The-World
- 👎🏻 cannot predict GC timing
- 👎🏻 Poor GC tuning can severly impact performance

## ✅ GC를 모니터링해야 하는 이유

- monitor how many times, for how long GC run to detect performance degradation

- _too frequent full GCs_ can freeze your app: STW
- _too frequent minor GCs_ can reduce throughput
- by monitoring GC, can analyze heap size ➡️ detect OOM(out of Memory error), memory leak

## ✅ how would you tune GC?

- monitor GC logs and heap dump
- tune heap size
- tune GC algorithm
- adjust GC thresholds: point that GC is triggered

## ✅ 자바로 jvm 응용 프로그램을 개발한 후에 운영하다보면 out of memory가 나올 수 있는데 이 에러가 발생했을때 어떻게 대처할 것 같으세요?

- 1. check GC logs and heap dumps
- 2. tune GC algorithm
- 3. tune heap size
- 4. check for large collections

## ✅ What is a memory leak?

- no longer referenced object not being removed by GC
- and keep accumulating ➡️ memory leak

## ✅ What causes memory leaks?

- creating meaningless instances with Wrapper class
  - `Long sum = 0L;` 만들고 1씩 만번 더하기 ➡️ `Long` 객체를 만번 새로 만들게 됨
- unreleased reference in static fields
- poorly managed large collections `Map`, `Set`, `List` that are not removed when no longer needed
- inner class that holds implicit references
- incorrect use of `equals/hashCode()` can end up saving same object many times

## ✅ How to detect memory leaks?

- analyze heap dump
- monitor GC logs

## ✅ GC에서 사용하는 알고리즘은 무엇이 있나요?

- **Mark and Sweep**: Check if object is referenced `Mark` and if not, remove `Sweep`
  - 👎🏻 can cause fragmentation
- **Copying**: move referenced objects to new space, compact memory. Used in Young Gen
- **Mark-Compact**: like mark and sweep, but compact memory to avoid fragmentation

## ✅ How does Java implement GC?

- **Serial GC**: `Mark-Sweep, Mark-Compact`, single threaded, for small heap
- **Parallel GC**: `Copying(young), Mark-Compact(olf)`, default in Java 8, multiple threads, best throughput
- **G1 GC**: `Copying(young), Mark-Compact(olf)`, default in Java 11+, divide heap into regions, prioritize area with most garbage.
  - 👍🏻 reduce STW time(Stop The World)

## ✅ Java 8 기준으로, GC는 어떤 방식으로 수행되나요?

- **Parallel GC**: for multi thread, focus on throughput
- multiple thread can run GC in parallel
- young gen: copy
- old gen: mark-compact, full heap pause

## ✅ Java 8과 Java 11의 디폴트 GC 실행 방식은 어떤 것인가요?

- Java 8: Parallel GC
- Java 11: G1 GC

## ✅ G1 GC에 대해 설명해 주세요.

- split heap into fixed size regions
- **prioritize** cleaning region with more garbage
- Prioritizes regions with the most garbage ("Garbage-First")
- 👍🏻 efficient in big heap memory, can manage better pause time and performance
- 👍🏻 short STW

## ✅ G1 GC의 Heap 구조를 설명해주세요

- Divides heap into uniform regions.
- different region for young generation, old generation
- young gen: remove short lived objects
- old gen: save long lived objects

## ✅ 왜 Java 11은 디폴트 GC를 G1 GC로 변경하였을까요?

- shorter STW
- less fragmentation of memory, as operated with regions

## ✅
