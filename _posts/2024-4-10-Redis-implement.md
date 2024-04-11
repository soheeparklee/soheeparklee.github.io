---
title: Redis_GitCommands
categories: [Redis]
tags: [redis] # TAG names should always be lowercase
---

## ✅ Install

First, brew has to be installed

```bash
// brew 버전 확인
brew --version
```

```bash
// redis 설치
brew install redis

// redis 설치 제거
brew uninstall redis

// redis 버전 확인
redis-server --version
```

## ✅ Run Redis on ForeGround

🔴 This will not allow other works to be run on terminal

```bash
// redis foreground로 실행
redis-server
```

## ✅ Run Redis on BackGround

```bash
// redis background로 실행
brew services start redis

// redis background로 재실행
brew services restart redis

// redis background로 중지
brew services stop redis
```

### redis 실행 상태 확인

```bash
// redis 실행 상태 확인
brew services info redis
```

## ✅ Terminate Redis running on port 6379

```bash
-- open new tab
-- connect to the Redis server:
redis-cli

-- 끄기
SHUTDOWN
```

## ✅ Redis CLI

> > Redis CLI(Command Line Interface)는 Redis 명령어 라인 인터페이스입니다.
> > 즉, Redis를 사용하기 위해 제공되는 Redis 명령어입니다.
> > 해당 명령어를 이용하여 Redis에 값을 쓰고, 조회하고, 삭제할 수 있습니다.

#### Redis CLI 사용

```bash
// redis-cli 사용
redis-cli
```

#### 데이터 생성, 수정

```bash
// redis 데이터 생성, 수정(같은 key값이 존재하면 데이터만 업데이트됨)
// set {key} {value}
// set {키 이름} {내가 입력하고 싶은 값}
set mykey myvalue
```

#### 데이터 조회

```bash
// redis 데이터 조회
// get {key}
get mykey
```

#### Key 목록 조회

```bash
keys *
```

#### Key 수정

```bash
// rename {기존키} {변경키}
rename mykey mykey2
```

#### Key 개수 조회

```bash
dbsize
```

#### Key(데이터) 삭제

```bash
// del {key}
del mykey2
```

#### Key(데이터) 전체 삭제

```bash
flushall
```
