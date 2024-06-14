---
title: AWS EC2 HTTPS
categories: [AWS, Backend]
tags: [deploy] # TAG names should always be lowercase
---

## 💡 Things I learned

### ✔️ Shell

> 커널과 사용자 간의 다리 역할을 하는 인터페이스 <br>
> 사용자로부터 명령을 받아 실행하는 역할 <br>

### ✔️ SSH

> Secure SHell <br>
> 원격 컴퓨터에 접속하기 위해 사용되는 보안 프로그램 <br>
> 👍🏻 강력한 암호화 기능을 구현해 모든 데이터가 암호화되어 높은 보안을 지원한다는 장점

**암호화**를 해 줘서 보안상 안전하다는 장점 <br>
인증키, 키 페어(`.pem`)같은 것들이 바로 `SSH`라는 보안 방식이 적용된 서버에서 필요한 파일 <br>

#### 🔑 작동 원리: KEY

> SSH 작동원리의 가장 핵심은 바로 **KEY** <br>

<br>

✔️ **비대칭키 방식**
사용자와 서버가 서로의 정체를 증명(인증)하기 위해 **비대칭키**가 필요하다. <br>
비대칭키 키 페어 = 공개 키(`.pub`) + 개인 키(`.pem`) <br>
사용자가 키 페어를 만들어 서버에게 공개키를 주고, 개인 키는 자신이 가지고 있는다. <br>
서버는 공개키를 받아 <br>
한 값(시험지)를 생성한다. <br>
사용자는 서버로부터 시험지를 받아 자기가 가지고 있는 개인 키를 사용하여 이 시럼지를 푼다. <br>
키 페어는 하나의 세트이기 때문에, 공개키와 개인키가 같은 키페어야지만 이 시험지를 출 수 있다. <br>
서버는 사용자가 푼 시험지를 처음에 자신이 생성한 값과 비교하고, 두 값이 같으면 접속 허용! <br>
<br>

✔️ **대칭키 방식** <br>
이제 사용자와 서버가 서로가 누구인지 알았으니 정보 주고받음 <br>
정보를 주고받는 과정에서 정보가 새어나가지 않게 정보를 암호화 <br>
이 떄 사용되는 암호화 키가 바로 **대칭키 방식** <br>
서버와 사용자 모두 **한 개의 키**만을 사용하여 암호화 <br>

### ✔️ EC2

> Amazon Elastic Compute Cloud <br>
> AWS에서 원격으로 제어할 수 있는 가상의 컴퓨터를 빌리는 것(클라우드 컴퓨터) <br>
> 후불제로 사용한 만큼 비용을 지불하기에 Elastic <br>
> 또 원하는 만큼 성능, 용량을 자유롭게 설정할 수 있어 Elastic하기도 하다. <br>

### ✔️ AMI

> Amazon Machine Image <br>
> master image for the creation of vertual servers(known as EC2) <br>
> machine images are like templates with OS(linux, ubuntu), region, system architecture(32 or 64bit) that determine the user's operating environment <br>
> EC2 인스턴스를 생성하는 template <br>

<img width="332" alt="Screenshot 2024-06-13 at 12 01 15" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/31857496-fcfa-4774-a6fa-a086120fb2dc">

### ✔️ VPC

> Amazon Virtual Private Cloud <br>
> 가상 네트워킹 환경 <br>
> VPC에 EC2, RDS 인스턴스와 같은 리소스를 추가한다. <br>
> VPC를 사용함으로서 VPC별로 네트워크를 구성할 수 있고, VPC는 독립죈 네트워크처럼 작동 <br>
> 다른 VPC와 통신하기 위해서는 인터넷 게이트웨이 사용 <br>

💡 참고
<https://medium.com/harrythegreat/aws-%EA%B0%80%EC%9E%A5%EC%89%BD%EA%B2%8C-vpc-%EA%B0%9C%EB%85%90%EC%9E%A1%EA%B8%B0-71eef95a7098>

### ✔️ 서브넷

