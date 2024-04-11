---
title: Redis_email certification
categories: [JAVA, Spring]
tags: [redis. jasypt] # TAG names should always be lowercase
---

## ✅ 작동 순서

유저가 회원가입 하면서 이메일 입력
➡️ 서버에서 이메일로 인증번호 이메일 발송
➡️ 인증번호는 Redis에 저장(만료시간 5분)
➡️ 유저가 이메일에서 인증번호 확인
➡️ 이메일과 인증번호로 서버에 인증 요청
➡️ 서버에서 Redis있는 인증번호와 비교
➡️ 인증 완료 혹은 exceptions처리

### 💡 Jasypt

> Java library that provides simple APIs for encryption and decryption of data, including hashing.

#### 해싱이란?

> transforming text into charecters using a one-way cryptographic hash function

- one way cryptographic function
- results in hash value/hash code
- **irreversable**
- MD5, SHA-1, SHA-256

🆚 Encryption <br>

- eversible cryptographic process
- encrypts with an algorithm and a key
- AES, DES, RSA

#### Salt?

> "salt" is random data that is used as an additional input to a hash function along with the plain text being hashed

- thanks to salt, we can defend against attacks and add complexity to the hashing process.
- When hashing a password or any other sensitive data, you can provide a salt along with the data.
- The salt is then combined with the data before hashing, resulting in a unique hash for each input even if the original data is the same.

#### 인코딩?

> process of transforming data into a format that is suitable for a particular type of transmission or storage system

- GOAL: make sure data can be represented and transmitted properly
- Base64, hexadecimal, URL encoding

🆚 Encryption <br>

- GOAL: protect data, data confidentiality

### 💡 Redis

> open-source, in-memory data structure store that can be used as a database, cache, and message broker

- caching, session management
- save frequently used data in memory, to reduce the laod off the primary data storage.
- 단 5분동안만 사용할 인증번호를 데이터베이스에 저장하고 삭제하는 것은 번거로운 일이며 비용도 많이 든다. 따라서 인메모리인 Redis에 저장하여 속도를 높이고 비용을 절약한다.

### 💡 @Valid 사용하여 유효성 검사

@Valid를 붙여 놓으면 check validation on input data. <br>
예를 들어, <br>
`public ResponseEntity<String> createUser(@Valid @RequestBody User user)` <br>
이렇게 `User`앞에 `@Valid`를 붙여 놓으면 `User`를 `@RequestBody`로 가져오기 전에 유효성을 검사하고 가져온다. <br>

## ✅ gmail 2단계 인증 설정

- 앱 비밀번호 받기
- 구글 계정 관리
- 보안
- google에 로그인 하는 방법 -> 2단계 인증 설정
- 구글 검색창에 "앱 비밀번호 검색"
- 앱 비밀번호 생성
- 이 비밀번호는 나중에 yaml파일에 jasypt로 암호화 해서 넣어둘 것이니 잘 기억해두기

### build.gradle에 의존성 추가

```groovy
   	// email 인증
    implementation group: 'org.springframework.boot', name: 'spring-boot-starter-mail', version: '2.6.3'
    implementation 'javax.mail:mail:1.4.7'

    // Spring Context Support
    implementation 'org.springframework:spring-context-support:5.3.9'

    // redis
    implementation 'org.springframework.boot:spring-boot-starter-data-redis'
```

## ✅ 인증번호 전송하는 email

### EmailCertificationConfig

- 이메일 보낼 email Address(yaml에서 관리)
- 아까 생성한 앱 비밀번호(yaml에서 관리)
- 이메일을 어떻게 보낼 것인가? `JavaMailSender
  - `JavaMailSender` host, port, javaMailProperties 정하기
- 랜덤 인증번호 생성 메소드 `generateRandomNumber`

```java
import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.mail.javamail.JavaMailSender;
import org.springframework.mail.javamail.JavaMailSenderImpl;

import java.util.Properties;
import java.util.Random;

@Configuration
public class EmailCertificationConfig {
    @Value("${email.address}")
    private String emailAddress;
    @Value("${email.app-password}")
    private String appPassword;

