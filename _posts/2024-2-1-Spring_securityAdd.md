---
title: Spring Security
categories: [JAVA, Spring]
tags: [security] # TAG names should always be lowercase
---

한솔이 노션
https://boulder-hippodraco-244.notion.site/Spring-Security-5c96bcae888547ce98d526f0e1901d34

## ☑️ user, roles, user DB setting 및 JPA setting

### 1. DB schema setting

- user table
- roles table
- user_role table

### 2. JPA setting

#### ✅ build.gradle

```java

plugins {
    id 'java'
    id 'org.springframework.boot' version '3.2.2'
    id 'io.spring.dependency-management' version '1.1.4'
}

group = 'com.example'
version = '0.0.1-SNAPSHOT'

java {
    sourceCompatibility = '17'
}

repositories {
    mavenCentral()
}

dependencies {
    implementation 'org.springframework.boot:spring-boot-starter'
    testImplementation 'org.springframework.boot:spring-boot-starter-test'
    implementation 'org.springframework.boot:spring-boot-starter-web'
    //lombok사용
    compileOnly 'org.projectlombok:lombok'
    annotationProcessor 'org.projectlombok:lombok'
    //Mapstruct
    implementation 'org.mapstruct:mapstruct:1.5.5.Final'
    annotationProcessor 'org.mapstruct:mapstruct-processor:1.5.5.Final'
    //Swagger
    implementation 'io.springfox:springfox-swagger-ui:3.0.0'
    implementation 'io.springfox:springfox-swagger2:3.0.0'
    implementation 'org.springdoc:springdoc-openapi-starter-webmvc-ui:2.0.2'
    //env-hide
    annotationProcessor 'org.springframework.boot:spring-boot-configuration-processor'
    //mariadb
    implementation 'org.mariadb.jdbc:mariadb-java-client:3.1.4'
    //JPA
    implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
    //jwt
    implementation 'io.jsonwebtoken:jjwt:0.9.1'

    //security
//    implementation 'org.springframework.boot:spring-boot-starter-security'
//    //javax.xml.bind.DatatypeConverter 에러나서 해야됨⬇️
//    implementation 'javax.xml.bind:jaxb-api:2.3.1'


    runtimeOnly 'mysql:mysql-connector-java:8.0.26'

    //security 무슨 에러 난다는거지?
    implementation 'org.springframework.boot:spring-boot-starter-security'

}

tasks.named('test') {
    useJUnitPlatform()
}

```

#### ✅ application.yaml

```java
spring:
  mvc:
    pathmatch:
      matching-strategy: ant_path_matcher

datasource:
  username: ${DATABASE_USERNAME}
  password: ${DATABASE_PASSWORD}
  driver-class-name: com.mysql.cj.jdbc.Driver
  url: jdbc:mysql://localhost:3306/BackEndProject_2_verSoh?useUnicode=true&characterEncoding=UTF-8

  jpa:
    show-sql: true

jwtpassword:
  source: ${JWT_SECRET_KEY}

  logging:
    level:
      org.hibernate.SQL: debug
```

#### ✅ JPAConfig