> VPC의 IP 주소 범위 <br>
> VPC를 또 잘게 쪼갠다. <br>
> 그래서 VPC보다 서브넷 마스크가 더 높게 되고, 아이피 번호는 더 작게 된다. <br>
> 서브넷을 만드는 이유는 더 많은 네트워크 망을 만들기 위해서. <br>
> 서브넷끼리는 라우터를 통해 통신 <br>

정리하자면, AWS > VPC > 서브넷 순이다. <br>
<img width="827" alt="Screenshot 2024-06-13 at 12 26 53" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/c9ee742b-e5ae-4768-9494-b24c2bc25284">

### ✔️ SSL인증서란?

> Secure Sockets Layer <br>
> 서버에 대한 인증, 데이터 암호화 기반 인터넷 **보안 프로토콜** <br>
> 사용 포트: HTTPS의 경우 HTTP를 위한 SSL/TLS 보안 터널 형성을 위해 443 포트 사용 <br>

<br>
SSL은 사용자와 웹 서버 사이를 이동하는 모든 데이터를 암호화해서 누가 가로채더라도 볼 수 없도록 한다. <br>
예를 들어, 쇼핑몰에서 신용카드 정보를 입력하면 SSL로 암호화되어 누군가가 정보를 가로채도 무작위 글자만 볼 수 있음. <br>
SSL은 두 통신 장치 사이에 핸드셰이크라는 인증 프로세스를 한다. <br>
<br>
그래서 SSL을 사용하면, SSL인증서가 있는 웹사이트만 실행할 수 있다.  <br>
SSL인증서는 신분증같은 역할을 해서 웹사이트 접속을 가능하게 한다.  <br>
SSL인증서에는 웹 사이트의 공개 키가 포함되어 있다.  <br>
그리고 웹 서버에는 개인 키가 있어 공개 키를 해독할 수 있음  <br>
CA는 SSL인증서 발급을 담당한다.  <br>

SSL인증서 관련 프로세스에는 다음과 같은 보안 기술이 탑재되어 있음<br>

- 하나의 키로 암호화/복호화를 하는 대칭 암호화 방식
- 한 쌍의 키 페어로 암호화/복호화를 하는 바대칭 암호화 방식
- authentication 신분 확인
- digital signature
- CA(certificate Authority)

#### 핸드셰이크

> 통신을 하려는 브라우저와 웹 서버가 서로 암호화 통신을 시작할 수 있도록 신분을 확인하고, 필요한 정보를 클라이언트와 서버가 주거니 받거니 하는 과정 <br>

💡 참고
<https://brunch.co.kr/@sangjinkang/38>
<https://aws-hyoh.tistory.com/39>

### ✔️ TLS

> Transport Layer Security<br>
> SSL보다 업데이트 된 암호화 프로토콜<br>

### ✔️ TCP 프로토콜

> Transmission Control Protocol <br>
> 인터넷 콘텐츠를 전달하는 프로토콜 <br>
> 두 개의 호스트를 연결하고 데이터 스트림 교환하게 해 줌 <br>
> HTTP는 TCP 프로토콜의 일종이다. <br>

### ✔️ FTP 프로토콜

> File Trasnfer Protocol<br>

### ✔️ SFTP 프로토콜

> SSH 파일 전송 프로토콜<br>
> 보안을 위해 사용되는 파일 전송 프로토콜<br>

<img width="768" alt="Screenshot 2024-06-14 at 12 53 04" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/3ceba9d4-f953-48ee-9381-a9d8e4b43476">

### ✔️ HTTP 🆚 HTTPS

> HTTPS: Hypertext Transfer Over SSL<br>
> SSL위에 HTTP 적용, 따라서 SSL을 적용한 도메인만이 `https://` 주소를 가질 수 있다.<br>

HTTP 포트번호는 일반적으로 80번을 사용한다면, HTTPS는 443이 할당되어 있다. <br>

### ✔️ HTTP ▶️ HTTPS 바꾸는 방법

### 🛠️ Let's Encrypt

