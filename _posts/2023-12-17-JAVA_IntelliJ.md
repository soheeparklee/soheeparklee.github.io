---
title: Java IntelliJ
categories: [JAVA, JAVA_Basics]
tags: [debugger, profiler] # TAG names should always be lowercase
---

## 🛠️ IntelliJ Profiler

CPU를 어떻게 쓰고 있는지 보여주는 도구
자바에서 우리가 설정하지는 않았지만 돌아가고 있는 class, methodㄷ도 보여준다.
memory를 어떻게 쓰는지 보여줌

## 🛠️ IntelliJ Debugger

🔴 브레이크 포인트: 빨강점, 여기서 멈추기
한 걸음씩 가거나 그 메소드 안으로 가서 어떤 동작이 일어나는지 보기 위함
진행 값을 시시각각 확인할 수 있음

🔴 붙인거 전 줄에 멈춤

- step over: 한 걸음 가면 그 줄 실행
- step into: 실행되는 메소드로 가기
- force step into: 원래 JAVA가 가지고 있는 class `System.out.println()`같은 메소드는 `step into`가 안 된다.
  그래서 `force step into`로 억지로 그 메소드 안으로 들어가기
- out: 다시 나가기

- resume program: breakpoint2개 찍고 resume program실행하면, 두 브레이크 포인트 사이 코드만 실행한다. 첫 번째 브레이크 포인트에서 두 번째 브레이크 포인트로 이동
