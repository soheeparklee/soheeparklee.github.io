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

- 인바운드 규칙에 모든 MYSQL/Aurora Anywhere IPv4, IPv6 총 2개 추가 <br>
  💡 이 때 VPC 주소 RDS와 일치하도록 주의 <br>
  ➡️ RDS에 보안 그룹 추가 <br>

### ☑️ 파라미터 그룹

- time_zone 값: Asia/Seoul
- character 들어간 필드 6개 값: utf8mb4
- collation 들어간 필드 2개 값: utf8mb4_general_ci <br>
  ➡️ RDS에 DB 파라미터 그룹 추가 <br>

## ✅ MySQl workbench

- Hostname: RDS의 엔드포인트 <br>
  예를 들어, `movie-database2.cn000owqib3s.ap-northeast-2.rds.amazonaws.com`
- Username: RDS에서 설정한 마스터 사용자 이름
- Password: RDS에서 설정한 비밀번호 <br>
  ➡️ TestConnection, connect anyway

### 🟢 Terminal 1: mariaDB설정

`ubuntu@ip-172-31-10-19:~/movie$` 이렇게 되어 명령어 입력 준비된 상태에서 시작 <br>
mariaDB 설치 <br>

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

## ✅ yaml files

#### ✔️ application.yaml

```yaml
server: port:8080

spring:
  mvc:
    pathmatch:
      matching-strategy: ant_path_matcher

  #  autoconfigure:
  #    exclude: org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration

  datasource:
    username: ${DATABASE_USERNAME}
    password: ${DATABASE_PASSWORD}
    driver-class-name: org.mariadb.jdbc.Driver
    url: jdbc:mariadb://movie-database2.cn000owqib3s.ap-northeast-2.rds.amazonaws.com:3306/Project_movie_reservation?useUnicode=true&characterEncoding=UTF-8

  jpa:
    show-sql: true

jwtpassword:
  source: ${JWT_SECRET_KEY}

  logging:
    level: debug
```

#### ✔️ application-prod.yaml

```yaml
spring:
  config:
    activate:
      on-profile: prod

logging:
  config: classpath:logback-spring-prod.xml

datasource:
  driver-class-name: org.mariadb.jdbc.Driver
  url: jdbc:mariadb://movie-database2.cn000owqib3s.ap-northeast-2.rds.amazonaws.com:3306/Project_movie_reservation?useUnicode=true&characterEncoding=UTF-8
```

#### ✔️ application-dev.yaml

```yaml
spring:
  config:
    activate:
      on-profile: dev

server:
  port: 8080

logging:
  config: classpath:logback-spring-local.xml
  level:
    org:
      hibernate:
        SQL: DEBUG
```

#### ✔️ application-local.yaml

```yaml
spring:
  config:
    activate:
      on-profile: local

server:
  port: 8080

logging:
  config: classpath:logback-spring-local.xml
  level:
    org:
      hibernate:
        SQL: DEBUG
```

## ✅ xml log files

#### ✔️ logback-spring-prod.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <property name="LOG_PATH" value="logs" />

    <!-- 콘솔 로그 출력 -->
    <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %highlight(%-5level) %cyan(%logger{36}) - %msg%n</pattern>
        </encoder>
    </appender>

    <appender name="FILE" class="ch.qos.logback.core.FileAppender">
        <file>${LOG_PATH}/server.log</file>
        <append>true</append>
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %highlight(%-5level) %cyan(%logger{36}) - %msg%n</pattern>
        </encoder>
    </appender>

    <!-- 루트 로거 설정 -->
    <root level="info">
        <appender-ref ref="CONSOLE" />
        <appender-ref ref="FILE" />
    </root>
</configuration>
```

#### ✔️ logback-spring-dev.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <property name="LOG_PATH" value="logs" />

    <!-- 콘솔 로그 출력 -->
    <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %highlight(%-5level) %cyan(%logger{36}) - %msg%n</pattern>
        </encoder>
    </appender>

    <appender name="FILE" class="ch.qos.logback.core.FileAppender">
        <file>${LOG_PATH}/server.log</file>
        <append>true</append>
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %highlight(%-5level) %cyan(%logger{36}) - %msg%n</pattern>
        </encoder>
    </appender>

    <!-- 루트 로거 설정 -->
    <root level="info">
        <appender-ref ref="CONSOLE" />
        <appender-ref ref="FILE" />
    </root>
</configuration>
```

#### ✔️ logback-spring-local.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <!-- 콘솔 로그 출력 -->
    <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %highlight(%-5level) %cyan(%logger{36}) - %msg%n</pattern>
        </encoder>
    </appender>

    <!-- 루트 로거 설정 -->
    <root level="info">
        <appender-ref ref="CONSOLE" />
    </root>