> 무료로 TLS/SSL인증서를 쉽게 가져오고 설치할 수 있는 방법을 제공하는 CA(인증 기관) <br>
> 무료의 SSL인증서를 발급받아 웹 서버에서 암호화된 HTTPS를 사용할 수 있음 <br>
> Certbot라는 소프트웨어를 제공함으로써 구현할 수 있게 합니다. <br>
> 90일동안 사용가능하지만 간단한 명령어로 자동갱신 가능 <br>

#### ✔️ Let's Encrypt SSL 인증서 발급 방법

⭐️ **Nginx**

- 인증 및 설치를 위해 nginx 플러그인 사용 <br>

⭐️ **standalone**

- 웹 서버 동작을 멈추고 이 사이트의 네트워킹을 통해 사이트 유효성 확인 후 SSL인증서 발급 <br>
- 80포트로 가상 standalone 웹서버를 띄워 인증서 발급 <br>
- 동시에 여러 도메인 발급 가능 <br>
- 자동갱신 가능 <br>
  <br>

⭐️ **webroot**

- 사이트 디렉토리 내에 인증서 유효성을 확인할 수 있는 파일을 업로드하여 인증서 발급
- 서버 중단 없이 인증서 발급 가능
- 인증 명령에 하나의 도메인 인증서만 발급 가능
- 자동갱신 가능
  <br>

⭐️ **DNS**

- 도메인을 쿼리해 확인되는 TXT레코드로 사이트 유효성 확인
- 와일드 카드 방식
- 서버 관리자가 도메인 DNS를 관리, 수정할 수 있어야 함
- 인증서 갱신할 때마다 DNS에서 TXT값 변경 필요

## ✅ 가비아에서 도메인 구매하기

### ✔️ 구매하기

- 참고
  <https://velog.io/@b1rdn2w/%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%ED%98%91%EC%97%85-Spring-Boot-%EC%84%9C%EB%B2%84-%EA%B5%AC%EC%B6%95-3-AWS-EC2-HTTPS-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0>

## ✅ AWS Route 53

### ✔️ 호스팅 영역 생성

- 도메인 이름: 가비아에서 구매한 도메인 이름 입력

### ✔️ 레코드 세트 생성

- EC2 IP연결 **값**: EC2 Public IP값 입력

### ✔️ 네임서버 설정

가비아에서 네임서버 설정해야 함 <br>
NS유형의 레코드 4가지의 값(ns-000)을 등록한다. <br>
`.` 은 생략하고 등록 <br>

## ✅ SSL 인증서 발급 Let's Encrypt

### ✔️ SSH로 EC2인스턴스에 접속해 certbot설치

업데이트 <br>

```bash
sudo apt update
sudo apt upgrade
sudo add-apt-repository ppa:certbot/certbot
```

<img width="786" alt="Screenshot 2024-06-11 at 13 33 09" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/49c496bb-9074-4da7-ab12-c0a08b4b0770">

### ✔️ Certbot의 Nginx 패키지 설치

```bash
sudo apt install -y certbot python3-certbot-nginx
```

<img width="772" alt="Screenshot 2024-06-11 at 13 34 02" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/82e3a2b8-98c2-42cd-9235-5790717e393b">

### ✔️ Nginx Configuration 설정 (🔺 건너뛰기)

server_name을 구매한 도메인 이름으로 바꿔준다.

```bash
sudo vim /etc/nginx/sites-available/default
```

<img width="532" alt="Screenshot 2024-06-11 at 13 34 47" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/c9c444bd-3c21-47f6-850b-42cbcf3d26fa">

도메인 이름으로 바꾼 뒤 잘 되는지 테스트

```bash
sudo nginx -t
```

### ✔️ Nginx reload (🔺 건너뛰기)

```bash
sudo systemctl reload nginx
```

### ✔️ HTTPS에 대한 방화벽 허용 설정

AWS EC2인스턴스는 기본적으로 방화벽이 비활성화되어 있다고 한다.

```bash
sudo ufw status
```

<img width="400" alt="Screenshot 2024-06-11 at 13 36 09" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/b825e189-7caf-45d4-95e2-47fcafbbcbc9">

### ✔️ SSL 인증서 받기

