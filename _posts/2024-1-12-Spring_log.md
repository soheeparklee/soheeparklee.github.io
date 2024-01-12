---
title: Logging, LogBack, Slf4j
categories: [JAVA, Spring]
tags: [log, logger, logpattern, slf4j] # TAG names should always be lowercase
---

## ✅ Logging

> Log: 서버가 수행한 작업/상태에 대한 기록 <br>

#### 🙏🏻 Logging 필요성

java 콘솔로 출력하다보면 내부 정보(어떤 스레드, 만들어진 시간 등)까지는 기록하지 못하고, <br>
애플리케이션이 꺼졌다 켜지면 사라짐, 파일로 생성하고 싶음 <br>
로그 제어, 필터링 하고 싶음 <br>

### ☑️ 로그 레벨

- ERROR: 요청을 처리하는 도중에 발생하는 오류 로그 <br>
- WARN: 처리 가능한 문제이지만, 향후 에러의 원인이 될 수 있다는 경고 로그 <br>
- INFO: 상태 변경(100개였는데 10개가 되었음) 같은 정보 <br>
- DEBUG: 프로그램 디버깅 정보 로그 <br>

### ☑️ Logger

> 로깅을 실행하는 주체 <br>

모든 로거는 Root로거의 하위에 있다. <br>

### ☑️ Log Pattern

> 로그 메세지 출력 형식을 정의한 템플릿 <br>

시간, 정보, 쓰레드 정보 등을 탑재할 수 있다. <br>

### ☑️ Log Appender

> log 기록의 목적지

- Console appender 그래도 console에 출력 <br>
- File appender 로깅 생성 시 파일 기록 <br>
- Messenger appender 로깅 생성 시 메세지로 송출 <br>

## ✅ Logback

> Logging을 구현하는 인터페이스를 Slf4j 인터페이스라고 한다. <br>
> Logging을 구현하는 Slf4j 인터페이스 중 Logback이 있음 <br> > <br>

`this.getClass()`<br>

### ✔️ Logback 사용 설정

```xml
//logback-spring-local.xml
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

```xml
//logback-spring-dev.xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <property name="LOG_PATH" value="logs" />

    <!-- 콘솔 로그 출력 -->
    <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
        //⭐️ logpattern
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %highlight(%-5level) %cyan(%logger{36}) - %msg%n</pattern>
        </encoder>
    </appender>

    <appender name="FILE" class="ch.qos.logback.core.FileAppender">
        <file>${LOG_PATH}/test.log</file>
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

```yaml
application.yaml
server:
  port: 8080
logging:
  config: classpath:logback-spring-local.xml
  #classpath: 이 파일로 가세요 가리키는 화살표
```

### ✔️ logger 사용 예시

```java
//Controller에서 logger 사용 예시
public class ElectronicStoreControllerLombok {
    //logger
    //logger을 추가해 어떤 정보가 들어왔는지 볼 수 있음
    //logger.warn, logger.debug 등등...필요한 레벨로 사용
    private Logger logger= LoggerFactory.getLogger(this.getClass());

    @GetMapping("/items")
    public List<Item> findAllItem(){
        logger.info("GET/items requested"); //이렇게 logger 추가
        List<Item> items= electronicStoreItemService.findAllItem();
        logger.info("GET/items:" + items); //이렇게 logger 추가
        return items;
    }
```

### ✔️ logger 사용 예시

```java
//Service에서 Logger 사용 예시

@Service
public class ElectronicStoreItemService {
    private final Logger logger = LoggerFactory.getLogger(this.getClass());

@Transactional(transactionManager = "tm1")
    public Integer buyItems(BuyOrder buyOrder) {
        //이런식으로 error보이도록 설정 가능
        logger.error("store 또는 stock이 없으면 구매할 수 없습니다");
        if(itemEntity.getStoreId() == null) throw new RuntimeException("No Store Found");
        if(itemEntity.getStock() == 0) throw new RuntimeException("No stock available");
    }
```

### ✔️ 더 간단하게 annotation으로 Log 사용 `log`

```java
//더 간단하게 annotation으로 Log 사용 설정
@Slf4j
@Service
public class ElectronicStoreItemService {

@Transactional(transactionManager = "tm1")
    public Integer buyItems(BuyOrder buyOrder) {
        //이런식으로 error보이도록 설정 가능
        log.error("store 또는 stock이 없으면 구매할 수 없습니다");
        log.info("구매를 완료하였습니다.");
    }
}
```
