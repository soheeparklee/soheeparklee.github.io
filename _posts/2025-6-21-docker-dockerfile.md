---
title: Docker file 작성하기, SpringBoot, Next.js, HTML올리기
categories: [Deploy, Docker]
tags: [] # TAG names should always be lowercase
---

## ✅ Docker file

- `docker file`: file to create `docker image`
- `docker image` is created using `docker file`
- 이미 만들어진 image가 아니라, 내가 원하는 이미지를 만들고 싶을 수 있음
- 이때 사용하는 것이 `docker file`

## ☑️ FROM

- create base image
- `ubuntu`, `JDK`, `Node`

```dockerfile
FROM ubuntu:latest

ENTRYPOINT ["/bin/bash", "-c", "sleep 500"]
# 500초동안 시스템을 일시정지시키는 명령어
```

```dockerfile
FROM openjdk:17-jdk

ENTRYPOINT ["/bin/bash", "-c", "sleep 500"]
# 500초동안 시스템을 일시정지시키는 명령어
```

- run in terminal
- inside **package** with docker file

```bash
-- inside package with docker file

-- build
docker build -t {{name of image}}
docker build -t my-node-server .

-- check image
docker image ls


-- run container
 docker run -d my-node-server
```

## ☑️ COPY

- copy file in host computer to container
- `COPY 호스트 상대경로 /container절대경로`

```dockerfile
FROM ubuntu

# host computer의 app.txt를 container의 /app.txt에 복사
COPY app.txt /app.txt

# host computer의 my-app폴더를 container의 /my-app/에 복사
COPY my-app /my-app/

# host computer의 모든 txt파일을 container의 /text-files/라는 파일에 복사
COPY *.txt /text-files/


ENTRYPOINT ["/bin/bash", "-c", "sleep 500"]
```

- ❓ if there is a file I do not want to copy?
- add to `.dockerignore`

## ☑️ ENTRYPOINT

- command to start when container is run for the first time

```dockerfile
ENTRYPOINT ["/bin/bash", "-c", "sleep 500"]
```

## ✅ Upload Springboot on Docker

- create docker file

```dockerfile
FROM openjdk:17-jdk
LABEL authors="soheeparklee"

COPY build/libs/*SNAPSHOT.jar app.jar

ENTRYPOINT ["java", "-jar", "/app.jar"]
```

- run build, run commands

```bash
-- clean build
./gradlew clean build

-- build
docker build -t java-server .

-- run
docker run -d -p 8080:8080 java-server

-- check
docker ps
```

## ☑️ RUN

- run command while creating image
- used for `install`, `set environment`

- RUN 🆚 ENTRYPOINT
- RUN: run command `while creating image`
- ENTRYPOINT: run command `after creating container`

```dockerfile
FROM ubuntu

#download git on this container
RUN apt update && apt install -y git

ENTRYPOINT ["/bin/bash", "-c", "sleep 500"]
```

- create `ubuntu` container
- install `git` with `RUN command`
- after container is created, run `ENTRYPOINT`

## ☑️ WORKDIR

- set work directory to save the files
- to maintain packages in container in an organized way

```dockerfile
FROM ubuntu

WORKDIR /my-dir

COPY ./ ./

ENTRYPOINT ["/bin/bash", "-c", "sleep 500"]
```

- now all dockerfiles will be created in `/my-dir` folder

## ☑️ EXPOSE

- document the `port` that the programming is running

```dockerfile
EXPOSE 3000
```

## ✅ Upload Nest.js

- install npm, create project

```bash
# install
sudo npm i -g @nestjs/cli

# create
nest new my-server
```

- dockerfile

```dockerfile
FROM node
WORKDIR /app

COPY . .

RUN npm install
RUN npm run build

EXPOSE 3000


ENTRYPOINT ["node", "dist/main.js"]
```

## ✅ Upload Next.js

- create project

```bash
npx create-next-app@latest
```

- dockerfile

```dockerfile
FROM node:20-alpine #simplified version of node:20

WORKDIR /app

COPY . .

RUN npm install
RUN npm run build

EXPOSE 3000

ENTRYPOINT ["npm", "run", "start"]

```

- run container

```bash
npm run dev

docker build -t my-server .

docker run -d -p 80:3000 my-server
```

## ✅ Upload HTML

- create project

```bash
mkdir my-server
```

- create `index.html`, `style.css`
- create dockerfile

```dockerfile
FROM nginx

COPY ./ /usr/share/nginx/html
```

- build and run

```bash
docker build -t my-server .

docker run -d -p 80:80 my-server
```

## ✅

## ✅
