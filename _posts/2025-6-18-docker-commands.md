---
title: Docker commands
categories: [Deploy, Docker]
tags: [] # TAG names should always be lowercase
---

## ✅ ccreate image, container and run container

```bash
-- create image, container and run container
docker run nginx
docker run mysql
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

-- remove container
docker rm {{containerID}}

```

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅

## ✅
