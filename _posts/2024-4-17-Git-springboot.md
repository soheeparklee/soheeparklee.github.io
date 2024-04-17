---
title: How to bring IntelliJ project to already existing github repository?
categories: [GIT, GIT_Basics]
tags: [commands] # TAG names should always be lowercase
---

### 1. Make an intelliJ project with SpringBoot

만들 때 스프링부트 가지고 실행

<img width="798" alt="Screenshot 2024-04-17 at 01 07 39" src="https://github.com/soheeparklee/githubBlog_forGreen/assets/97790983/ff1621a2-76be-4e61-a4ca-4484838fd25c">

### 2. I dont have a github repository yet

이 경우는 쉽다.
git으로 가서 `share project on github`

<img width="1063" alt="Screenshot 2024-04-17 at 01 10 05" src="https://github.com/soheeparklee/githubBlog_forGreen/assets/97790983/091e9f79-d945-485d-b246-5c9b1c153f0d">

### 3. I have a github repository already

이럴 경우에는 `manage remotes`

<img width="1056" alt="Screenshot 2024-04-17 at 01 10 41" src="https://github.com/soheeparklee/githubBlog_forGreen/assets/97790983/c8ce03f8-5c49-402d-a2b7-14ad2997ce2e">

그리고 깃허브 url을 넣어준다.

<img width="587" alt="Screenshot 2024-04-17 at 01 11 17" src="https://github.com/soheeparklee/githubBlog_forGreen/assets/97790983/57c5d951-05ed-4210-bfed-6b3ed1f23c06">

깃허브 url이라 하면 바로 여기있는 url

<img width="706" alt="Screenshot 2024-04-17 at 01 12 25" src="https://github.com/soheeparklee/githubBlog_forGreen/assets/97790983/e8ad316f-85e5-424c-88bb-f6d60286ea58">

그리고 commit을 보면 springboot설치하면서 변경된 내용들을 커밋하라고 나온다.
<img width="1059" alt="Screenshot 2024-04-17 at 01 13 57" src="https://github.com/soheeparklee/githubBlog_forGreen/assets/97790983/2b3a3e88-4c19-46fd-a148-0cbe9a1845e8">

하지만 우리는 커밋할 수가 없다. 왜냐? 우리는 아직 메인브랜치가 없기 때문이다.
<img width="1240" alt="Screenshot 2024-04-17 at 01 16 32" src="https://github.com/soheeparklee/githubBlog_forGreen/assets/97790983/58d143f5-524a-4ef2-a47e-83f88965b402">

그러니까 터미널에서 친절하게 알려준대로, 시키는대로 한다.

```git
git push --set-upstream origin main
```

<img width="1163" alt="Screenshot 2024-04-17 at 01 17 55" src="https://github.com/soheeparklee/githubBlog_forGreen/assets/97790983/4a8c8b6e-10f1-4644-90a1-ba3a839fdeba">

그러면 짠! 스프링부트가 설치되어 커밋된 우리의 프로젝트를 볼 수 있다.

<img width="715" alt="Screenshot 2024-04-17 at 01 19 26" src="https://github.com/soheeparklee/githubBlog_forGreen/assets/97790983/16c2c339-5888-4b42-a9b3-f0ea510267aa">

### 4. 참고자료

[https://velog.io/@ssoop/%EA%B9%83%ED%97%88%EB%B8%8CGitHub-%EC%97%B0%EB%8F%99%ED%95%98%EA%B8%B0-Spring-Boot-IntelliJ]