    @Bean
    public JavaMailSender mailSender(){ //JAVA MAILSENDER 인터페이스를 구현한 객체를 빈으로 등록하기 위함.
        JavaMailSenderImpl mailSender= new JavaMailSenderImpl(); // JavaMailSender 의 구현체 생성
        mailSender.setHost("smtp.gmail.com"); // 이메일 전송에 사용할 SMTP 서버 호스트를 설정
        mailSender.setPort(587); // 587로 포트를 지정
        mailSender.setUsername(emailAddress); //구글계정을 넣습니다.
        mailSender.setPassword(appPassword); //구글 앱 비밀번호를 넣습니다

        Properties javaMailProperties= new Properties(); //JavaMail의 속성을 설정하기 위해 Properties 객체를 생성
        javaMailProperties.put("mail.transport.protocol", "smtp"); //프로토콜로 smtp 사용
        javaMailProperties.put("mail.smtp.auth", "true"); //smtp 서버에 인증이 필요
        javaMailProperties.put("mail.smtp.socketFactory.class", "javax.net.ssl.SSLSocketFactory"); //SSL 소켓 팩토리 클래스 사용
        javaMailProperties.put("mail.smtp.starttls.enable", "true"); //STARTTLS(TLS를 시작하는 명령)를 사용하여 암호화된 통신을 활성화
        javaMailProperties.put("mail.debug", "true"); //디버깅 정보 출력
        javaMailProperties.put("mail.smtp.ssl.trust", "smtp.naver.com"); //smtp 서버의 ssl 인증서를 신뢰
        javaMailProperties.put("mail.smtp.ssl.protocols", "TLSv1.2"); //사용할 ssl 프로토콜 버젼

        mailSender.setJavaMailProperties(javaMailProperties); //mailSender에 우리가 만든 properties 넣고
        return mailSender;
    }

    // min과 max 사이의 랜덤한 정수를 반환하는 메서드
    public static int generateRandomNumber(int min, int max){
        Random random= new Random();
        return random.nextInt(max - min + 1) + min;
    }
}

```

### EmailRequest DTO

유저의 이메일 받아오기 <br>
Validation을 사용해 유효성 검사 <br>

```java
@Getter
@Setter
public class EmailRequest {
    @Email(message= "이메일 형식을 확인해주세요.")
    @NotEmpty(message="이메일을 입력해주세요.")
    private String email;
}
```

### EmailCertificationController

- 이메일 보내는 메소드

```java
import jakarta.validation.Valid;
import lombok.RequiredArgsConstructor;
import org.shoppingMall.service.service.EmailCertificationService;
import org.shoppingMall.service.service.RedisUtil;
import org.shoppingMall.web.DTO.email.EmailRequest;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequiredArgsConstructor
@RequestMapping("/mail")
public class EmailCertificationController {

    private final EmailCertificationService emailCertificationService;
    private final RedisUtil redisUtil;
    @PostMapping("/send-mail")
    public String sendMail(@RequestBody @Valid EmailRequest emailRequest){
        System.out.println("이메일 인증 이메일 : " + emailRequest.getEmail());
        return emailCertificationService.joinEmail(emailRequest.getEmail());
    }
}


```

### EmailCertificationService

- 이메일 보내는 메소드(yaml에서 관리)
  - 이메일 보낼 email Address
  - 이메일 제목
  - 이메일 내용

```java
import lombok.RequiredArgsConstructor;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.mail.javamail.JavaMailSender;
import org.springframework.mail.javamail.MimeMessageHelper;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

import javax.mail.MessagingException;
import javax.mail.internet.MimeMessage;

import static org.shoppingMall.config.certification.EmailCertificationConfig.generateRandomNumber;

@Service
@RequiredArgsConstructor
public class EmailCertificationService {
    private final JavaMailSender mailSender;
    private final RedisUtil redisUtil;

    private final int authNumber= generateRandomNumber(100000, 999999); // config 에 미리 만들어둔 메서드
    @Value("${email.address}")
    private String emailAddress; // email-config에 설정한 자신의 이메일 주소를 입력
    public String joinEmail(String email) {
        String setFrom= emailAddress;
        String toMail= email;
        String title= "[인증]OOO사이트 가입 인증번호";
        String content=
                "회원가입 창으로 돌아가 인증 번호를 정확히 입력해주세요." + 	//html 형식으로 작성 !
                        "<br><br>" +
                        "인증 번호는 " + authNumber + "입니다." +
                        "<br>" ; //이메일 내용 삽입
        mailSend(setFrom, toMail, title, content);
        return Integer.toString(authNumber);
    }

