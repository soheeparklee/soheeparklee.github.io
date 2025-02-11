---
title: CICD with Github Actions for project Deving
categories: [Deploy, CICD]
tags: [cicd] # TAG names should always be lowercase
---

## ✅ CICD settings

- `nohup`해서 실행했을 때 잘 실행되는 상태
- `.github`안에 `workflows`라는 파일 만들고
- 이 안에 `cd.yml` 파일 생성

<img width="294" alt="Image" src="https://github.com/user-attachments/assets/1d187fb7-5a34-4d03-9a14-a8214f84babc" />

- `test controller`도 하나 있으면 변경되는 내용 확인하기에 좋음

```java
@Slf4j
@RestController
public class TestController {
    @GetMapping("/test")
    public String hello() {
        return "/CICD test 페이지입니다";
    }
}

```

## 🔴 /login redirect error

- `spring security`를 `build`파일에 넣고 배포를 했더니
- `/test`로 보내도 로그인이 안 되어 있다면서 `spring security`가 `/login`으로 redirect해버림
- 아직 로그인, 회원가입 등 구현하기 전 단계이므로
- `security config`파일을 `spring security`를 사용하지 않도록 임시로 `permitAll`로 바꿔둔다.
- ❗️ 나중에 로그인, 회원가입 등 **인증 구현 후에는 원래대로 바꿔야!!**

```java
@Configuration
@RequiredArgsConstructor
public class SecurityConfig {

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http.csrf(AbstractHttpConfigurer::disable)
                .cors(cors -> cors
                        .configurationSource(CorsConfig.corsConfigurationSource()))
                .formLogin(AbstractHttpConfigurer::disable)
                .httpBasic(AbstractHttpConfigurer::disable)
                .authorizeHttpRequests(authorizeRequests ->
                        authorizeRequests
                                .requestMatchers("/signup").permitAll()
                                .requestMatchers("/login").permitAll()
                                .requestMatchers("/swagger-ui/**").permitAll()
                                .requestMatchers("/**").permitAll()
                                .anyRequest().permitAll() //redirect막기 위해 임시로 permitAll
//                    .anyRequest().authenticated() // 인증 구현시, 주석 해제
                );
        return http.build();
    }
}
```

## ✅ CD 1

<img width="709" alt="Image" src="https://github.com/user-attachments/assets/50ddfefb-11aa-4ece-84b2-ac52b37fd32a" />

```yaml
name: CD #actions workflow에 뜨는 이름

on:
  push: #push되었을 때
    branches: #어떤 브랜치에 push되었을 때
      - main # - develop

jobs:
  deploy:
    runs-on: ubuntu-latest # 내 github actions를 실행할 컴퓨터 OS

    steps:
      - name: connect EC2 through SSH
        uses: appleboy/ssh-action@v1.0.3
        with:
          host: ${{ secrets.HOST }} #github actions secerts에 다음 3가지 저장
          username: ${{ secrets.USERNAME }}
          key: ${{secrets.EC2_PRIVATE_KEY }} #EC2만들 때 다운받은 pem키
          script: |
            cd /home/ec2-user/Moim-BE
            git pull origin main #새로운 코드 pull해서 가져오고
            ./gradlew clean build -x test # build하기
            sudo fuser -k -n tcp 8080 || true #port 8080에 running하는 프로세스 지우고, 없다면 그냥 없는대로
            nohup java -jar build/libs/*SNAPSHOT.jar > ./output.log  2>&1 & #nohup으로 무중단 배포, log도 만들어라
```

- github actions secerts에 사용되는 `secrets` 추가

<img width="1015" alt="Image" src="https://github.com/user-attachments/assets/50a7f6d8-6beb-4258-bfd2-bddd392c3fc2" />

- 💡 결론: `main`브랜치에 새로운 내용을 바꾸고, `push`하면 잘 반영된다.
- `test controller`의 `return`값에 간단히 내용을 추가하고 `git add, commit, push`하면 반영되는 것 확인

- 👍🏻 git pull을 활용해서 변경된 부분의 프로젝트 코드에 대해서만 업데이트 하기 때문에 CI/CD 속도가 빠르다
- 👍🏻 CI/CD 툴로 Github Actions만 사용하기 때문에 인프라 구조가 복잡하지 않고 간단
- 👎🏻 빌드 작업을 EC2에서 직접 진행, 서버 부하가 크다
- 👎🏻 Github 계정 정보가 해당 EC2에 저장된다

## ✅ CD 2

<img width="734" alt="Image" src="https://github.com/user-attachments/assets/bee9fec6-595d-4f2f-a24e-35827043b399" />

