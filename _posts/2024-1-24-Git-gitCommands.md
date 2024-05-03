---
title: Git push, commit, merge error
categories: [GIT, GIT_Basics]
tags: [commands] # TAG names should always be lowercase
---

### branch 생성하기

```bash
 git checkout -b comment
```

### branch 옮기기

```bash
 git checkout comment
```

### commit, push

```bash
git add .
git commit -m "바꾼내용"
git push

```

### how to merge

보통은 pull request하면 되지만 머지가 안 되는 경우 <br>

#### ❌ Cannot automatically merge

먼저 develop에 commit branch를 머지하였고 이후 post branch를 머지하려고 했더니 Cannot automatically merge에러가 떴다. post입장에서는 자기가 만들어졌을 때 develop의 모습과 commit branch가 머지된 현재의 develop 모습이 너무 다르기 때문이다. 이럴 때 해결방법은 다음과 같다.

1. 먼저 post branch를 개발한 사람의 컴퓨터에서 develop으로 체크아웃한다.

```bash
git checkout develop
```

2. develop에서 pull을 통해 바뀐 develop의 내용들을 가져온다.

```bash
git pull origin develop
```

3. 다시 post branch로 체크아웃한다.

```bash
git checkout post
```

4. 그러면 다시 develop으로 merge했을 때 오류없이 머지가 가능하다.

```bash
git merge develop
```

5. 문제가 생기면 코드 수정

```bash
git add .
git commit -m “merge error fix”
git push
```

6. 다시 pull request하면 문제없이 merge 가능!