```java
package com.example.supercoding2stsohee.config;
import com.example.supercoding2stsohee.config.properties.DataSourceProperties;
import jakarta.persistence.EntityManagerFactory;
import lombok.RequiredArgsConstructor;
import org.springframework.boot.autoconfigure.domain.EntityScan;
import org.springframework.boot.context.properties.EnableConfigurationProperties;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.data.jpa.repository.config.EnableJpaRepositories;
import org.springframework.jdbc.datasource.DriverManagerDataSource;
import org.springframework.orm.jpa.JpaTransactionManager;
import org.springframework.orm.jpa.JpaVendorAdapter;
import org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean;
import org.springframework.orm.jpa.vendor.HibernateJpaVendorAdapter;
import org.springframework.transaction.PlatformTransactionManager;

import javax.sql.DataSource;
import java.util.HashMap;
import java.util.Map;

@Configuration
@EntityScan
@EnableConfigurationProperties(DataSourceProperties.class)
@RequiredArgsConstructor
@EnableJpaRepositories(
        basePackages = {"com.example.supercoding2stsohee.repository.cart",
                "com.example.supercoding2stsohee.repository.orderItem",
                "com.example.supercoding2stsohee.repository.orderTable",
                "com.example.supercoding2stsohee.repository.product",
                "com.example.supercoding2stsohee.repository.productOption",
                "com.example.supercoding2stsohee.repository.productPhoto",
                "com.example.supercoding2stsohee.repository.review",
                "com.example.supercoding2stsohee.repository.roles",
                "com.example.supercoding2stsohee.repository.userRoles",
                "com.example.supercoding2stsohee.repository.user"
        },
        entityManagerFactoryRef = "localContainerEntityManagerFactoryBean",
        transactionManagerRef = "tm"
)
public class JpaConfig {
    private final DataSourceProperties dataSourceProperties;

    @Bean
    public DataSource dataSource() {
        DriverManagerDataSource driverManagerDataSource = new DriverManagerDataSource();
        driverManagerDataSource.setUrl(dataSourceProperties.getUrl());
        driverManagerDataSource.setUsername(dataSourceProperties.getUsername());
        driverManagerDataSource.setPassword(dataSourceProperties.getPassword());
        driverManagerDataSource.setDriverClassName(dataSourceProperties.getDriverClassName());
        return driverManagerDataSource;
    }

    @Bean
    public LocalContainerEntityManagerFactoryBean localContainerEntityManagerFactoryBean(DataSource datasource) {
        LocalContainerEntityManagerFactoryBean lemfb = new LocalContainerEntityManagerFactoryBean();
        lemfb.setDataSource(datasource);
        lemfb.setPackagesToScan(
                "com.example.supercoding2stsohee.repository.cart",
                "com.example.supercoding2stsohee.repository.orderItem",
                "com.example.supercoding2stsohee.repository.orderTable",
                "com.example.supercoding2stsohee.repository.product",
                "com.example.supercoding2stsohee.repository.productOption",
                "com.example.supercoding2stsohee.repository.productPhoto",
                "com.example.supercoding2stsohee.repository.review",
                "com.example.supercoding2stsohee.repository.roles",
                "com.example.supercoding2stsohee.repository.userRoles",
                "com.example.supercoding2stsohee.repository.user"
        );
        JpaVendorAdapter vendorAdapter = new HibernateJpaVendorAdapter();
        lemfb.setJpaVendorAdapter(vendorAdapter);

        Map<String, Object> properties = new HashMap<>();
        properties.put("hibernate.dialect", "org.hibernate.dialect.MariaDBDialect");
        properties.put("hibernate.format_sql", "true");
        properties.put("hibernate.use_sql_comment", "true");

        lemfb.setJpaPropertyMap(properties);

        return lemfb;
    }

    @Bean(name = "tm")
    public PlatformTransactionManager platformTransactionManager(EntityManagerFactory entityManagerFactory) {
        return new JpaTransactionManager(entityManagerFactory);
    }
}

```

#### ✅ DataSourceProperties

```java
package com.example.supercoding2stsohee.config.properties;

import lombok.Getter;
import lombok.Setter;
import org.springframework.boot.context.properties.ConfigurationProperties;

@Getter
@Setter
@ConfigurationProperties(prefix = "datasource")
public class DataSourceProperties {
    private String username;
    private String password;
    private String driverClassName;
    private String url;
}

```

### 3. Entity

#### ✅ User(Entity)

- memberRoles와 역방향 연결

```java
package com.example.supercoding2stsohee.repository.user;

import com.example.supercoding2stsohee.repository.userRoles.UserRoles;
import jakarta.persistence.*;
import lombok.*;

import java.time.LocalDateTime;
import java.util.List;

@Entity
@Getter
@Setter
@EqualsAndHashCode(of = "userId")
@Table(name = "user")
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "user_id")
    private Integer userId;

    @Column(name = "name", nullable = false)
    private String name;

    @Column(name = "phone_number", nullable = false)
    private String phoneNumber;

    @Column(name = "email", nullable = false)
    private String email;

    @Column(name = "nick_name", nullable = false)
    private String nickName;

    @Column(name = "password", nullable = false)
    private String password;

    @Column(name = "profile_img", nullable = false)
    private String profile_img;

    @Column(name = "address", nullable = false)
    private String address;

    @Column(name = "gender", nullable = false)
    private String gender;

    @Column(name = "status", nullable = false)
    private String status;

    @Column(name = "failure_count", nullable = false)
    private Integer failureCount;

    @Column(name = "create_at", nullable = false)
    private LocalDateTime createdAt;

    @Column(name = "delete_at")
    private LocalDateTime deletedAt;

    @Column(name = "lock_at")
    private LocalDateTime lockedAt;

    @OneToMany(mappedBy = "user", cascade = CascadeType.ALL, orphanRemoval = true) //cascade, orphanRemoval 추가해보았음
    private List<UserRoles> userRoles;
}

```

#### ✅ Roles(Entity)

```java
package com.example.supercoding2stsohee.repository.roles;

import jakarta.persistence.*;
import lombok.*;

@Entity
@Getter
@Setter
@EqualsAndHashCode(of = "roleId")
@Table(name = "roles")
public class Roles {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "roles_id")
    private Integer rolesId;

    @Column(name = "name", nullable = false)
    private String name;
}

```

#### ✅ UserRole(Entity)

```java
package com.example.supercoding2stsohee.repository.userRoles;

import com.example.supercoding2stsohee.repository.roles.Roles;
import com.example.supercoding2stsohee.repository.user.User;
import jakarta.persistence.*;
import lombok.Getter;
import lombok.Setter;

@Entity
@Getter
@Setter
@Table(name = "user_roles")
public class UserRoles {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "user_roles_id")
    private Integer userRolesId;

    @ManyToOne
    @JoinColumn(name = "user_id")
    private User user;

    @ManyToOne
    @JoinColumn(name = "roles_id")
    private Roles roles;

}

```

### 4. JPA

#### ✅ UserJpa

```java
package com.example.supercoding2stsohee.repository.user;

import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.data.jpa.repository.Query;
import org.springframework.stereotype.Repository;

import java.util.Optional;

@Repository
public interface UserJpa extends JpaRepository<User, Integer> {

    @Query(
            "SELECT u " +
                    "FROM User u " +
                    "JOIN FETCH u.userRoles ur " +
                    "JOIN FETCH ur.roles r " +
                    "WHERE u.email = ?1 "
    )

    Optional<User> findByEmailFetchJoin(String email);
}

```

#### ✅ RolesJpa

```java
package com.example.supercoding2stsohee.repository.roles;

import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface RolesJpa extends JpaRepository<Roles, Integer> {
}

```

#### ✅ UserRolesJpa

```java
package com.example.supercoding2stsohee.repository.userRoles;

import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface UserRolesJpa extends JpaRepository<UserRoles, Integer> {
}

```

## ☑️ Security setting

### 5. CustomuserDetails

    -CustomUserDetails는 implements UserDetails
    - 그래서 @Override 하면 된다.
    - JWT token에 대한 정보 설정
    - JWT token을 받을 형식
        - 권한 조회

```java
package com.example.supercoding2stsohee.repository.userDetails;

import lombok.*;
import org.springframework.security.core.GrantedAuthority;
import org.springframework.security.core.authority.SimpleGrantedAuthority;
import org.springframework.security.core.userdetails.UserDetails;

import java.util.Collection;
import java.util.List;
import java.util.stream.Collectors;

@Builder
@Getter
@AllArgsConstructor
@NoArgsConstructor
@ToString
public class CustomUserDetails implements UserDetails {
    @Getter
    private Integer userId;

    private String email;

    private String password;

    private List<String> authorities;

    @Override
    public Collection<? extends GrantedAuthority> getAuthorities() {
        return authorities.stream().map(SimpleGrantedAuthority::new).collect(Collectors.toList());
    }
    // email 과 password로 유저 인식
    @Override
    public String getPassword() {
        return this.password;
    }

    @Override
    public String getUsername() {
        return this.email;
    }

    @Override
    public boolean isAccountNonExpired() {
        return true;
    }

    @Override
    public boolean isAccountNonLocked() {
        return true;
    }

    @Override
    public boolean isCredentialsNonExpired() {
        return true;
    }

    @Override
    public boolean isEnabled() {
        return true;
    }
}

```

### 6. CustomUserDetailService setting

    - loadUserByUsername(): UserJpa에서 이메일로 User 정보를 찾아오고 이를 CustomUserDetails에 builder로 넣어준다.
        - UserJpa에서 이메일로 User 정보를 찾기 위해 findByEmailFetchJoin()
        - findByEmailFetchJoin()은 JPA에 내장된 함수가 아니니까 @Query로 함수를 정의해 준다.

```java
package com.example.supercoding2stsohee.service.security;

import com.example.supercoding2stsohee.repository.roles.Roles;
import com.example.supercoding2stsohee.repository.user.User;
import com.example.supercoding2stsohee.repository.user.UserJpa;
import com.example.supercoding2stsohee.repository.userDetails.CustomUserDetails;
import com.example.supercoding2stsohee.repository.userRoles.UserRoles;
import com.example.supercoding2stsohee.service.exceptions.NullPointerException;
import lombok.RequiredArgsConstructor;
import org.springframework.context.annotation.Primary;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.core.userdetails.UsernameNotFoundException;
import org.springframework.stereotype.Service;

import java.util.stream.Collectors;

@Service
@RequiredArgsConstructor
@Primary //이 bean이 default
public class CustomUserDetailService implements UserDetailsService {

    private final UserJpa userJpa;

    @Override
    public UserDetails loadUserByUsername(String email) throws UsernameNotFoundException {
        User user = userJpa.findByEmailFetchJoin(email)
                .orElseThrow(()-> new NullPointerException("email에 해당하는 user를 찾을 수 없습니다."));

        // 해당 user의 email 로 조회한 정보를 CustomUserDetails repository에 빌더로 넣어준다.

        return CustomUserDetails.builder()
                .userId(user.getUserId())
                .email(user.getEmail())
                .password(user.getPassword())
                .authorities(user.getUserRoles().stream().map(UserRoles::getRoles).map(Roles::getName).collect(Collectors.toList()))
                .build();
    }
}

```

### 7. JWTAuthenticationFilter

    doFilterInternal(): request, response, filterChain을 받아
    JWT를 쪼개서
    - resolveToken : token에서 원하는 정보 가져오기
    - JWT가 Null이 아니고 validateToken 토큰이 유효한지 검사
    - getAuthentication : JwtTokenProvider에서 권한 가져오기
    SecurityContextHolder의 context에 권한 auth를 set 한다.

```java
package com.example.supercoding2stsohee.web.filters;

import com.example.supercoding2stsohee.config.security.JwtTokenProvider;
import jakarta.servlet.FilterChain;
import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;
import lombok.RequiredArgsConstructor;
import org.springframework.security.core.Authentication;
import org.springframework.security.core.context.SecurityContextHolder;
import org.springframework.web.filter.OncePerRequestFilter;

import java.io.IOException;
@RequiredArgsConstructor
public class JwtAuthenticationFilter extends OncePerRequestFilter {
    private final JwtTokenProvider jwtTokenProvider;
    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain) throws ServletException, IOException {
        String jwtToken= jwtTokenProvider.resolveToken(request); // Token 에서 원하는 정보를 가져오기
        if(jwtToken != null && jwtTokenProvider.validateToken(jwtToken)){ // jwtToken 이 존재하고 유효하다면
            Authentication auth= jwtTokenProvider.getAuthentication(jwtToken); // jwtTokenProvider 에서 권한을 가져오고
            SecurityContextHolder.getContext().setAuthentication(auth); // SecurityContextHolder.getContext() 에 auth 를 넣어준다.
        }
        filterChain.doFilter(request, response);
    }
}

```

