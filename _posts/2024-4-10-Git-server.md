---
title: Git clone a repo to another repo
categories: [GIT, GIT_Basics]
tags: [commands] # TAG names should always be lowercase
---

### 1. 클론하기

```bash
//  git clone --bare {repo to clone}
 git clone --bare https://github.com/soheeparklee/soheeparklee.github.io.git
```

### 2. 여기에

```bash
// find file
 cd soheeparklee.github.io.git

```

### 3. mirror push

```bash
// git push --mirror {where to clone}
git push --mirror https://github.com/soheeparklee/githubBlog_forGreen.git
```

### 4. back to main

```bash
cd ..
```

### 5. erase

```bash
// rm -rf {what to erase}
rm -rf soheeparklee.github.io.git
```