- 🆚 **기존 `CD 1`과 차이점**

  - `CD 1`는 바뀐 `code`에 대해서만 `pull`을 받아왔다면, `CD 2`는 통째로 파일을 지우고, 새로 올려서 배포하는 방식
  - checkout repository
  - install JDK: temurin이라는 JDK설치, 기업에서 많이 사용
  - change build file name
  - use SCP

- `running`: 현재 실행중인 `jar`파일이 있는 폴더
- `willrun`: 새롭게 내용이 반영되어, 앞으로 실행하고 싶은 `jar`파일이 있는 폴더
- 새로운 내용 반영 후 실행하고 싶은 `jar`파일을 `willrun`에 저장
- `running`은 지우고
- 다시 폴더 `running`만들고
- `willrun`에 있는 `jar`파일을 `running`으로 복사
- 포트 8080에서 실행하고 있는 프로세스 죽이고
- `willrun`에 있는 `jar`파일 `nohup`으로 실행
- `willrun`폴더 삭제

```bash
name: CD

on:
  push:
    branches:
      - develop

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository #repository불러오기
        uses: actions/checkout@v2=4

      - name: Set up JDK 17  #java 17을 설치해라, 그 중에서도 temurin
        uses: actions/setup-java@v4
        with:
          java-version: '17'
          distribution: 'temurin'

      - name: test and build #build하고
        run: ./gradlew clean build -x test

      - name: change build file name #build file이름 바꾸기
        run: mv ./build/libs/*SNAPSHOT.jar ./project.jar #원래 *SNAPSHOT.jar 였는데 ./project.jar로 이름을 바꾼다

      - name: use SCP to send build file to EC2 #SCP라는걸 이용해서 만든 build file을 EC2로 보낸다
        uses: appleboy/scp-action@v0.1.7
        with:
          host: ${{ secrets.HOST }}
          username: ${{ secrets.USERNAME }}
          key: ${{secrets.EC2_PRIVATE_KEY }}
          source: project.jar
          target: /home/ec2-user/Moim-BE/willrun  #앞으로 실행될 파일을 build file을 willrun라는 폴더에 저장할 것

      - name: connect EC2 through SSH
        uses: appleboy/ssh-action@v1.0.3
        with:
          host: ${{ secrets.HOST }}
          username: ${{ secrets.USERNAME }}
          key: ${{secrets.EC2_PRIVATE_KEY }} #EC2만들 때 다운받은 pem키
				  script: |
            rm -rf /home/ec2-user/Moim-BE/running  #rm -rf 현재 실행 중인 파일 담긴 폴더 지우기
            mkdir /home/ec2-user/Moim-BE/running #mkdir 현재 실행 중인 파일 담을 폴더 만들기 mkdir
            mv /home/ec2-user/Moim-BE/willrun/project.jar /home/ec2-user/Moim-BE/running/project.jar  #앞으로 실행될 파일에 있는 폴더에 가서 willrun/project.jar #현재 실행될 파일을 저장하는 폴더로 이동
            cd /home/ec2-user/Moim-BE/running   #cd 현재 실행되고 있는 파일 있는 폴더로 가서
            sudo fuser -k - tcp 8080 || true #현재 포트 8080에서 실행되는 파일 있으면 지우고, 없으면 없는대로 true
            nohup java -jar project.jar > ./output.log 2>&1 & #nohup 빌드 파일 실행
            rm -rf /home/ec2-user/Moim-BE/willrun #rm -rf 실행될 파일 저장하는 폴더는 삭제

```

- 👍🏻 빌드 작업을 Github Actions에서 해줌, 서버에 영향을 주지 않는다
- 👍🏻 CI/CD 툴로 Github Actions만 사용, 다른 스크립트가 필요없어 간단하다
- 👎🏻 여러 EC2 인스턴스에 배포를 해야 하는 상황이라면, 직접 Github Actions에 스크립트를 작성해야 한다

## 👎🏻 다른 브랜치에서 push, pull request한 경우

- 개발을 하다보면 `develop`브랜치에서 직접 작업을 하는 경우는 거의 없고
- 특정 기능 개발을 위한 다른 브랜치에서 개발, 테스트 후 `develop`으로 `merge`한다
- 따라서 다른 브랜치에서 `push`한 다음, `develop`으로 `pull request`를 하여 `merge`했을 때
- `CI`가 자동으로 이루어지기 위해 `CI` 스크립트 작성

## ✅ CI

- `on: pull_request:`라는 점이 `CD`와 다르다