원하는 도메인을 지정해서 Nginx 플러그인으로 인증서 획득

```bash
sudo certbot --nginx -d 도메인
이메일 입력
## Let's Encrypt 이메일에 추가되고 싶은지 아닌지 선택
## 기존 HTTP 연결 요청을 HTTPS로 자동으로 바꿔줄 것인지 선택
```

`certbot`: 인증서를 다운받고 설치하는 명령어 <br>
`--nginx`: 해당 도메인에 대한 소유주가 자신임을 인증하기 위해 이용할 플러그인 <br>
도메인 관리자의 이메일 주소를 입력하라고 함(만료일에 대한 정보 메일로 전송해 줌) <br>
약관에 대한 동의 (A)/(C) 를 묻는데 동의에 선택하는 (A) <br>

<img width="590" alt="Screenshot 2024-06-11 at 13 36 33" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/aaf3d176-40cc-429d-9c53-86a444f6fed8">

### ✔️ key 잘 발급되었는지 확인

4개의 .pem, 1개의 readme가 생성되었는지 확인 <br>
이 파일들은 `/etc/letsencrypt/live/[도메인주소]`에 대한 심볼릭 링크이다. <br>

```bash
## ll /etc/letsencrypt/live/ 내 도메인
ls -al /etc/letsencrypt/live/drugstoreproject.shop
```

<img width="685" alt="Screenshot 2024-06-13 at 21 20 00" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/d5bc56d8-095b-4212-bb25-d4864427f5c1">

### ✔️ 도메인 서버 테스트

도메인을 입력하고 submit <br>
<https://www.ssllabs.com/ssltest/> <br>

<img width="1094" alt="Screenshot 2024-06-12 at 00 19 34" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/a2db97bc-d15e-4f05-8b09-f99366b93e88">
<img width="1025" alt="Screenshot 2024-06-12 at 00 21 10" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/b5b9a9ab-23fe-4a69-9edd-6e7e744e5623">

#### ➡️ Nginx 설정으로 가기

### ✔️ Certbot 자동갱신

- Let's Encrypt의 인증서는 90일동안만 유효해서 90일마다 갱신해주어야 한다. <br>
- 설치하는 과정에서 `/etc/cron.d` 에 자동으로 갱신시켜주는 명령어가 추가되어 있었다! <br>
- 갱신 프로세스가 잘 동작하는지 확인하기 위해 다음과 같은 명령어를 입력하고, 오류가 나지 않으면 잘 동작하는 것 <br>

```bash
sudo certbot renew --dry-run
```

<img width="511" alt="Screenshot 2024-06-11 at 13 36 43" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/a96ae358-9ec7-48f9-bb2f-3f6e3e283e33">

### ✔️ 이제 발급이 완료되었으므로 `/etc/letsencrypt/live/도메인` 경로에 `fullchain.pem` , `privkey.pem `이 발급되었을 것이다. (🔺 건너뛰기)

- 새로 터미널 탭 열고
- root계정으로 해당 경로로 이동
  🔴 바로 `cd /etc/letsencrypt/live/도메인`으로 실행하니 동작하지 않았다! <br>
  이유: `/etc/` is usually restricted, needs elevated permissions. <br>
  To get elevated permissions, use `sudo` <br>
  However, `cd` with `sudo` might not work bc `cd` is a shell-built-in command. <br>
  To solve, open a shell with `sudo` and then navigate. <br>

```bash
sudo -s
cd /etc/letsencrypt/live/drugstoreproject.shop/
```

### ✔️ pem을 PKCS12형식으로 변경 (🔺 건너뛰기)

- `.pem`은 스프링부트에서 인식을 못한다.
- 따라서 PKCS12형식으로 변경해주어야 한다.
- 변경할 때 비밀번호를 설정해야 하는데 이 비밀번호 꼭 기억할 것(나중에 yaml파일에 설정함)
- 결과물: keystore.p12
- 변경 후 나가려면 `exit`치면 된다.

```bash
sudo openssl pkcs12 -export -in fullchain.pem -inkey privkey.pem -out keystore.p12 -name ttp -CAfile chain.pem -caname root
```

