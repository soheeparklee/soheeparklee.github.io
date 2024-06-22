---
title: Project Feedback
categories: [Project, Movie Reservation Project]
tags: [project]
---

## ✅ Feedback (on 22nd of May 2024)

#### ✔️ 자기 브랜치가 아닌 디벨롭 브랜치에서 개발한경우 커밋 되돌리기

실수한 경우 푸시 되돌리기

```bash
git reset --hard $커밋 & git push -f
```

#### ✔️ 깃 전략

- 기능별로 이슈를 따서 쪼개기
- 그래서 페이지당 기능별로 브랜치를 따서 계속 머지하면서 작업
- 머지할 때는 pr받아서 꼬이지 않도록 하기
- git-flow
- mash-up-kr
- 기능 이걸 개발해서 디벨롭 브랜치에 머지한다

💡 참고: <https://techblog.woowahan.com/2553/> <br>
✌🏻 What I studied: <https://soheeparklee.github.io/posts/PROJECT_MovieReservation_postFD1/>

#### ✔️ Login

- 로그인할 때 httpSeverletResponse에 setHeader을 하는게 아니라 그냥 토큰을 리턴하는 경우가 많다. 어디에 저장할지는 프론트가 정하는 것
- 로그아웃 또한 프론트에서 저장된 토큰을 쿠키에서 삭제하거나 세션스토리지에서 삭제함

#### ✔️ Repository names

- 레포지토리 이름을 movie, movieRepository라고 하기

#### ✔️ Logout

- 로그아웃되면 블랙리스트 추가, 이 블랙리스트를 레디스에 저장
- 블랙리스트 추가된 토큰을 어떻게 저장할 것인가?
- 예를 들어 키를 만들어 true하고 TTL 7일
- 그러면 로그아웃하거나 토큰시간이 만료되면 로그인 못하게 하고,
- 7일이 지나면 삭제하기에 너무 많이 저장할 필요 없도록

#### ✔️ Exceptions

- exception할 때 그냥 스트링으로 에러 메세지 내보내는게 아니라
- ApiResponse만들어서, generic써서 dto로 내보내기

#### ✔️ path를 만들 때 경로, 네이밍 주의하기

다음 개념들에 대해 공부해 볼 것

1. rest api
2. resful api

💡 참고: <https://m.boostcourse.org/web316/lecture/16740>

#### ✔️ Method code readability

- 메소드가 길지 않게 하세요
- 각각 함수로 빼서

#### ✔️ Transactional

- 이메일 보내는거 @Transactional 삭제할 것
- dirty checking
  <https://product.kyobobook.co.kr/detail/S000000935744>

#### ✔️ 실제 서비스라고 생각하고 고민해 볼 것

- 왜 예매하려다 실패하면 한 10분동안은 그 좌석을 선택을 못하게될까? 직접 예매를 해보면서 잔여좌석 관리를 어떻게할지 고민해보기
- redis쓰면 잔여관리 해결 가능함

#### ✔️ 파사드 패턴이란?

💡 참고:

#### ✔️ 서비스에서 인터페이스와 임플리멘트를 각각?

💡 참고:

#### ✔️ JWT argument resolver

💡 참고:

#### ✔️ if else에 대하여