```bash
name: CI

on:
  pull_request:
    branches:
      - develop

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Set up JDK 17
        uses: actions/setup-java@v4
        with:
          java-version: '17'
          distribution: 'temurin'

      - name: Setup Gradle
        uses: gradle/actions/setup-gradle@af1da67850ed9a4cedd57bfd976089dd991e2582
        # GitHub Action that installs and caches Gradle to speed up builds.

      - name: Run tests with Gradle
        run: ./gradlew test

      - name: Build with Gradle
        run: ./gradlew build -x test
```

- 👍🏻 이렇게 `CI`를 작성하면 다른 브랜치에서 머지했을 때 빌드가 자동화 됨

## CD 2 🆚 CD 3

- ✔️ `CD 2`: Renames JAR to project.jar
- ✔️ `CD 3`: Uses versioned JAR (todo-0.0.1-SNAPSHOT.jar)
- 👍🏻 `JAR`파일의 버전을 관리할 수 있다

- ✔️ `CD 2`: Uses SCP (Secure Copy Protocol)
- ✔️ `CD 3`: Uses SCP but with additional SSH key setup
- 👍🏻 `SSH 키`로 접속한다는 점이 다르다

- ✔️ `CD 2`: Directly moves and runs the JAR on EC2
- ✔️ `CD 3`: Runs a separate deploy.sh script for better modularity
- 👍🏻 변경사항 발생 시 modularity가 높으니 부분만 수정하면 된다

- ✔️ `CD 2`: Minimal Logging (only redirects to output.log)
- ✔️ `CD 3`: Maintains date-based logs for better debugging
- 👍🏻 날짜별로 log를 유지하니 에러 발생 시 디버깅이 쉽다

- ✔️ `CD 2`: Deletes /willrun directory after deployment
- ✔️ `CD 3`: Keeps logs and maintains directory structure
- 👍🏻 bug발생 시 directory확인 가능

#### ✔️ Conclusion

- 👍🏻 `CD 2`의 장점:
  - simple, fast, straightforward
  - no external script dependency, 따로 스크립트 작성할 필요 없음! only github actions
- 👎🏻 `CD 2`의 단점:

  - No Environment Variable Handling
  - minimal logging
  - not modular

- 👍🏻 `CD 3`의 장점:
  - more secure: SSH key based authentication
  - better loggin
  - modular, maintainable
  - handle environment variables properly
- 👎🏻 `CD 3`의 단점:
  - more complex setup, requires external `deploy.sh` script
  - SSH setup required
  - slower, additional SSH setups required

## ✅ CD 3

```bash
name: CD

on:
  push:
    branches:
      - develop

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v2

      - name: Set up JDK 17
        uses: actions/setup-java@v4
        with:
          java-version: '17'
          distribution: 'temurin'

      - name: Setup Gradle
        uses: gradle/actions/setup-gradle@af1da67850ed9a4cedd57bfd976089dd991e2582

      - name: Add SSH host key #Adds SSH host key (to prevent host verification issues)
        run: |
          mkdir -p ~/.ssh
          ssh-keyscan -H ${{ secrets.HOST }} >> ~/.ssh/known_hosts
          chmod 644 ~/.ssh/known_hosts

      - name: Set up SSH private key #Sets up SSH private key for authentication.
        run: |
          echo "${{ secrets.EC2_PRIVATE_KEY }}" > ~/.ssh/private_key.pem
          chmod 600 ~/.ssh/private_key.pem

      - name: Build with Gradle
        run: ./gradlew clean build -x test

      - name: Check JAR File
        run: ls -l build/libs/

      - name: Upload JAR to Remote Server
        run: |
          echo "${{ secrets.EC2_PRIVATE_KEY }}" > ~/.ssh/private_key.pem
          chmod 600 ~/.ssh/private_key.pem
          ssh -i ~/.ssh/private_key.pem ${{ secrets.USERNAME }}@${{ secrets.HOST }} "mkdir -p ${{ secrets.APP_DIR }}"
          scp -i ~/.ssh/private_key.pem build/libs/moim-0.0.1-SNAPSHOT.jar ${{ secrets.USERNAME }}@${{ secrets.HOST }}:${{ secrets.APP_DIR }}
        env:
          EC2_PRIVATE_KEY: ${{ secrets.EC2_PRIVATE_KEY }}

      - name: Deploy to Remote Server # Runs the deploy.sh script remotely
        run: |
          ssh -i ~/.ssh/private_key.pem ${{ secrets.USERNAME }}@${{ secrets.HOST }} '
            export APP_DIR="${{ secrets.APP_DIR }}";
            export DB="${{ secrets.DB }}";
            export DB_PASSWORD="${{ secrets.DB_PASSWORD }}";
            export DB_USERNAME="${{ secrets.DB_USERNAME }}";
            export HOST="${{ secrets.HOST }}";
            bash -s
          ' < ./deploy.sh
        env:
          EC2_PRIVATE_KEY: ${{ secrets.EC2_PRIVATE_KEY }}
          APP_DIR: ${{ secrets.APP_DIR }}
          DB: ${{ secrets.DB }}
          DB_PASSWORD: ${{ secrets.DB_PASSWORD }}
          DB_USERNAME: ${{ secrets.DB_USERNAME }}
          HOST: ${{ secrets.HOST }}
```