</configuration>
```

## ✅ ubuntu에 환경변수 저장하기

일단 서버로 들어가기 . 들어가서 시작

```bash
~/Desktop
~/Downloads
cd movie-key
 ssh -i "movie-reservation.pem" ubuntu@ec2-54-180-126-207.ap-northeast-2.compute.amazonaws.com
```

환경변수 설정 위해 들어감 <br>

```bash
vim ~/.bashrc
```

안에서 편집 시작 <br>
s누르면 편집 가능 <br>
💡 =사이에 띄어쓰기 하지 않기 주의! <br>
💡 다 편집 후 ESC 누르면 편집 모드에서 read only 모드로 바뀜 <br>
그제서야 `:wq` 눌러서 저장하고 quit <br>

```bash
#add environment variables
export DATABASE_PASSWORD=비밀번호
export DATABASE_USERNAME=root
export JWT_SECRET_KEY=시크릿키
```

vim에서 나왔으면 확인

```bash
-- 저장
source ~/.bashrc
-- 하나씩 불러와서 잘 저장되었는지 확인할 것
echo $JWT_SECRET_KEY
echo $DATABASE_USERNAME
echo $DATABASE_PASSWORD
```

## ✅ git clone, deploy

ubuntu > movie folder > github project clone<br>

```bash
-- git clone -b 복사할브랜치이름  --single-branch 깃허브 링크
git clone -b deploy --single-branch https://github.com/sc-project2-MovieReservation/MovieReservation-BE.git
```

#### ✔️ 결과

ubuntu > movie안에 깃허브 프로젝트가 만들어진다. <br>
`ubuntu@ip-172-31-10-19:~/movie/MovieReservation-BE$`<br>

## ✅ build file만들기

`ubuntu@ip-172-31-10-19:~/movie/MovieReservation-BE$` 하고 `ls`해보면 build파일이 없음. <br>
build파일 만들어야 한다. <br>

```bash
-- build file 만드는 명령어
./gradlew bootJar
```

그럼 이제 `ubuntu@ip-172-31-10-19:~/movie/MovieReservation-BE$` 하고 `ls`해보면 build파일이 만들어져 있는걸 확인할 수 있다. <br>

<img width="495" alt="image" src="https://github.com/sc-project2-MovieReservation/MovieReservation-BE/assets/97790983/1e08516f-3c23-4093-b2a3-714445ad0d02">

이제 build파일 안에 있는 libs파일에 들어가면 SNAPSHOT.jar 파일이 생긴걸 확인할 수 있다. <br>
이렇게 생겼음: `MovieReservation-BE-0.0.1-SNAPSHOT.jar`<br>

```bash
ls ./build/libs
```

#### ✔️ 결과

<img width="488" alt="image" src="https://github.com/sc-project2-MovieReservation/MovieReservation-BE/assets/97790983/a415cff4-6b41-4049-95f9-c3ff3437372b">

## ✅ deploy, swagger

게속 `ubuntu@ip-172-31-10-19:~/movie/MovieReservation-BE$`에서 이어서 진행
이제 SNAPSHOT.jar 파일을 배포하면, 어떤 컴퓨터에서도 웹페이지 접속 가능<br>
💡 띄어쓰기 주의하기!<br>

- Jar띄고 `-jar ./ `<br>
  💡 `./build/libs/MovieReservation-BE-0.0.1-SNAPSHOT.jar` 주의 <br>

```bash
java -jar ./build/libs/MovieReservation-BE-0.0.1-SNAPSHOT.jar --spring.profiles.active=prod
```

#### ✔️ 결과

http://`EC2퍼블릭 IPv4 DNS 여기에 쓰기`:8080/swagger-ui/index.html <br>
예를 들어, 아래 주소를 넣으면<br>
`http://ec2-3-249-108-216.eu-west-1.compute.amazonaws.com:8080/swagger-ui/index.html` <br>
이렇게 하면 우리가 만든 백엔드 단이 swagger에 보이게 된다.

#### ✔️ 결과

마찬가지로 포스트맨도 가능하다. <br>
localhost를 `EC2퍼블릭 IPv4 DNS`로 바꾸기<br>
<img width="1034" alt="image" src="https://github.com/sc-project2-MovieReservation/MovieReservation-BE/assets/97790983/a09d17b5-95e0-422c-9d16-45828dcc690e">

#### 🔴 Trouble Shooting