<img width="1144" alt="Screenshot 2024-06-11 at 18 17 38" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/e052b1a6-7e9d-4a72-90e6-7c7c0f3bfd91">
<img width="664" alt="Screenshot 2024-06-11 at 18 20 29" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/2a2d8b27-6a07-4e08-b88e-27e4e61f2e71">

### ✔️ 모든 HTTPS설정 끝! Nginx 서버 restart (🔺 건너뛰기)

```bash
sudo service nginx restart
```

## ✅ FileZilla (🔺 건너뛰기)

FileZilla에서 `keystore.p12` 파일 로컬로 가져오기 <br>

### ✔️ FileZilla에 새로운 사이트 추가

- FileZilla Client 설치
  > 프로토콜: SFTP <br>
  > 호스트: AWS EC2 퍼블릭 IPv4 <br>
  > 사용자: ubuntu <br>
  > 로그온 유형: 키 파일 <br>
  > 키 파일(pem이 존재하는 경로) <br>

<img width="1056" alt="Screenshot 2024-06-11 at 19 27 45" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/b384efa0-137d-4891-9823-a951bb4b4f77">

### 🔴 FileZilla에서 `keystore.p12`이 있는 경로 `/etc/letsencrypt/live/도메인`로 들어가려고 하는데 계속 실패

권한이 없다고 떴다. <br>
결국 `keystore.p12`를 `home/ububtu`로 옮겨 거기서 로컬로 받아옴 <br>
로컬 원하는 장소에 저장 후 이후에 SpringBoot에 추가 <br>
<img width="619" alt="Screenshot 2024-06-11 at 19 22 46" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/aa413899-3d91-4b13-ac35-523743c7ffee">

### ✔️ 여기까지 과정 총정리

<img width="681" alt="Screenshot 2024-06-11 at 19 24 23" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/72967aca-8ce5-4950-b645-8635c35d5270">

## ✅ SpringBoot Setting (🔺 건너뛰기)

### ✔️ Resources에 SSL인증서 파일 넣기

<img width="286" alt="Screenshot 2024-06-12 at 00 49 47" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/d2b549a6-6a67-4005-86dc-7b3ffbf6a88e">

### ✔️ yaml 파일에 설정 추가

```yaml
server:
  ssl:
    key-store: classpath:keystore.p12
    key-store-type: "PKCS12"
    key-store-password: ENC(i5PeoNKddffOFHGj/baHbHVAsek6cRQK) //PKCS12변경할 때 사용한 비밀번호
```

<img width="485" alt="Screenshot 2024-06-12 at 00 50 25" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/9a1a0393-d6cb-462f-9f56-ab69f39045ca">

## 🔴 도메인 연결이 안 됨

여기까지 따라했으나 `http://drugstoreproject.shop:8080/swagger-ui/index.html` 쳐도 스웨거 화면이 404로 뜸 <br>

### 🔵 `nginx config`를 수정하였다.

1. Open Nginx Configuration

```bash
sudo nano /etc/nginx/sites-available/drugstoreproject.shop
```

2. Update config

<img width="706" alt="Screenshot 2024-06-13 at 01 10 20" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/4b120df4-34e4-4365-b09f-ff55d3bc396e">

3. Check syntax error in Nginx Configuration

```bash
sudo nginx -t
```

4. Reload nginx

```bash
sudo systemctl reload nginx
```

그랬더니 스웨거 화면은 잘 나오게 되었음! <br>
<img width="1129" alt="image" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/a193cd33-45cf-4a4b-b319-54c76a534914">

그러나 아직도 `https://`는 되지를 않는다ㅠㅠ

## 🔴 https 해결

`https://`로 도메인을 연결하면 이런 화면이 뜸 <br>
<img width="1130" alt="image" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/50f4951f-2aab-4390-a2c0-891f1086973a">

그리고 `https://drugstoreproject.shop:8080/swagger-ui/index.html`는 `ERR_SSL_PROTOCOL_ERROR`이 뜬다. <br>