#### ❓ Where do I save the `.pem key`?

- `SSH`연결을 위해 EC2서버에 `.pem key`를 저장해야 하는건 알겠는데,
- 이 `.pem key`는 너무 길어서 `bashrc`에 저장하는게 아닌 것 같았다
- 그러다 검색하다 이걸 알게되었다
- ⚠️ Important: If your private key is multi-line, you should store it as a file instead of an environment variable.
- `reference the key in a file`

- 그래서 추가된 내용이 다음과 같다
- github secrets에서 EC2_PRIVATE_KEY를 가져와서
- `~/.ssh/private_key.pem`라는 파일을 만들고 복사해서 저장하기

```yaml
- name: Set up SSH private key #Sets up SSH private key for authentication.
  run: |
    echo "${{ secrets.EC2_PRIVATE_KEY }}" > ~/.ssh/private_key.pem
    chmod 600 ~/.ssh/private_key.pem
```

## ✅ deploy.sh

```sh
#!/bin/bash

# 어플리케이션 세팅
APP_DIR="${APP_DIR}"
JAR_PATH="${APP_DIR}/moim-0.0.1-SNAPSHOT.jar"
LOG_DIR="${APP_DIR}/logs"
DEPLOY_DATE=$(date +'%Y-%m-%d')

# DB 세팅
DB="${DB}"
DB_PASSWORD="${DB_PASSWORD}"
DB_USERNAME="${DB_USERNAME}"
HOST="${HOST}"

mkdir -p "$LOG_DIR"

PID=$(lsof -t -i:8080)
if [ ! -z "$PID" ]; then
  echo "Killing the old application with PID: $PID"
  kill -9 $PID
fi

LOG_FILE="${LOG_DIR}/moim-${DEPLOY_DATE}.log"

echo "Starting new application..."
nohup java -jar "$JAR_PATH" > "$LOG_FILE" 2>&1 &
NEW_PID=$!

sleep 5

# 서버가 실행 중인지 확인
if ps -p $NEW_PID > /dev/null; then
  echo "Application started successfully!"
else
  echo "Server did not start. Please check the logs: $LOG_FILE"
fi

```

## 🔴 No such file or directory error

<img width="725" alt="Image" src="https://github.com/user-attachments/assets/d84d38c4-d4da-42e9-8b63-522e3020f3a7" />

<img width="712" alt="Image" src="https://github.com/user-attachments/assets/26c7906c-0c14-4626-817c-9b3553d3381b" />

#### 💊 환경변수에 추가

- `${{ secrets.APP_DIR }}`
- 💊 bashrc에도 추가

```
APP_DIR
/home/ec2-user/Moim-BE/build/libs
```

#### 💊 파일을 먼저 생성하고, upload JAR하도록 코드 추가

- ensure the directory `${{ secrets.APP_DIR }}` exists before scp runs

- 🔴 Before

```yaml
- name: Upload JAR to Remote Server
  run: |
    echo "${{ secrets.EC2_PRIVATE_KEY }}" > ~/.ssh/private_key.pem
    chmod 600 ~/.ssh/private_key.pem
    scp -i ~/.ssh/private_key.pem build/libs/moim-0.0.1-SNAPSHOT.jar ${{ secrets.USERNAME }}@${{ secrets.HOST }}:${{ secrets.APP_DIR }}
```

- 🟢 After

```yaml
- name: Upload JAR to Remote Server
  run: |
    echo "${{ secrets.EC2_PRIVATE_KEY }}" > ~/.ssh/private_key.pem
    chmod 600 ~/.ssh/private_key.pem
    ssh -i ~/.ssh/private_key.pem ${{ secrets.USERNAME }}@${{ secrets.HOST }} "mkdir -p ${{ secrets.APP_DIR }}"
    scp -i ~/.ssh/private_key.pem build/libs/moim-0.0.1-SNAPSHOT.jar ${{ secrets.USERNAME }}@${{ secrets.HOST }}:${{ secrets.APP_DIR }}
```
