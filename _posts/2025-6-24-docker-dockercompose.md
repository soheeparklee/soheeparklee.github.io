---
title: Docker compose
categories: [Deploy, Docker]
tags: [] # TAG names should always be lowercase
---

## ✅ Docker Compose

- docker container **여러개 띄우고** 하나로 관리하고 싶을 때
- 여러개의 docker container들을 하나의 서비스로 정의하고 구성, **하나의 묶음으로 관리**
- 👍🏻 easy to maintain several containers together
- 👍🏻 easier commands

## ☑️ Docker compose file with Nginx

- create `compose.yml`

```yaml
services:
  my-web-server: #service name
    container_name: webserver #container name
    image: nginx
    ports:
      - 80:80
```

- run, stop docker

```bash
# run docker
docker compose up -d

# stop, remove docker
 docker compose down
```

## ☑️ Docker compose CLI

- get running containers

```bash
# get containers
docker compose ps
docker compose ps -a

# get logs
docker compose logs

# go inside container
 docker exec -it {{containerID}} bash
```

- pull
- if `docker image` has a new version, **update** new version

```bash
# pull docker image
docker compose pull
```

## ☑️ Docker compose file with Redis

```yaml
services:
  my-cache-server: #service name
    container_name: redis-server #container name
    image: redis
    ports:
      - 6379:6379
```

## ☑️ Docker compose file with MySQL

- 기존 docker volume: `docker run -e MYSQL_ROOT_PASSWORD=12341234 -d -p 3306:3306 -v /Users/sohmac/downloads/docker-mysql/mysql_data:/var/lib/mysql mysql`

- docker compose yml file is much more simple!

```yaml
services:
  my-db:
    container_name: sql-server
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: 12341234
    volumes:
      - ./mysql_data:/var/lib/mysql
    ports:
      - 3306:3306
```

## ☑️ Docker compose file with SpringBoot

- need `dockerfile`
- create `compose.yml`

```yaml
services:
  my-server:
    build: . #dockerfile is in the same directory as compose.yml
    ports:
      - 8080:8080
```

- run on terminal
- `--build` means if build file changes, build again
- always build with the latest code updates

```bash
 docker compose up -d --build
```

## ☑️ Docker compose file with Nest.js

- need `dockerfile`
- create `compose.yml`

```yaml
services:
  my-nest:
    build: . #dockerfile and compose.yml are in the same directory
    ports:
      - 3000:3000
```

- run on terminal
- `--build` with the latest code updates

```bash
docker compose up -d --build
```

## ☑️ Docker compose file with Next.js

- need `dockerfile`
- create `compose.yml`

```yaml
services:
  my-next:
    build: . #dockerfile and compose.yml are in the same directory
    ports:
      - 80:3000
```

- run on terminal

```bash
docker compose up -d --build
```

## ☑️ Docker compose file with HTML

- need `dockerfile`
- create `compose.yml`

```yaml
services:
  my-server:
    build: .
    ports:
      - 80:80
```

- run on terminal

```bash
docker compose up -d --build
```

## 💡 Docker CLI ↔️ compose.yml

- CLI ➡️ compose.yml
- <https://www.composerize.com/>

- compose.yml ➡️ CLI
- <https://www.decomposerize.com/>

## ✅ Docker Compose MySQL & Redis

- MySQL & Redis container을 동시에 띄우기

```yaml
services:
  my-db:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: 12341234
    volumes:
      - ./mysql_data:/var/lib/mysql
    ports:
      - 3306:3306
  my-cache-server:
    image: redis
    ports:
      - 6379:6379
```

- run, stop on terminal

```bash
# 두 컨테이너 동시에 올리기
docker compose up -d

# 두 컨테이너 동시에 내리기
docker compose down
```

