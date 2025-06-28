---
title: Docker volume, MySQL, PostgreSQL, MongoDB
categories: [Deploy, Docker]
tags: [] # TAG names should always be lowercase
---

## ✅ Docker volume

- command: `-v`

- volume: to save data on host memory
- can keep data **regardless** of container
- instead of container, save data on host memory
- ⚠️ if not use volume, when container is removed/replaced, all data will also de lost
- even if container is removed, data is not removed

## ✅ MySQL

```bash
# run sql
# sql needs password setting
# set password to 12341234
docker run -e MYSQL_ROOT_PASSWORD=12341234 -d -p 3306:3306 mysql

# go into container
docker exec -it {{containerID}} bash

# go into SQL
mysql -u root -p
```

## ✅ MySQL on Docker Volume

```bash
# make file on host computer to save data(volume)
mkdir docker-mysql

# go to the file, get file directory
cd docker-mysql
pwd

# run docker with volume
# Users/sohmac/downloads/docker-mysql 라는 폴더에
# /mysql_data라는 폴더를 또 만들어라
# 그리고 컨테이너 안의 /var/lib/mysql mysql에 저장되는 data를
# /mysql_data에 복사해서 저장해라
# [host computer directory]:[container directory]

docker run -e MYSQL_ROOT_PASSWORD=12341234 -d -p 3306:3306 -v /Users/sohmac/downloads/docker-mysql/mysql_data:/var/lib/mysql mysql

```

- ⚠️ if `host computer directory` already exists, `container directory` will not be initialized
- if `/downloads/docker-mysql/mysql_data` exists, mySQL setting files will not be created
- so `host computer directory` should be newly created, and `container directory` data should be **copied** to host computer

```
볼륨 설정 시 호스트의 지정 경로에 이미 파일이 있다면, 해당 내용이 컨테이너 내부 경로를 덮어쓰게 된답니다. 컨테이너 이미지에 원래 있던 파일들은 가려지게 되죠. 이것이 데이터베이스 초기 구동에 필요한 파일까지 덮어써서 오류가 발생할 수 있어요.
```

## ✅ ETC

```bash
# create folder
mkdir {{folder}}

# remove folder
rm -rf {{folder}}
```

## ✅ PostgreSQL

```bash
# create folder
mkdir docker-postgresql

# run postgresql
# 새로운 폴더 postgres-data를 만들고
# 컨테이너의 /var/lib/postgresql/data를 volume 폴더 postgres-data에 저장한다

docker run -e POSTGRES_PASSWORD=12341234 -p 5432:5432 -v /Users/sohmac/downloads/docker-postgresql/postgres-data:/var/lib/postgresql/data -d postgres
```

## ✅ MongoDB

```bash
# create folder
mkdir docker_mongo

# run mongoDB
# 새로운 폴더 mongo_data를 만들고
# 컨테이너의 /data/db를 volume 폴더 mongo_data에 저장한다

docker run -e MONGO_INITDB_ROOT_USERNAME= root -e MONGO_INITDB_ROOT_PASSWORD=12341234 -d -p 27017:27017 -v /Users/sohmac/downloads/docker_mongo/mongo_data:/data/db --name my-mongo mongo
```

## ✅
