---
title: GIT 깃 전략
categories: [GIT, GIT_Basics]
tags: [project]
---

## ✔️ Feedback

- 기능별로 이슈를 따서 쪼개기
- 그래서 페이지당 기능별로 브랜치를 따서 계속 머지하면서 작업
- 머지할 때는 pr받아서 꼬이지 않도록 하기
- git-flow
- mash-up-kr
- 기능 이걸 개발해서 디벨롭 브랜치에 머지한다

## ✔️ GIT flow

#### 🌳 develop

> 다음 출시 버전을 개발하는 브랜치

- develop은 master에서 시작되었음
- 상시로 버그를 수정하거나 기능을 개발한 브랜치가 추가됨

#### 🌳 feature branch

> 각각의 기능을 개발하는 브랜치

- 새로운 기능을 추가하는 경우 develop에서 feature branch를 만듦.
- 기능 개발 후 develop으로 merge
- merge할 때 pull request필요

#### 🌳 release branch

> 이번 버전 출시를 준비하는 브랜치

- develop에 모든 기능이 merge되었다면 QA를 하기 위해 develop에서 release라는 브랜치 생성
- QA를 하면서 수정사항은 release 브랜치에 수정
- QA를 모두 통과하면 release 브랜치를 master, develop브랜치로 merge

## ✔️ Example

```bash
-- 현재 이 브랜치 upstream/feature-user

-- make featureA branch
git fetch upstream
git checkout -b featureA –track upstream/feature-user

-- develop
-- commit
git commit -m "featureA 개발 완료"

-- 두 개의 커밋을 합치려면 squash
git rebase -i HEAD~2

-- rebase
git pull –rebase upstream feature-user

-- push
git push origin featureA

-- featureA를 upstream/feature-user에 merge
```

##### 💡 QA

> Quality Assurance

#### 🌳 master

> 제품으로 출시하는 브랜치

- 출시

## GIT flow 🆚 GITHUB flow

A simpler branching strategy optimized for continuous deployment and integration.
Focuses on simplicity and rapid deployment.
Branches:

Main (or Master): The default branch where production-ready code lives.
Feature branches: Created from main for developing new features or fixing bugs.

💡 참고: <https://techblog.woowahan.com/2553/>

## JIRA

## ⭐️ What I want to implement

- making feature branches to develop one issue
- rebase