<img width="1018" alt="image" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/a52670dd-c0ba-4e53-a0ab-94d5d24e3296">

## ✅ Nginx conf 설정

### ✔️ Nginx의 nginx.conf, sites-available, sites-enabled

- /ets/nginx/nginx.conf <br>
  Nginx 설정에 관한 블록 작성 <br>
  이 파일에서 `sites-enabled`폴더에 있는 파일들을 include하여 가져온다. <br>
  <br>

- /ets/nginx/sites-available <br>
  **가상 서버 환경**에 대한 설정 파딜들이 위치한 디렉토리 <br>
  <br>
- /ets/nginx/sites-enabled <br>
  `sites-available`에 있는 가상 서버 파일들 중에서 실행시키고 싶은 파일을 symbolic link로 연결한 폴더 <br>
  이 폴더에 위치한 가상서버 환경 파일들을 읽어 실제 서버를 세팅함! <br>

### 💡 결론

> 우리는 `/ets/nginx/sites-available`아래 새로운 `drugstoreproject.shop`이라는 파일을 만들고, <br> > `sites-enabled`폴더에 심볼릭 링크를 만들어 `sites-enabled`가 `drugstoreproject.shop`을 가리키도록 할 것이다!<br>

### ➕ symbolic link

> 링크를 연결해 원본 파일을 직접 사용하는 것과 같은 효과를 내는 링크 <br>
> 폴더 바로가기 같은 개념 <br>
> 특정 폴더에 링크를 걸어 원본파일을 사용하기 위해 쓴다. <br>

### ✔️ nginx.conf

`nginx.conf`을 열어보면 <br>

```bash
cd /etc/nginx
vi nginx.conf
```

<img width="251" alt="Screenshot 2024-06-13 at 23 21 50" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/38e38f49-96f8-43bd-bd9c-989dce79f5bd">
가장 아래에 이런 설정이 있어야 한다. <br> 
1. /etc/nginx/conf.d 아래에 있는 모든 .conf 파일들을 inclue한다.<br> 
2. /etc/nginx/sites-enabled의 모든 파일들을 include한다.<br>

## ✅ Nginx 설정

1. sites-available 설정(Create and configure a New Site Configuration) <br>

```bash
sudo nano /etc/nginx/sites-available/drugstoreproject.shop
```

2. 다음과 같이 입력
   저장 `command + O`
   나가기 `command + X`

```bash
server {
    listen 80;
    server_name drugstoreproject.shop www.drugstoreproject.shop;
    return 301 https://drugstoreproject.shop$request_uri;
}

server {
    listen 443 ssl http2;
    server_name drugstoreproject.shop www.drugstoreproject.shop;

    ssl_certificate /etc/letsencrypt/live/drugstoreproject.shop/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/drugstoreproject.shop/privkey.pem;

    location / {
        proxy_pass http://localhost:8080;
        proxy_set_header Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}

server {
   if ($host = drugstoreproject.shop) {
        return 301 https://$host$request_uri;
   }
   listen 80;
   server_name drugstoreproject.shop;
        return 404;
}
```

(1) 80포트로 들어오는 요청, 즉 `http`로 들어오는 요청을 `https`로 **리다이렉션**을 한다.<br>
<br>

(2) `https://`로 들어오는 요청을 **서비스 중인 포트로 연결**한다.<br>
<br>

- `proxy_pass`: 프록시 주소, 백엔드 운영 서버 ip <br>
  🔴 두 번째 server 블록 `proxy_pass`는 ` http://localhost:8080;`이다. <br>
  `http` ⭕️ `https` ❌ <br>
  8080포트에서는 spring boot앱이 실행되고 있는 상태 <br>
- `proxy_set_header Host $http_host;`: HTTP request의 Host 헤더 값, 클라이언트가 요청한 원래 호스트 주소 <br>
- `X-Real-IP`: 실제 방문자의 원격 IP주소 <br>
- `X-Forwarded-For`: 클라이언트가 프록시 처리한 모든 서버의 IP주소를 포함하는 목록 <br>
- `X-Forwarded-Proto`: HTTP구조로 http 또는 https를 의미 <br>
  <br>
  (3) 도메인 이름이 다르면 404에러 처리<br>
  <br>