    @Transactional
    public void mailSend(String setFrom, String toMail, String title, String content) {
        MimeMessage message= mailSender.createMimeMessage(); //JavaMailSender 객체를 사용하여 MimeMessage 객체를 생성
        try{
            MimeMessageHelper helper= new MimeMessageHelper(message, true, "utf-8"); //이메일 메시지와 관련된 설정을 수행합니다.
            // true를 전달하여 multipart 형식의 메시지를 지원하고, "utf-8"을 전달하여 문자 인코딩을 설정
            helper.setFrom(setFrom); //이메일의 발신자 주소 설정
            helper.setTo(toMail); //이메일의 수신자 주소 설정
            helper.setSubject(title); //이메일의 제목을 설정
            helper.setText(content, true);
            mailSender.send(message); //이메일의 내용 설정 두 번째 매개 변수에 true를 설정하여 html 설정으로한다.
        }catch(MessagingException e){ //이메일 서버에 연결할 수 없거나, 잘못된 이메일 주소를 사용하거나, 인증 오류가 발생하는 등 오류
            // 이러한 경우 MessagingException이 발생
            e.printStackTrace(); //e.printStackTrace()는 예외를 기본 오류 스트림에 출력하는 메서드

        }
    }
}
```

## ✅ Bean으로 Jasypt 암호화 설정

### Jasypt build.gradle 추가

```groovy
// redis -> java로 redis control
    implementation 'redis.clients:jedis:5.1.0'

    //jasypt
    implementation 'com.github.ulisesbocchio:jasypt-spring-boot-starter:3.0.5'
    implementation 'javax.xml.bind:jaxb-api:2.3.1'

    // validation
    implementation 'org.springframework.boot:spring-boot-starter-validation'


    //assertions for testJasyptConfig
    implementation 'org.assertj:assertj-core:3.19.0'
    //test for testJasyptConfig
    implementation 'org.junit.jupiter:junit-jupiter-api:5.8.1'
    testRuntimeOnly 'org.junit.jupiter:junit-jupiter-engine:5.8.1'
```

### Jasypt Config

- 아까 이메일 보낼 email Address, 생성한 앱 비밀번호를 yaml에서 암호화해서 관리하기 위해 필요함
- Jasypt secret key: 이메일 주소, 앱 비밀번호 등을 암호화하기 위해 필요한 비밀번호
- 암호화하는 메소드 `stringEncryptor`
  - 암호화 비밀번호
  - 어떤 알고리즘 쓸건지
  - 반복할 해싱 회수
  - salt 생성 클래스
  - 인코딩 방식

```java
import com.ulisesbocchio.jasyptspringboot.annotation.EnableEncryptableProperties;
import org.jasypt.encryption.StringEncryptor;
import org.jasypt.encryption.pbe.PooledPBEStringEncryptor;
import org.jasypt.encryption.pbe.config.SimpleStringPBEConfig;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
@EnableEncryptableProperties
public class JasyptConfig {
    @Value(value= "${jasypt.encryptor.password}")
    private String PASSWORD_KEY;

    @Bean(name= "jasyptStringEncryptor")
    public StringEncryptor stringEncryptor(){
        PooledPBEStringEncryptor encryptor= new PooledPBEStringEncryptor();
        SimpleStringPBEConfig config= new SimpleStringPBEConfig();
        config.setPassword(PASSWORD_KEY);
        config.setAlgorithm("PBEWithMD5AndDES");
        config.setKeyObtentionIterations("1000");  // 반복할 해싱 횟수
        config.setPoolSize("1"); // 암호화 인스턴스 pool
        config.setProviderName("SunJCE");
        config.setSaltGeneratorClassName("org.jasypt.salt.RandomSaltGenerator"); // salt 생성 클래스
        config.setStringOutputType("base64"); // 인코딩 방식
        encryptor.setConfig(config);
        return encryptor;
    }

}

```

### application.yaml

PBEWithMD5AndDES encryption 제공하는 사이트에서 암호화 <br>
<https://devglan.com/onaline-tools/jasypt-online-encryption-decryption>

<br>
또는 `JasyptConfigTest ` 에서 System.out.println해서 암호화해도 된다. <br>
암호화한 email Address, 생성한 앱 비밀번호를 ENC()로 감싸서 넣어둠 <br>

```yaml

  data:
    redis:
      host: localhost
      port: 6379

