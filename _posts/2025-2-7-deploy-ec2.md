---
title: EC2, CICD, Github Actions
categories: [Deploy, CICD]
tags: [] # TAG names should always be lowercase
---

## ✅ Deployment

- upload my service on network
- so other users can access my service through ingernet

## ✅ EC2

- Elastic Compute Cloud
- borrow one `computer/server` from AWS
- storage: `30GB`, `gp3`

## ✅ EC2 Instance

- one single computer on a EC2 server
- instance type: computer performance
- key pair: key to login to instance

## ✅ IP and Port

- IP: computer's address on network
- port: process's address on computer

```
61.41.153.2:8080

61.41.153.2: IP address
8080: port
```

- on single computer, many programs are running
- IP를 알아서 이 컴퓨터까지 찾아왔는데, 이 컴퓨터에 여러 개의 프로세스 실행 중
- 이 컴퓨터의 어떤 프로세스에 연결해야 함? ➡️ port번호를 보고 알 수 있음

## ✅ Elastic IP

- fix an IP address so that IP address does not change

## ✅ CI/CD

<img width="720" alt="Image" src="https://github.com/user-attachments/assets/87dbc537-afad-407e-83a0-0d6e0ea789ba" />

## ✅ Github Actions

- Github Actions: `CICD` 자동화 로직을 실행시킬 수 있는 일종의 컴퓨터
- 내가 `CICD` 로직을 작성하면, Github Actions가 `build, test, deploy`수행해준다

<img width="700" alt="Image" src="https://github.com/user-attachments/assets/7b8a6ce8-7d02-406f-a28b-952f99851130" />

- 1. 코드 작성 후 Commit
- 2. Github에 Push
- 3. Push를 감지해서 Github Actions에 작성한 로직이 실행
  - 1.  빌드(Build)
  - 2.  테스트(Test)
  - 3.  서버로 배포(Deploy)
- 4. 서버에서 배포된 최신 코드로 서버를 재실행

## ✅ Github Actions 사용 이유

- 👍🏻 build용 서버가 따로 필요하지 않아 비용이 적게 든다
- 👍🏻 서버 세팅도 필요 없으니 시간, 비용 절약
- 🆚 Jenkins는 별도의 서버가 필요하다, 서버 빌리는 비용 발생

## ✅

## ✅

## ✅