3. Enable the new site<br>
   `create a symbolic link`해서 `sites-enabled`로 연결<br>
   우리가 만든 config파일을 `sites-enabled` 디렉토리에 링크해준다.<br>

```bash
sudo ln -s /etc/nginx/sites-available/drugstoreproject.shop /etc/nginx/sites-enabled/
```

잘 만들어졌는지 확인하고 싶으면 <br>

```bash
cd /etc/nginx/sites-enabled
ls -l

```

4. default site를 삭제한다.<br>
   그래서 아까 `sites-available/default`는 건너뛰라고 한거다...<br>

```bash
sudo rm /etc/nginx/sites-enabled/default
```

5. Config에 syntax error 없는지 확인<br>

```bash
sudo nginx -t
```

6. reload nginx<br>

```bash
sudo systemctl reload nginx
```

## ✅ Error Log 보기

1. `Error Log`있는 디렉토리로 가기<br>

```bash
cd /var/log/nginx
```

`ls`해보면 `error.log`있을 것이다. 2. View `error.log` content<br>

```bash
cat error.log
```

## 🔴 여기까지 했더니 502에러

그래도 `https://drugstoreproject.shop/`는 잘 되었는데, Nginx Config설정을 하고 오니 502 에러가 떴다. <br>

에러 로그를 찍어 보니 이렇게 나왔다. <br>
<img width="1090" alt="Screenshot 2024-06-13 at 22 14 12" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/4c5c52b3-344d-424c-b11c-533501207742">

🔵 이 에러는 config파일 문제 때문에 생긴다. <br>
nginx config에서 443으로 들어온 요청은 `http`로 우리 서비스와 연결을 시켜줘야 한다. <br>
그래서 두 번째 server 블록 `proxy_pass`를 `https`가 아닌 `http`로 고쳐주니 잘 실행되었다. <br>
` http://localhost:8080;`이렇게 바꾸기 <br>

## ⭐️ 성공한 모습

<img width="590" alt="Screenshot 2024-06-13 at 23 36 15" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/229cbc40-41e9-4b5a-859a-858adf10f7bf">

<img width="606" alt="Screenshot 2024-06-13 at 23 35 36" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/71e6515f-d862-48b1-995b-a04d718c5028">

<img width="1173" alt="image" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/63afa05b-d9a8-4769-8feb-b6b0cc3eccb9">

## 💡 참고

- AWS EC2, 가비아, nginx, Certbot, FileZilla(이걸로 따라할 것)
  <https://un-lazy-midnight.tistory.com/172>

- 도메인 연결하는 방법
  <https://olrlobt.tistory.com/89>

- Nginx Config 설정하는 방법
  <https://velog.io/@coastby/Nginx-SSL-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0>

- Filezilla: 파일질라로 파일 업로드/다운로드 하기
  <https://velog.io/@ky0_hw/AWS-ec2-Filezilla%ED%8C%8C%EC%9D%BC%EC%A7%88%EB%9D%BC%EB%A1%9C-%ED%8C%8C%EC%9D%BC-%EC%97%85%EB%A1%9C%EB%93%9C%EB%8B%A4%EC%9A%B4%EB%A1%9C%EB%93%9C%ED%95%98%EA%B8%B0>

재고처리를 장바구니, 주문할 때 모두 해야 한다.
TTL을 사용하면 장바구니에 담은 후 10분 지나면 사라지도록
https://offbyone.tistory.com/303

https://mangkyu.tistory.com/174

https://medium.com/naver-cloud-platform/기술-컨텐츠-문자-알림-발송-서비스-sens의-mapstruct-적용기-8fd2bc2bc33b

https://hudi.blog/effective-java-static-factory-method/

https://techblog.woowahan.com/2553/

이미지 파일이 클 때 올라가지 않는 문제
nginx conf 에 설정해주어야함
ttl
method static으로 리팩토링
JPA repository로 이름 바꾸기