jasypt:
  encryptor:
    password: ${JASYPT_SECRET_KEY} //환경변수
    bean: jasyptStringEncryptor

email:
  address: ENC(암호화해서 쓰기)
  app-password: ENC(암호화해서 쓰기)



jwtpassword:
  source: ENC(jwtpassword암호화해서 쓰기)
```

⭐️⭐️⭐️ 여기까지 하고 테스트하면 메일이 발송되어야 한다.

## ✅ Redis

### Redis 설치

<https://soheeparklee.github.io/posts/Redis-gitCommands/>
<br>

### EmailCheckRequest DTO 생성

유저가 인증번호 받은 후, 이 인증번호를 확인할 때 쓰는 DTO
Validation을 사용해 유효성 검사

```java
@Data
public class EmailCheckRequest {
    @Email
    @NotEmpty(message = "이메일 형식을 확인해주세요.")
    private String email;

    @NotEmpty(message = "인증 번호를 입력해 주세요.")
    private String authNum;
}
```

### checkAuthNum Controller 메소드를 EmailCertificationController에 추가

```java
@RestController
@RequiredArgsConstructor
@RequestMapping("/mail")
public class EmailCertificationController {

    private final EmailCertificationService emailCertificationService;
    private final RedisUtil redisUtil;

    @PostMapping("/send-mail")
    public String sendMail(@RequestBody @Valid EmailRequest emailRequest) {
        System.out.println("이메일 인증 이메일 : " + emailRequest.getEmail());
        return emailCertificationService.joinEmail(emailRequest.getEmail());
    }

// checkAuthNum Controller 추가
    @PostMapping("/check-auth-num")
    public String checkAuthNum(@RequestBody @Valid EmailCheckRequest emailCheckRequest) {
        Boolean checked = emailCertificationService.checkAuthNum(emailCheckRequest.getEmail(), emailCheckRequest.getAuthNum());
        if (checked) {
            return "OK";
        }else {
						// exception은 custom 하여 사용중
            throw new BadRequestException("잘못된 인증 번호 입니다.", emailCheckRequest.getAuthNum());
        }
    }
}
```

### RedisUtil

지정된 key에 해당하는 데이터를 Redis에서 가져오고, 저장하고 <br>
지정된 시간 후에는 데이터 만료, 그리고 삭제까지 <br>

```java
import lombok.RequiredArgsConstructor;
import org.springframework.data.redis.core.StringRedisTemplate;
import org.springframework.data.redis.core.ValueOperations;
import org.springframework.stereotype.Service;

import java.time.Duration;

@Service
@RequiredArgsConstructor
public class RedisUtil {
    private final StringRedisTemplate redisTemplate; // Redis에 접근하기 위한 Spring의 Redis 탬플릿 클래스

    public String getData(String key){ // 지정된 key에 해당하는 데이터를 Redis에서 가져오는 메서드
        ValueOperations<String, String> valueOperations= redisTemplate.opsForValue();
        return valueOperations.get(key);
    }

    public void setData(String key, String value){ // 지정된 key에 값을 저장하는 메서드
        ValueOperations<String, String> valueOperations= redisTemplate.opsForValue();
        valueOperations.set(key, value);
    }

    public void setDataExpire(String key, String value, long duration){ // 지정된 key에 값을 지정하고, 지정된 시간 후에 데이터가 만료되도록 설정하는 메서드
        ValueOperations<String, String> valueOperations= redisTemplate.opsForValue();
        Duration expireDuration= Duration.ofSeconds(duration);
        valueOperations.set(key, value, expireDuration);
    }

    public void deleteData(String key){ // 지정된 key 에 해당하는 데이터를 Redis에서 삭제하는 메서드
        redisTemplate.delete(key);
    }

}

```

## ✅ Exceptions

인증번호 틀리면 BadReqeustException 발생<br>

### ExceptionControllerAdvice

```java
import lombok.extern.slf4j.Slf4j;
import org.shoppingMall.service.exceptions.*;
import org.shoppingMall.web.DTO.email.ErrorResponse;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.ResponseStatus;
import org.springframework.web.bind.annotation.RestControllerAdvice;