`java -jar ./MovieReservation-BE/build/libs/MovieReservation-BE-0.0.1-SNAPSHOT.jar --spring.profiles.active=prod`을 하고 application start가 뜨기를 기다렸다. <br>
하지만 계속계속 기다리는데 WARN에 멈추더니 터미널이 꿈쩍도 안했다. <br>
심지어 run을 멈추는 방법도 모르겠어서 터미널을 꺼버렸다. <br>
그리고 다시 터미널을 열어 처음부터 시작했다. <br>
그런데 이번에는 ` ssh -i "movie-reservation.pem" ubuntu@ec2-54-180-126-207.ap-northeast-2.compute.amazonaws.com` 도 들어가지지가 않았다. <br>
내 ubuntuㅠㅠ 뭐가 문제일까?? <br>

🟡 원인: 컴퓨터 CPU과부화일 수도 있다고 한다. 또는 EC2의 문제일 수도 있다. <br>
🔵 우선 컴퓨터에서 실행되는 프로세스들을 멈추고, 컴퓨터 전원을 껐다가 켰다. 하지만 이걸로 해결이 되지 않았다. <br>
🔵 그래서 이번에는 EC2를 중지했다가, 다시 시작했다. 물론 이렇게 하면 퍼블릭 도메인이 바뀐다. 바뀐 도메인 주소로 다시 우분투에 접속한다. <br>
`ssh -i "movie-reservation.pem" ubuntu@ec2-43-200-67-116.ap-northeast-2.compute.amazonaws.com`<br>
이렇게 했더니 잘 접속이 되었고, 이어서 `java -jar` 까지도 잘 실행되었다. 끝!<br>

## ✅ terminal꺼져도 끝나지 않는 서버, nohub

지금은 terminal을 꺼버리면 서버도 꺼진다. <br>
따라서 백그라운드에서 저쪽 서버에서 영원히 돌도록 만들기. <br>

`ubuntu@ip-172-31-10-19:~/movie$` 까지 들어온 상태에서 진행<br>

💡 띄어쓰기 주의하기!<br>

- Jar띄고 `-jar ./ `<br>
- /dev 띄어쓰기 없음 `>>/dev/null` <br>
  💡 `./MovieReservation-BE/build/libs/MovieReservation-BE-0.0.1-SNAPSHOT.jar` 주의 <br>

```bash
nohup java -jar ./MovieReservation-BE/build/libs/MovieReservation-BE-0.0.1-SNAPSHOT.jar --spring.profiles.active=prod >>/dev/null 2>&1 &
```

#### ✔️ 결과

4자리 숫자가 출력되어야 한다. <br>
그리고 네트워크 상태 확인하면 새로운 tcp 있음<br>
이제 터미널을 꺼도 잘 실행된다. <br>

```bash
netstat -ltpn
```

<img width="994" alt="image" src="https://github.com/sc-project2-MovieReservation/MovieReservation-BE/assets/97790983/332e6613-44ae-4d6e-b913-cca78cbf83b4">

## ✅ IP고정하기

AWS EC2를 중지했다가 다시 시작하게 되면 `EC2퍼블릭 IPv4 DNS`가 바뀐다. <br>
따라서 바뀌지 않는 탄력적 IP를 지정한다. <br>

EC2에 탄력적 IP <br>

- 탄력적 IP 주소 할당 <br>
- 만든 탄력적 IP에 주소 연결, 우리가 만든 instance연결<br>
  이후 인스턴스에 들어가면 `탄력적 IP 주소`라는게 생김<br>
  이제 `EC2퍼블릭 IPv4 DNS`대신에 `탄력적 IP 주소`를 넣는다. <br>

```
-- 이전
ssh -i "movie-reservation.pem" ubuntu@ec2-43-200-67-116.ap-northeast-2.compute.amazonaws.com
http://ec2-43-203-126-199.ap-northeast-2.compute.amazonaws.com:8080/auth/sign-up
-- IP고정 이후
ssh -i "movie-reservation.pem" ubuntu@43.200.67.116
http://43.200.67.116:8080/auth/login
```

#### ✔️ 결과

swagger주소 이제 이렇게 생김<br>
`http://43.200.67.116:8080/swagger-ui/index.html` <br>

## ✅ 진짜 마지막으로 IP주소 백그다운드에서 run

```bash
~/Desktop
~/Downloads
cd movie-key
ssh -i "movie-reservation.pem" ubuntu@43.200.67.116
```

그러면 `ubuntu@ip-172-31-10-19:~/$` <br>
이후 `ubuntu@ip-172-31-10-19:~/movie/$` 까지 들어와서 <br>

```bash
nohup java -jar ./MovieReservation-BE/build/libs/MovieReservation-BE-0.0.1-SNAPSHOT.jar --spring.profiles.active=prod >>/dev/null 2>&1 &
```

<img width="663" alt="image" src="https://github.com/sc-project2-MovieReservation/MovieReservation-BE/assets/97790983/6e9189de-a995-4ee0-aaf1-fb128bff91a1">

<img width="769" alt="image" src="https://github.com/sc-project2-MovieReservation/MovieReservation-BE/assets/97790983/74f4e12d-7869-4597-845f-60a08745500c">

