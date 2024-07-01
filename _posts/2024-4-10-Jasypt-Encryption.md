---
title: Jasypt_encryption
categories: [JAVA, Spring]
tags: [redis. jasypt] # TAG names should always be lowercase
---

## ✅ Background Knowledge

### 💡 Jasypt:

> Java Simplified Encryption
> Java library that provides simple APIs for encryption and decryption of data, including hashing.

#### ✔️ 해싱이란?

> transforming text into charecters using a one-way cryptographic hash function

- one way cryptographic function
- results in hash value/hash code
- **irreversable**
- MD5, SHA-1, SHA-256

🆚 Encryption <br>

- eversible cryptographic process
- encrypts with an algorithm and a key
- AES, DES, RSA

#### ✔️ Salt?

> "salt" is random data that is used as an additional input to a hash function along with the plain text being hashed

- thanks to salt, we can defend against attacks and add complexity to the hashing process.
- When hashing a password or any other sensitive data, you can provide a salt along with the data.
- The salt is then combined with the data before hashing, resulting in a unique hash for each input even if the original data is the same.

#### ✔️ 인코딩?

> process of transforming data into a format that is suitable for a particular type of transmission or storage system

- GOAL: make sure data can be represented and transmitted properly
- Base64, hexadecimal, URL encoding

🆚 Encryption <br>

- GOAL: protect data, data confidentiality

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
    <br>
- salt 생성 클래스를 지정하지 않으면 default로: `RandomSaltGenerator`
- 고정된 salt 값을 사용하려면 `StringFixedSaltGenerator`를 사용하면 된다
- 단 이 경우 복호화시에도 기존에 설정한 salt 값 사용해야지만 복호화 가능

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

<img width="355" alt="image" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/c5740158-3185-4e00-a34f-94aba087ff20">

<br>
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

완성된 yaml파일은 다음과 같이 생겼을 것이다.

```yaml
server: port:8080

spring:
  mvc:
    pathmatch:
      matching-strategy: ant_path_matcher

  autoconfigure: exclude:org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration

  datasource:
    username: ENC(dg0o6RGGnI5v2NTvYqiCeA==)
    password: ENC(3S04ny0whtz9bZ4PvLkMuIFXmnRB0pjy)
    driver-class-name: org.mariadb.jdbc.Driver
    #  url: jdbc:mariadb://sohan2.c7suy242wrpp.eu-west-1.rds.amazonaws.com:3306/shopping_mall?useUnicode=true&characterEncoding=UTF-8
    url: jdbc:mariadb://localhost:3306/BackEndProject_2_verSoh?useUnicode=true&characterEncoding=UTF-8

  jpa:
    show-sql: true

  data:
    redis:
      host: localhost
      port: 6379

jasypt:
  encryptor:
    password: ${JASYPT_SECRET_KEY}
    bean: jasyptStringEncryptor

email:
  address: ENC(9FFPzV1CpODhRFqWQPJg6RDj9yuVaV4jnT0FQvc4oE0=)
  app-password: ENC(3ViVckG3lnbAeZWKhkWT06ChwI8rfEazJBqXJL5fBak=)

jwtpassword:
  source: ENC(/CzryCVnQTpLw20DGA4M7ENiN+eg+PDQ)

  logging:
    level: debug
```

#### 🔴 TroubleShooting

`jwtpassword:`또한 `ENC()`로 감싸서 암호화했더니, `jwtTokenProvider`에 문제가 있다고 error가 발생했다. <br>
위 `yaml`처럼 바꿔줄거면, 마찬가지로 `jwtTokenProvider`파일에서 `jwtpassword:`또한 수정해 주어야 한다. <br>
`yaml`파일에 어디를 보면 되는지를 알려주어야 함. <br>
jwtpassword 의 source를 보렴! <br>

```java
@Component
@RequiredArgsConstructor
public class JwtTokenProvider {
    private final UserDetailsService userDetailsService;
//    @Value("${JWT_SECRET_KEY}") //수정 전
    @Value("${jwtpassword.source}") //수정 후
    private String secretKey;
    private String key;

    //JwtTokenProvider methods...
}
```

### ➕ `JasyptConfigTest` 에서 암호화

또는 `JasyptConfigTest ` 에서 System.out.println해서 암호화해도 된다. <br>
위 사이트에서 암호화했으면 이 파일 없어도 됨. <br>

```java
import org.assertj.core.api.Assertions;
import org.jasypt.encryption.pbe.StandardPBEStringEncryptor;
import org.junit.jupiter.api.Test;

public class JasyptConfigTest {

    @Test
    void jasypt(){
        String url= "db주소";
        String username= "네임";
        String password= "비밀번호";

        String encryptUrl= jasyptEncrypt(url);
        String encryptUsername= jasyptEncrypt(username);
        String encryptPassword= jasyptEncrypt(password);

        System.out.println("encryptUrl : " + encryptUrl);
        System.out.println("encryptUrl : " + encryptUsername);
        System.out.println("encryptPassword : " + encryptPassword);

        Assertions.assertThat(url).isEqualTo(jasyptDecrypt(encryptUrl));
    }

    private String jasyptEncrypt(String input){
        String key= "cesarpoo";
        StandardPBEStringEncryptor encryptor= new StandardPBEStringEncryptor();
        encryptor.setAlgorithm("PBEWithMD5AndDES");
        encryptor.setPassword(key);
        return encryptor.encrypt(input);
    }

    private String jasyptDecrypt(String input){
        String key= "cesarpoo";
        StandardPBEStringEncryptor encryptor= new StandardPBEStringEncryptor();
        encryptor.setAlgorithm("PBEWithMD5AndDES");
        encryptor.setPassword(key);
        return encryptor.decrypt(input);
    }


}
```

## ✅ Run redis server on EC2

### Redis server install

<img width="791" alt="Screenshot 2024-06-16 at 15 29 10" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/7b9f66d1-b25d-40cf-abca-5f22b59fae90">

<img width="587" alt="Screenshot 2024-06-16 at 15 29 28" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/c685857e-b946-4ab3-ba59-f7aa1561a77e">

### 서버 시작하는 명령어

```bash
sudo systemctl start redis
```

### 서버 상태 확인하는 명령어

```bash
sudo systemctl status redis
```

### redis.conf

1. Redis.conf에 들어가서

```bash
sudo nano /etc/redis/redis.conf
```

- 비밀번호 바꾸기(참고자료)
- protected-mode 바꾸기

```bash
protected-mode no

```

- 서버 바꾸기

```bash
bind 0.0.0.0
```

2. 방화벽 풀어주기

```bash
sudo ufw allow 6379
```

### 서버 재시작 명령어

```bash
sudo systemctl restart redis
```

### 포트 6379 열기

redis는 보통 포트 6379에서 실행된다.

```bash
sudo netstat -tuln | grep 6379
```

### EC2와 연결된 redis서버 연결

```bash
redis-cli -h {{public IP}} -p 6379 -a {{위에서 설정한 비밀번호}}
```

### 💡 참고

<https://wookgu.tistory.com/26>

## Redis Config??? 필요가 없었다......

## 💡 참고

```plaintext
https://velog.io/@jinny-l/spring-jasypt-encrypt-yml-and-store-encryption-key-as-environment-variable


-- 한솔이 블로그
https://boulder-hippodraco-244.notion.site/Email-Spring-Boot-3-2-52fa5aa2f1154691bd7c2a8fea3d89a6
```