@RestControllerAdvice
@Slf4j
public class ExceptionControllerAdvice {

    @ResponseStatus(HttpStatus.BAD_REQUEST) //BadRequestException 가져올 떄 직접 만든 것으로 가져오기 주의, java원래 클래스 가져오면 에러
    @ExceptionHandler(BadRequestException.class)
    public ResponseEntity<ErrorResponse> handleBadRequestException(BadRequestException bre){
        log.error("Bad Request Exception: "+ bre.getMessage());
        ErrorResponse errorResponse= new ErrorResponse(400, "Bad Request Exception", bre.getDetailMessage(), bre.getRequest());
        return new ResponseEntity<>(errorResponse, HttpStatus.BAD_REQUEST);
    }
}

```

### BadReqeustException extends RunTimeException

```java
@Getter
public class BadRequestException extends RuntimeException{
    private String detailMessage;
    private Object request;

    public BadRequestException(String detailMessage, Object request) {
        this.detailMessage = detailMessage;
        this.request = request;
    }
}
```

### ErrorResponse DTO

```java
@Getter
@AllArgsConstructor
public class ErrorResponse {
    private Integer code;
    private String message;
    private String detailMessage;
    private Object request;
}

```

## ✅ 마지막으로 EmailCertificationService에 인증 로직 추가

```java
import lombok.RequiredArgsConstructor;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.mail.javamail.JavaMailSender;
import org.springframework.mail.javamail.MimeMessageHelper;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

import javax.mail.MessagingException;
import javax.mail.internet.MimeMessage;

import static org.shoppingMall.config.certification.EmailCertificationConfig.generateRandomNumber;

@Service
@RequiredArgsConstructor
public class EmailCertificationService {
    private final JavaMailSender mailSender;
    private final RedisUtil redisUtil;

    private final int authNumber= generateRandomNumber(100000, 999999); // config 에 미리 만들어둔 메서드
    @Value("${email.address}")
    private String emailAddress; // email-config에 설정한 자신의 이메일 주소를 입력
    public String joinEmail(String email) {
        String setFrom= emailAddress;
        String toMail= email;
        String title= "[인증]OOO사이트 가입 인증번호";
        String content=
                "회원가입 창으로 돌아가 인증 번호를 정확히 입력해주세요." + 	//html 형식으로 작성 !
                        "<br><br>" +
                        "인증 번호는 " + authNumber + "입니다." +
                        "<br>" ; //이메일 내용 삽입
        mailSend(setFrom, toMail, title, content);
        return Integer.toString(authNumber);
    }

    @Transactional
    public void mailSend(String setFrom, String toMail, String title, String content) {
        MimeMessage message= mailSender.createMimeMessage(); //JavaMailSender 객체를 사용하여 MimeMessage 객체를 생성
        try{
            MimeMessageHelper helper= new MimeMessageHelper(message, true, "utf-8"); //이메일 메시지와 관련된 설정을 수행합니다.
            // true를 전달하여 multipart 형식의 메시지를 지원하고, "utf-8"을 전달하여 문자 인코딩을 설정
            helper.setFrom(setFrom); //이메일의 발신자 주소 설정
            helper.setTo(toMail); //이메일의 수신자 주소 설정
            helper.setSubject(title); //이메일의 제목을 설정
            helper.setText(content, true);
            mailSender.send(message); //이메일의 내용 설정 두 번째 매개 변수에 true를 설정하여 html 설정으로한다.
            //redis에 인증번호 저장 로직 추가
            redisUtil.setDataExpire(Integer.toString(authNumber), toMail, 60*5L); // redis에 데이터 저장 // 유효기간 5분
        }catch(MessagingException e){ //이메일 서버에 연결할 수 없거나, 잘못된 이메일 주소를 사용하거나, 인증 오류가 발생하는 등 오류
            // 이러한 경우 MessagingException이 발생
            e.printStackTrace(); //e.printStackTrace()는 예외를 기본 오류 스트림에 출력하는 메서드

        }
    }

    public Boolean checkAuthNum(String email, String authNum) {
        if(redisUtil.getData(authNum) == null) return false;
        else if (redisUtil.getData(authNum).equals(email)) return true;
        else return false;
    }
}

```

### Redis Config??? 필요가 없었다......