## 💡 개선 포인트

- bash script <br>
  여러번 반복되는 bash 명령어는 bash script 만들어 활용하기<br>
- github action CI/CD<br>
  여러 툴 사용하여 빌드/배포 자동화 가능<br>

## ✅ CORS

### ☑️ kill server

Identify the Process ID (PID) of the Server Process <br>

```bash
sudo netstat -tulpn | grep :8080
```

<img width="556" alt="Screenshot 2024-05-01 at 14 33 28" src="https://github.com/sc-project2-MovieReservation/MovieReservation-BE/assets/97790983/bf521e93-9933-4c8c-be0d-a86295e5bf69">

Stop the Server Process

```bash
sudo kill PID
```

이제 다시 `sudo netstat -tulpn | grep :8080`하면 아무것도 안 뜬다.

### ☑️ erase git cloned file

현재 ubuntu@, movie 안에 깃허브 클론 폴더 만들어져 있는 상태

```bash
ubuntu@ip-172-31-10-19:~/movie$ ls
MovieReservation-BE  logs  mariadb_repo_setup  mariadb_repo_setup.1  mariadb_repo_setup.2  nohup.out
-- MovieReservation-BE가 깃허브 클론한 것
```

깃 클론 지우기

```bash
 sudo rm -r MovieReservation-BE
```

### ☑️ security config에 cors관련 세팅 추가

```java
import github.com.jbabe.service.exception.CustomAuthenticationEntryPoint;
import github.com.jbabe.service.exception.CustomExceptionDeniedHandler;
import github.com.jbabe.web.filters.JwtFilter;
import lombok.RequiredArgsConstructor;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.authentication.AuthenticationManager;
import org.springframework.security.config.annotation.authentication.configuration.AuthenticationConfiguration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.http.SessionCreationPolicy;
import org.springframework.security.web.SecurityFilterChain;
import org.springframework.security.web.authentication.UsernamePasswordAuthenticationFilter;
import org.springframework.web.cors.CorsConfiguration;
import org.springframework.web.cors.CorsConfigurationSource;
import org.springframework.web.cors.UrlBasedCorsConfigurationSource;

import java.util.List;

@Configuration
@EnableWebSecurity
@RequiredArgsConstructor
public class SecurityConfig {
    private final JwtTokenConfig jwtTokenConfig;
//    private final JwtExceptionFilter jwtExceptionFilter;
    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
                .headers(h -> h.frameOptions(f -> f.sameOrigin()))
                .csrf((c) -> c.disable())
                .httpBasic((h) -> h.disable())
                .formLogin(f -> f.disable())
                .rememberMe(r -> r.disable())
                .sessionManagement(s -> s.sessionCreationPolicy(SessionCreationPolicy.STATELESS))
                .cors(c-> c.configurationSource(corsConfig())) //add
                .authorizeRequests(a ->
                        a
                                .requestMatchers("/test","v1/api/competition/add-competition-info").hasRole("MASTER")
                                .requestMatchers("/v1/api/sign/logout").authenticated()
                                .requestMatchers("/resource/static/**", "/v1/api/sign/sign-up", "/v1/api/sign/login",
                                        "/mail/*", "v1/api/competition/competition").permitAll()
                )
                .exceptionHandling(e -> {
                    e.authenticationEntryPoint(new CustomAuthenticationEntryPoint());
                    e.accessDeniedHandler(new CustomExceptionDeniedHandler());
                })
                .addFilterBefore(new JwtFilter(jwtTokenConfig), UsernamePasswordAuthenticationFilter.class);
//                .addFilterBefore(jwtExceptionFilter, JwtFilter.class);
        return http.build();

    }

    private CorsConfigurationSource corsConfig() {
        CorsConfiguration corsConfiguration = new CorsConfiguration();
        corsConfiguration.setAllowedOrigins(List.of("*")); // TODO: 쿠키사용 시 변경
//        corsConfiguration.setAllowCredentials(true); // TODO: 쿠키사용 시 변경
        corsConfiguration.addExposedHeader("access-token");
        corsConfiguration.addExposedHeader("refresh-token");
        corsConfiguration.addAllowedHeader("*");
        corsConfiguration.setAllowedMethods(List.of("GET","PUT","POST","PATCH","DELETE","OPTIONS"));
        corsConfiguration.setMaxAge(1000L*60*60);
        UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource();
        source.registerCorsConfiguration("/**",corsConfiguration);
        return source;
    }


    @Bean
    public AuthenticationManager authenticationManager(AuthenticationConfiguration authenticationConfiguration) throws Exception {
        return authenticationConfiguration.getAuthenticationManager();
    }
}

```

### ☑️그리고 git commit, push 한다음 또 deploy
