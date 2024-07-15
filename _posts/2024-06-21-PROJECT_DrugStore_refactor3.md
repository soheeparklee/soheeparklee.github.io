---
title: TroubleShooting_Too many Connections
categories: [Project, Drug Store Project]
tags: [project, trouble]
---

## ✅ 500 Error on frontend

Although everything was running just fine on postman, when connecting with frontend, there was a 500 error.

![image](https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/b1ab6ca1-ff60-473a-91db-bd1b8915fbff)

![image](https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/c32c7815-a0f3-4985-ac96-2b771558f52f)

<img width="1332" alt="Screenshot 2024-06-20 at 21 53 50" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/6cd5e094-25ae-4878-b4d4-d26671c40f65">

## 🔵 Check Max connections, wait_timeout

Go into Ubuntu then,

```bash
mysql -h drugstoredb.cn000owqib3s.ap-northeast-2.rds.amazonaws.com -u root -p
```

```bash
show variables like "%max_connections%";
```

<img width="352" alt="Screenshot 2024-06-20 at 14 39 48" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/cf367dd7-4085-46ef-9ac2-43015979b71d">

```bash
show status like "%connect%";
```

<img width="357" alt="Screenshot 2024-06-20 at 14 39 52" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/3067a990-09a6-45d6-b6d2-418b207b6a82">

```bash
show status like '%thread%';
```

<img width="335" alt="Screenshot 2024-06-20 at 14 54 10" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/81a06859-836d-4b2a-bd54-299b27a6fd88">

```bash
show variables like '%timeout%';
```

<img width="329" alt="Screenshot 2024-06-20 at 15 11 32" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/52d04ab3-ebb9-4404-8b56-6b8492761303">

나의 경우 다음과 같은 수치가 나왔다.

- Cache Miss Rate= 2.40%
- Connection Miss Rate= 17%
- Connection Usage= 53%

따라서

- wait_timeout = 180
- max_connections = 300
  으로 설정하기로 하였다.

## 🔵 Change connections, timeout

### ✔️ AWS parameter

RDS의 parameter 바꿔주기
<https://cha-vi.tistory.com/56>

설정 이후 `show variables like "%max_connections%";` 해보면 내가 바꾼 숫자로 잘 나오는 것 확인 가능

### ✔️ ubuntu mariaDB

1. Install mariaDB service

```bash
sudo apt update
sudo apt install mariadb-server

sudo systemctl start mariadb.service

```

2. Change config file

```bash
cd /etc/mysql/mariadb.conf.d/
sudo nano 50-server.cnf
```

```ini
[mysqld]
max_connections = 300
wait_timeout = 180
```

3. Restart mariaDB server

```bash
sudo systemctl restart mariadb.service
```

<img width="537" alt="Screenshot 2024-07-15 at 12 08 22" src="https://github.com/user-attachments/assets/da6bbcf9-4e7c-461f-abde-26a2f7636737">

### 💡 참고자료

- ubuntu, DB 연결 계산 방법
  <https://velog.io/@kimjiwonpg98/mysql-too-many-connections-error-%ED%95%B4%EA%B2%B0-%EB%B0%A9%EB%B2%95>

## 🔵 Check server.log

지긋지긋하던 too many connections가 사라졌다!
그리고 여러명이 동시에 접속해도 잘 작동한다.

<img width="415" alt="Screenshot 2024-07-15 at 11 57 48" src="https://github.com/user-attachments/assets/b9e30b79-02c9-4bcf-9ca1-b517c1b1073c">

![Screenshot 2024-06-20 at 21 56 52](https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/be396059-9b79-4577-8c89-455b52c6d606)
