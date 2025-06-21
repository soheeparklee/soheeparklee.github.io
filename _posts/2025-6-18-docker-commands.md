---
title: Docker commands
categories: [Deploy, Docker]
tags: [] # TAG names should always be lowercase
---

## ✅ create image, container and run container

```bash
-- create image, container and run container
docker run nginx
docker run mysql

-- run docker in background
run nginx -d nginx

-- name container
docker run -d --name my-web-server nginx

-- run container in a certain port
-- host port: 4000, (localhost:4000으로 접속)
-- container port: 80
docker run -d -p 4000:80 nginx

-- get running containers
docker ps

-- get all containers
docker ps -a
```

## ✅ Image commands

- can download images in dockerhub.com

```bash
-- download image
docker pull nginx

-- get image, check downloaded image
docker image ls

-- delete image
docker image rm {{imageID}}

-- force delete image
docker image rm -f {{imageID}}

-- delete all images
docker image rm $(docker images -q)
```

## ✅ Container commands

```bash
-- create container
docker create nginx
docker create mysql

-- get all created containers
docker ps -a

-- start the container
-- now ps -a STATUS would be "up"
docker start {{containerID}}

-- stop container
docker stop {{containerID}}

-- force stop container
docker kill {{containerID}}

-- remove stopped container
docker rm {{containerID}}

-- delete all containers
docker rm $(docker ps -qa)

-- stop and remove container
docker rm -f {{containerID}}
```

## ✅ Logs

```bash
-- read logs
docker logs {{containerID}}

-- tail read logs
docker logs --tail 10 {{containerID}}

-- read live logs
docker logs -f {{containerID}}

-- read live logs of tail
docker logs --tail 0 -f {{containerID}}
```

## ✅ container 접속하기

```bash
docker exec -it {containerID}} bash
```

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅
