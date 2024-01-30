---
title: 스프링 보안코드 환경 변수로 숨기기
categories: [JAVA, Spring]
tags: [configurationproperty, value] # TAG names should always be lowercase
---

## 💡 Spring 설정 값 넣는 방법(외부에서 값을 주입할 때)

1️⃣ @ConfigurationPropoerties <br>
여러개의 값 숨기기<br>
새로운 파일 만들어서 설정해야 하고<br>
게터세터 꼭 필요<br>
2️⃣ @Value<br>
application.yaml에 한 두개의 값 가져올 때<br>
좀 더 간단히<br>

## ✅ dataSource 숨기기(1️⃣ @ConfigurationPropoerties)

```java
//JdbcConfig 기존 코드
//👎🏻 JdbcConfig에 이런식으로 setUsername, setPassword 다 보임!!!
@Configuration
public class JdbcConfig {
    //db 연결
    @Bean
    public DataSource dataSourceItem(){
        DriverManagerDataSource dataSource= new DriverManagerDataSource();
        dataSource.setUsername("root");
        dataSource.setPassword("12341234");
        dataSource.setDriverClassName("com.mysql.cj.jdbc.Driver");
        dataSource.setUrl("jdbc:mysql://localhost:3306/crud_chap_96?useUnicode=true&characterEncoding=UTF-8");
        return dataSource;
    }
}

// application.yaml에서 숨기기
//이렇게 아까 JdbcConfig있던 비밀 정보를 application.yaml에 넣는다.
datasource:
  username: ${DATABASE_USERNAME}
  password: ${DATABASE_PASSWORD}
  driver-class-name: com.mysql.cj.jdbc.Driver
  url: jdbc:mysql://localhost:3306/crud_chap_96?useUnicode=true&characterEncoding=UTF-8

//⭐️ 그리고 username, password는 환경변수로 추가
//edit configuration- modify options- environmental variables

//새로운 파일 DataSourceProperty추가
//@ConfigurationProperties(prefix= "datasource") 어노테이션 추가해주어야 한다.
@Getter
@Setter
@ConfigurationProperties(prefix= "datasource")
public class DataSourceProperty {
    private String username;
    private String password;
    private String driverClassName;
    private String url;
}

// 👍🏻 DataSource수정
//어노테이션으로 EnableConfigurationProperties를 추가해주어야 한다.
@Configuration
@EnableConfigurationProperties(DataSourceProperty.class)
@RequiredArgsConstructor
public class JdbcConfig {
    private final DataSourceProperty dataSourceProperty;

    //db 연결
    @Bean
    public DataSource dataSourceItem(){
      // 👍🏻 이제 정보 안 보이고, dataSourceProperty에서 getter로 가져오는 형태
        DriverManagerDataSource dataSource= new DriverManagerDataSource();
        dataSource.setUsername(dataSourceProperty.getUsername());
        dataSource.setPassword(dataSourceProperty.getPassword());
        dataSource.setDriverClassName(dataSourceProperty.getDriverClassName());
        dataSource.setUrl(dataSourceProperty.getUrl());
        return dataSource;
    }
}

```

## ⭐️ environment variable 환경변수 추가하기

<img width="1035" alt="스크린샷 2024-01-23 오후 1 41 25" src="https://github.com/supercoding-project-be-1/backend-crud1/assets/97790983/03ba67ee-f066-4d64-b873-2ed0b4d561e6">

## ✅ secretKey 숨기기(2️⃣ @Value)

```java
// 👎🏻 JwtTokenProvider에 secretKey다 보인다!!!
@RequiredArgsConstructor
@Component
public class JwtTokenProvider {
    //암호화되는 JwtToken을 풀 수 있는 Signature
    private final String secretKey = Base64.getEncoder().encodeToString("sohee-password".getBytes());
}

// secretKeySource라는 변수를 추하한다.
//secretKey에 대한 로직은 @PostConstruct안에 쓴다.
//값을 가져오는 순서와 component가 만들어지는 순서를 꼬이지 않게 하기 위해서
@RequiredArgsConstructor
@Component
public class JwtTokenProvider {
    //암호화되는 JwtToken을 풀 수 있는 Signature
    @Value("${jwt.secret-key-source}")
    private String secretKeySource;
    private String secretKey;


    //jwt secret key를 가져오는 과정에서 순서 차이가 발생해 NullPointException발생
    //@PostConstruct: component들이 다 construct된 이후 post에 다음 코드를 실행해주세요
    @PostConstruct
    public void setUp(){
            secretKey=  Base64.getEncoder().encodeToString(secretKeySource.getBytes());
    }
}

//아까는 새로운 파일을 만들었다면, 이번에는 한 개의 값만 숨기면 되니까 그냥 @Value로 값 넣기
//그리고 환경변수 추가

```

## ⭐️ environment variable 환경변수 추가하기

<img width="1229" alt="스크린샷 2024-01-23 오후 5 36 02" src="https://github.com/supercoding-project-be-1/backend-crud1/assets/97790983/aa655f65-af7c-4418-b833-1ec00ef7b569">
