---
title: How to bring IntelliJ project to already existing github repository?
categories: [GIT, GIT_Basics]
tags: [commands] # TAG names should always be lowercase
---

## 1. Make an intelliJ project with SpringBoot

만들 때 스프링부트 가지고 실행 <br>
<img width="798" alt="Screenshot 2024-04-17 at 01 07 39" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/2a4673c4-5943-4b92-af76-eb6fc6e3cd2f">

## 2. I dont have a github repository yet

이 경우는 쉽다. <br>
git으로 가서 `share project on github` <br>

<img width="1020" alt="Screenshot 2024-04-17 at 01 29 15" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/793fdb7e-fdba-42fc-9a86-88771c8df33d">

## 3. I have a github repository already

이럴 경우에는 `manage remotes` <br>
<img width="953" alt="Screenshot 2024-04-17 at 01 29 42" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/4507e94c-f77e-46e4-94c0-d54bf4b58903">

그리고 깃허브 url을 넣어준다. <br>

<img width="587" alt="Screenshot 2024-04-17 at 01 11 17" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/57094b60-c263-4a52-b2d4-937454556338">

 <br>

깃허브 url이라 하면 바로 여기있는 url <br>

<img width="706" alt="Screenshot 2024-04-17 at 01 12 25" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/ab2e01eb-18f2-4d8a-a2b4-a09e046fee63">

그리고 commit을 보면 springboot설치하면서 변경된 내용들을 커밋하라고 나온다. <br>
<img width="1059" alt="Screenshot 2024-04-17 at 01 13 57" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/48524c02-43c3-4693-8f5e-3cde46f0c89b">

하지만 우리는 커밋할 수가 없다. 왜냐? 우리는 아직 메인브랜치가 없기 때문이다. <br>
<img width="1240" alt="Screenshot 2024-04-17 at 01 16 32" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/dfaebd52-26ea-4fdc-9b2e-fe31a37ba41b">

그러니까 터미널에서 친절하게 알려준대로, 시키는대로 한다. <br>

```
git push --set-upstream origin main
```

 <br>

<img width="1163" alt="Screenshot 2024-04-17 at 01 17 55" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/df92ac09-bb06-4dbc-8d73-15ae40ec8277">

그러면 짠! 스프링부트가 설치되어 커밋된 우리의 프로젝트를 볼 수 있다. <br>

<img width="710" alt="Screenshot 2024-04-17 at 01 31 34" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/0de082d6-a13c-4edf-aaeb-2fdba24fd0b5">

## 4. 참고자료

<https://velog.io/@ssoop/%EA%B9%83%ED%97%88%EB%B8%8CGitHub-%EC%97%B0%EB%8F%99%ED%95%98%EA%B8%B0-Spring-Boot-IntelliJ>