[![Screenshot-2025-06-24-at-16-42-38.png](https://i.postimg.cc/5y8VQK6W/Screenshot-2025-06-24-at-16-42-38.png)](https://postimg.cc/m1Zq0wYm)

## ✅ Docker Compose SpringBoot & MySQL

- create `application.yaml` file

```yaml
spring:
  config:
    activate:
      on-profile: dev
  datasource:
    url: jdbc:mysql://${HOST}:3306/${DB} #⭐️
    username: ${DB_USERNAME}
    password: ${DB_PASSWORD}
    driver-class-name: com.mysql.cj.jdbc.Driver
    hikari:
      maximum-pool-size: 10
```

- springboot should run **after** mySQL is successfully connected
- use `depends_on`, `healthcheck`
- if `my-db` health check fails, `my-server` will not run

```yaml
services:
  my-server:
    build: .
    ports:
      - 8080:8080
    depends_on: #my-server will run when condition is fulfilled
      my-db:
        condition: service_healthy #my-server will run when my-db service_healthy
  my-db: #⭐️
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: MoimSQL02!
      MYSQL_DATABASE: moim
    volumes:
      - ./mysql_data:/var/lib/mysql
    ports:
      - 3306:3306
    healthcheck: #how to do health_check for my-db
      test: ["CMD", "mysqladmin", "ping"]
      interval: 5s
      retries: 10
```

- build and run

```bash
./gradlew clean build

docker compose up -d --build
```

- ✔️ **result**
- mysql is healthy

[![Screenshot-2025-06-24-at-16-56-18.png](https://i.postimg.cc/nr6q0kKk/Screenshot-2025-06-24-at-16-56-18.png)](https://postimg.cc/m1ycr75z)

- ⚠️ **However, this will not connect springboot and mysql**

[![Screenshot-2025-06-24-at-17-09-42.png](https://i.postimg.cc/HLjm0Dzb/Screenshot-2025-06-24-at-17-09-42.png)](https://postimg.cc/Z9kXZQ1q)

- mysql succeeded, but spring fails

[![Screenshot-2025-06-24-at-17-03-16.png](https://i.postimg.cc/d1sTq0jG/Screenshot-2025-06-24-at-17-03-16.png)](https://postimg.cc/WDy48TK4)

- each container is **independent**
- springboot will look for `port 3306` in its container
- however, mysql is run in another container
- ➡️ fail to connect
- need to tell spring container to get `port 3306` in another container
- 💊 configure `application.yml`

## ✅ Final Docker Compose SpringBoot & MySQL

- 💊 **fix and configure** `application.yml`
- Final `application.yaml` file
- write in `host`, the service name we wrote in `compose.yml` file

```yaml
spring:
  config:
    activate:
      on-profile: dev
  datasource:
    #url: jdbc:mysql://${HOST}:3306/${DB}
    url: jdbc:mysql://my-db:3306/${DB} #⭐️ my-db
    username: ${DB_USERNAME}
    password: ${DB_PASSWORD}
    driver-class-name: com.mysql.cj.jdbc.Driver
    hikari:
      maximum-pool-size: 10
```

```yaml
services:
  my-server:
    build: .
    ports:
      - 8080:8080
    depends_on:
      my-db:
        condition: service_healthy
  my-db: #⭐️
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: MoimSQL02!
      MYSQL_DATABASE: moim
    volumes:
      - ./mysql_data:/var/lib/mysql
    ports:
      - 3306:3306
    healthcheck:
      test: ["CMD", "mysqladmin", "ping"]
      interval: 5s
      retries: 10
```

- ✔️ **result**
  [![Screenshot-2025-06-24-at-17-11-19.png](https://i.postimg.cc/Dyg3tyYq/Screenshot-2025-06-24-at-17-11-19.png)](https://postimg.cc/qzzFK0rR)

- both mysql and springboot is up

## ✅ Docker Compose SpringBoot & MySQL & Redis

- add redis configuration
- ✔️ `application.yaml`

```yaml
spring:
  config:
    activate:
      on-profile: dev
  datasource:
    #url: jdbc:mysql://${HOST}:3306/${DB}
    url: jdbc:mysql://my-db:3306/${DB}
    username: ${DB_USERNAME}
    password: ${DB_PASSWORD}
    driver-class-name: com.mysql.cj.jdbc.Driver
    hikari:
      maximum-pool-size: 10
  data: # add redis config
    redis:
      #host: localhost
      host: my-cache-server #⭐️
      port: 6379
```

- ✔️ `redis.config`

```java
@Configuration
public class RedisConfig {
    @Bean
    public RedisTemplate<String, Object> redisTemplate(RedisConnectionFactory connectionFactory) {
        RedisTemplate<String, Object> template = new RedisTemplate<>();
        template.setConnectionFactory(connectionFactory);
        template.setKeySerializer(new StringRedisSerializer());
        template.setValueSerializer(new GenericJackson2JsonRedisSerializer());
        return template;
    }
}

```

- ✔️ `testCtontroller`

```java
@Slf4j
@RestController
public class TestController {

    @Autowired
    private RedisTemplate<String, Object> redisTemplate;
    @GetMapping("/")
    public String home(){
        redisTemplate.opsForValue().set("abc", "def");
        return "Hello world this is home page";
    }
```

- ✔️ `compose.yml`

```yaml
services:
  my-server:
    build: .
    ports:
      - 8080:8080
    depends_on:
      my-db:
        condition: service_healthy
      my-cache-server: # add health check
        condition: service_healthy
  my-db:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: MoimSQL02!
      MYSQL_DATABASE: moim
    volumes:
      - ./mysql_data:/var/lib/mysql
    ports:
      - 3306:3306
    healthcheck: #how to do health_check for my-db
      test: ["CMD", "mysqladmin", "ping"]
      interval: 5s
      retries: 10
  my-cache-server: # redis compose config
    image: redis
    ports:
      - 6379:6379
    healthcheck:
      test: ["CMD", "redis-cli", "ping"]
      interval: 5s
      retries: 10
```

## ✅

## ✅

## ✅

59
60
quiz
