---
title: Deploy environment EC2, RDS
categories: [JAVA, Spring]
tags: [deploy] # TAG names should always be lowercase
---

## ✅ EC2: 스프링을 올릴 수 있는 서버

- OS는 ubuntu를 사용
- 인스턴스 유형: 프리 티어
- 키 페어: make new key pair
  💡 이름 지을 때 띄어쓰기 하지 말 것(나중에 terminal에서 띄어쓰기 인식 못함)
- 네트워크: vpc-어쩌고저쩌고
  💡 이후 RDS할 때 `vpc-0c6562bc157853529 `가 동일해야 하므로 꼭 기억해두기
- 스토리지 구성: 30GB

### ☑️ 보안그룹 추가

- 인바운드 규칙에 모든 TCP - Anywhere IPv4, IPv6 총 2개 추가
- 이렇게 방화벽을 해제해야 local에서도 서버 접속 가능
  💡 이 때 VPC 주소 EC2와 일치하도록 주의 <br>
  ➡️ EC2에 보안그룹 추가<br>

### 🟢 Terminal 1: keypair

- keypair을 생성하면 Downloads에 저장된다.
- Downloads에 폴더 하나 만들어서
- 거기에다가 keypair을 복사한다.

```bash
-- Desktop으로 들어가
 ~/Desktop

-- Downloads로 들어가
 ~/Downloads

-- movie-key라는 폴더 만들어
 mkdir movie-key

-- movie-key 폴더 안으로 들어가
 cd movie-key

-- movie-key 폴더에 Downloads안에 있는 movie-reservation.pem . 라는 키페어 복사해
 cp ~/Downloads/movie-reservation.pem .

-- keypair
-- sudo chmod 400 pem키 이름: 들어올 수 있는 권한을 주기
sudo chmod 400 movie-reservation.pem
ssh -i "movie-reservation.pem" ubuntu@ec2-54-180-126-207.ap-northeast-2.compute.amazonaws.com
```

#### ✔️ 결과: `ubuntu@ ip주소`

```bash
ubuntu@ip-172-31-10-19:~$ 이제 여기에 명령어 쓸 것
```

### 🟢 Terminal 1: ubuntu에 폴더 만들어 java, git, netstat install

먼저 임시 서버에 들어와 `ubuntu@ip-172-31-10-19:~$`된 상태에서 시작

```bash
pwd
-- /home/ubuntu
mkdir movie
cd movie
```

#### ✔️ 결과: `ubuntu@ip-172-31-10-19:~/movie$`

```bash
-- 먼저 업데이트 하고
sudo apt update

-- 자바 설치
java -version
-- java 버전 여러개 뜨면 내가 설치하고 싶은 버전의 java설치
sudo apt install openjdk-17-jre-headless

-- 깃 이미 설치되어 있음
git --version

-- net-tools 설치
sudo apt install net-tools
netstat -h
```

### 🟢 Terminal 1: 서버 열기

```bash
sudo netstat -ltpn
```

#### ✔️ 결과

```bash
ubuntu@ip-172-31-10-19:~/movie$ sudo netstat -ltpn
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 127.0.0.54:53           0.0.0.0:*               LISTEN      321/systemd-resolve
tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN      321/systemd-resolve
tcp6       0      0 :::22                   :::*                    LISTEN      1/init
```

### 🟢 Terminal 1: 8080 연결

```bash
nc -lkv 8080
-- Listening on 0.0.0.0 8080
```

### 🔵 Terminal 2: keyPair있는 곳에서 임시서버와 연결

keyPair있는 폴더로 들어가기
ssh연결에서 보이는 링크로 들어가기

```bash
~/Desktop
~/Downloads
cd movie-key
ssh -i "movie-reservation.pem" ubuntu@ec2-54-180-126-207.ap-northeast-2.compute.amazonaws.com
```

임시 서버에 들어와 `ubuntu@ip-172-31-10-19:~$` 된 상태에서 시작

```bash
sudo netstat -ltpn
nc -v localhost 8080
```

#### ✔️ 결과: 8080 추가된 것 보이죠?!

```bash
ubuntu@ip-172-31-10-19:~$ sudo netstat -ltpn
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 127.0.0.54:53           0.0.0.0:*               LISTEN      321/systemd-resolve
tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN      321/systemd-resolve
tcp        0      0 0.0.0.0:8080            0.0.0.0:*               LISTEN      2115/nc
tcp6       0      0 :::22                   :::*                    LISTEN      1/init
```

#### ✔️ 결과

```bash
ubuntu@ip-172-31-10-19:~$ nc -v localhost 8080
-- Connection to localhost (127.0.0.1) 8080 port [tcp/http-alt] succeeded!
```

### 🟣 Terminal 3: 로컬에서 서버와 연결

```bash
-- 로컬에서 서버 연결
nc -v ec2-54-180-126-207.ap-northeast-2.compute.amazonaws.com 8080

```

## ✅ RDS

- 템플릿: 프리 티어
- 자격 증명 설정: 마스터 사용자 이름(db이름) root
- password
- 연결: EC2컴퓨팅 리소스에 연결 안 함
  💡 VPC 주소가 EC2와 동일해야 함 (꼭 설정할 것, 데이터베이스 생성 이후에는 VPC변경 불가)
- 퍼블릭 액세스: 예

### ☑️ 보안그룹 추가(EC2에 있음)

- 인바운드 규칙에 모든 MYSQL/Aurora Anywhere IPv4, IPv6 총 2개 추가
  💡 이 때 VPC 주소 RDS와 일치하도록 주의 <br>
  ➡️ RDS에 보안 그룹 추가 <br>

### ☑️ 파라미터 그룹

- time_zone 값: Asia/Seoul
- character 들어간 필드 6개 값: utf8mb4
- collation 들어간 필드 2개 값: utf8mb4_general_ci
  ➡️ RDS에 DB 파라미터 그룹 추가 <br>

## ✅ MySQl workbench

- Hostname: RDS의 엔드포인트
  예를 들어, `movie-database2.cn000owqib3s.ap-northeast-2.rds.amazonaws.com`
- Username: RDS에서 설정한 마스터 사용자 이름
- Password: RDS에서 설정한 비밀번호
  ➡️ TestConnection, connect anyway

### 🟢 Terminal 1: mariaDB설정

`ubuntu@ip-172-31-10-19:~/movie$` 이렇게 되어 명령어 입력 준비된 상태에서 시작
mariaDB 설치

```bash
sudo apt install wget

wget https://downloads.mariadb.com/MariaDB/mariadb_repo_setup

echo "f5ba8677ad888cf1562df647d3ee843c8c1529ed63a896bede79d01b2ecc3c1d mariadb_repo_setup" \
    | sha256sum -c -

chmod +x mariadb_repo_setup

sudo ./mariadb_repo_setup \
   --mariadb-server-version="mariadb-10.11"

sudo apt update
```

mariaDB client 설치

```bash
 sudo apt install mariadb-client
```

mysql 잘 있나 확인

```bash
mysql --version
```

mysql 들어가기

```bash
--  mysql -h RDS엔드포인트 -u DBusername -p
 mysql -h movie-database2.cn000owqib3s.ap-northeast-2.rds.amazonaws.com -u root -p
 show databases;
```

#### ✔️ 결과

```bash
MariaDB [(none)]> show databases;
+---------------------------+
| Database                  |
+---------------------------+
| Project_movie_reservation |
| information_schema        |
| innodb                    |
| mysql                     |
| performance_schema        |
| sys                       |
+---------------------------+
6 rows in set (0.001 sec)
```
