---
title: Git terminate port
categories: [GIT, GIT_Basics]
tags: [port, terminate] # TAG names should always be lowercase
---

### 1. what is listening on port 8080?

lsof: list open files

```bash
lsof -i :8080
```

```bash
kill PID
```
