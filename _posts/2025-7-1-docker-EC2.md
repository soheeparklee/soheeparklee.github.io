---
title: Docker with AWS EC2
categories: [Deploy, Docker]
tags: [] # TAG names should always be lowercase
---

## ✅ Install Docker

- reference AWS
- <https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/install-docker.html>

```bash
# update
sudo yum update -y

# install
sudo yum install -y docker

# start Docker
sudo service docker start

# add user
sudo usermod -a -G docker ec2-user

# close connection
# create new connection
# now try running docker commands
docker ps
```

## ✅ AWS ECR

- ECR: Elastic Container Registry
- `AWS ECR`에 image를 저장해두었다가 다운받을 수 있음. 일종의 저장소
- 👍🏻 `AWS`내에서 한번에 관리할 수 있고, 다른 AWS resource와 연동이 편하다

- 👎🏻 기존에는 EC2에 `JDK`, `MySQL`, `Redis`...등 필요한 프로그램을 다 설치하고 프로젝트를 `push, pull`해서 사용해야 했음
- 👍🏻 Docker만 깔려있으면 어디에서든 내가 원하는 프로젝트 실행 가능
- 내 프로젝트에서 필요한 코드에 대해서만 `Docker Image`로 `build`하고
- EC2에서는 그 `이미지`만 다운받아서 실행
- 프로젝트 코드 전체를 EC2로 옮겨 실행 ❌
- 훨씬 simple!
- 간단하게 프로젝트 deploy, run가능

## ✅ AWS IAM 설정하기

- IAM에 `AmazonEC2ContainerRegistryFullAccess`추가하기

[![Screenshot-2025-07-01-at-12-11-56.png](https://i.postimg.cc/MG2MBMVL/Screenshot-2025-07-01-at-12-11-56.png)](https://postimg.cc/VJgkQN79)

- access key, secret key 파일로 받아서 저장해 둘 것

- 이제 `AWS CLI`를 설정하고 권한을 주어야 한다

```bash
# AWS CLI 설치되어 있는지 확인
aws --version

# configure access key
aws configure
```

- 1️⃣ local bash에 권한 주기

[![Screenshot-2025-07-01-at-12-11-33.png](https://i.postimg.cc/9FLszy5W/Screenshot-2025-07-01-at-12-11-33.png)](https://postimg.cc/VdbKVrkT)

- 2️⃣ EC2접속해서 명령 권한 주기

[![Screenshot-2025-07-01-at-12-11-21.png](https://i.postimg.cc/rwmX9QC0/Screenshot-2025-07-01-at-12-11-21.png)](https://postimg.cc/jLGFx61t)

## ✅ AWS ECR

- create repository
- private repository
- 이름 정하고
- 아래는 건드리지 않고 그냥 생성

- 생성 후 repository에 들어가면 image있음
- 생성 직후에는 image 없을 것

[![image.png](https://i.postimg.cc/8PLjSkqB/image.png)](https://postimg.cc/PPrtbHfP)

- 이를 눌러서 명령어 보고
- 1️⃣ local bash에 명령어 따라치기
- 2️⃣ EC2접속해서 명령어 따라치기
- 이렇게 같은 명령을 두 번 실행한다

- create image

## ✅

## ✅

## ✅

## ✅

## ✅