### 8. JwtTokenProvider

    - JWTAuthenticationFilter에서 사용한 메소드를 구현

        - resolveToken
        - validateToken
        - getAuthentication
    - 그리고 createToken

```java
package com.example.supercoding2stsohee.config.security;

import com.example.supercoding2stsohee.service.security.CustomUserDetailService;
import io.jsonwebtoken.Claims;
import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.SignatureAlgorithm;
import jakarta.annotation.PostConstruct;
import jakarta.servlet.http.HttpServletRequest;
import lombok.RequiredArgsConstructor;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.security.authentication.UsernamePasswordAuthenticationToken;
import org.springframework.security.core.Authentication;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.stereotype.Component;

import java.util.Base64;
import java.util.Date;
import java.util.List;

@Component
@RequiredArgsConstructor
public class JwtTokenProvider {

    private final UserDetailsService userDetailsService;

    @Value("${jwtpassword.source}")
    private String secretKey;
    private String key;

    @PostConstruct
    public void setUp(){  // JWT_SECRET_KEY를 인코딩
        key= Base64.getEncoder().encodeToString(secretKey.getBytes());
    }
    private long tokenValidMillisecond= 1000L * 60 * 60; //Token이 유효한 시간 1시간
    public String resolveToken(HttpServletRequest request) {
        return request.getHeader("Token");
    }

    public String createToken(String email, List<String> roles){ // 토큰 생성
        Claims claims= Jwts.claims().setSubject(email);
        claims.put("roles", roles);
        Date now= new Date();
        return Jwts.builder()
                .setClaims(claims)
                .setIssuedAt(now)
                .setExpiration(new Date(now.getTime() + tokenValidMillisecond))
                .signWith(SignatureAlgorithm.HS256, key)
                .compact();
    }

    public boolean validateToken(String jwtToken) {
        try{
            Claims claims= Jwts.parser().setSigningKey(key).parseClaimsJws(jwtToken).getBody();
            Date now= new Date();
            return !claims.getExpiration().before(now);
        } catch(Exception e){
            return false;
        }
    }

    public Authentication getAuthentication(String jwtToken) {
        UserDetails userDetails = userDetailsService.loadUserByUsername(getUserEmail(jwtToken));
        return new UsernamePasswordAuthenticationToken(userDetails, "", userDetails.getAuthorities());
    }
    public String getUserEmail(String jwtToken){
        return Jwts.parser().setSigningKey(key).parseClaimsJws(jwtToken).getBody().getSubject();
    }
}

```

## ☑️ SignController, AuthService, SecurityConfig, PasswordEncoderConfig

### 9. SignController

```java

```

### 10. AuthService

```java

```

### 11. PasswordEncoderConfig

```java

```

## ☑️ Login 로직 추가

### (추가) SignController

```java

```

### 12. LoginRequest(DTO)

```java

```

### (추가) AuthService(loginService 추가)

```java

```

### 13. SecurityConfig

```java

```

## ☑️ 권한 설정

### (추가) SecurityConfig(authorizeRequests 추가)

```java

```

## ☑️ Token 관련 excpetion 설정

- CustomAccessDeniedHandler
- CustomAuthenticationEntryPoint
- ExcpetionController
- (추가) SecurityConfig의 SecurityFilterChain에 exceptionHandling 추가

```java

```

## ☑️ TEST 코드에서 CustomerMemberDetails 사용

- TestController
- POSTMAN 으로 로그인 후 Token을 TEST 코드에 넣어주면

```java

```
