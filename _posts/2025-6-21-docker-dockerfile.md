---
title: Docker file
categories: [Deploy, Docker]
tags: [] # TAG names should always be lowercase
---

## ✅ Docker file

- `docker file`: file to create `docker image`
- `docker image` is created using `docker file`

## ✅ FROM

- create base image
- `ubuntu`, `JDK`, `Node`

```dockerfile
FROM ubuntu:latest

ENTRYPOINT ["/bin/bash", "-c", "sleep 500"]
```

```dockerfile
FROM openjdk:17-jdk

ENTRYPOINT ["/bin/bash", "-c", "sleep 500"]
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

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅
