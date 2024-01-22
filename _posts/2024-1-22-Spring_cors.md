---
title: XXS, CSRF, SQL injection, CORS
categories: [JAVA, Spring]
tags: [xxs, csrf, injection, cross, scripting, forgery] # TAG names should always be lowercase
---

## ✅ XXS

> Cross Site Scripting <br>
> 사용자가 **웹 페이지에 악성 스크립트를 삽입**하여 의도치 않은 명령을 하거나 해킹에 사용하는 것 <br>
> 상대방의 쿠키를 가져오기 <br>

삽입한 악성 스크립트로 쿠키를 빼가거나, 내가 원하지 않는 사이트로 접속하도록 만들 수 있음. <br>

### 💡 XXS 해결 방법

- 웹 페이지 작성 시 스크립트를 등록할 수 없도록 설정하기 <br>
- 중요 cookie HTTP ONLY 및 Secure 설정 <br>
  그래서 중요 cookie는 스크립트로도 쿠키를 빼갈 수 없도록 설정 <br>

## ✅ CSRF

> Cross Site Request Forgery <br>
> 사용자의 **섹션이나 토큰을 이용해 다른 명령**을 실행하도록 한다. <br>
> 상대방 쿠키는 상대방이 그대로 가지고 있고, 상대방에게 원하지 않은 get요청을 하도록 만들기 <br>

예를 들어 피싱 메일 <br>
메일을 받아서 클릭하면(get요청) 비밀번호가 바뀌어버리는 일이 발생할 수 있음. <br>

### 💡 CSRF 해결 방법

- HTTP Referer:Host이름 비교하고 확인하기 <br>
  해커(메일에서)가 비밀번호 바꾸려고 하는 것인지, 호스트가 비밀번호 바꾸려고 하는 것인지 확인 <br>
- CAPTCHA로 사람 실행 확인 <br>
  ~신호등이 나와 있는 사진 클릭하세요 <br>
  사람인지 확인하기 <br>

## ✅ SQL injection

> 서버로 보낼 때, 정상적인 요청값 대신 악의적인 DB SQL문을 주입하는 것<br>

에를 들어 아이디를 입력하는데 악의적인 DB SQL문 DELETE를 넣어버림. <br>
그러면 로그인하면 테이블이 변경되거나 삭제되어 버릴 수 있음! <br>
또는 사용자의 권한을 바꿔버린다던가... <br>

### 💡 SQL injection 웹 공격 방지 방법

- 여러 IF문으로 검증 로직 추가 <br>
  아이디는 DB SQL문을 사용할 수 없도록 <br>
- JPA를 사용하면 위협이 많이 낮아짐 <br>

## ✅ SOP

> 웹 브라우저의 동일 출처 정책 <br>
> SOP: Same Orgin Policy <br>
> prevent web pages from making **requests** to a different domain than the one that **served** the web page. <br>

- 같은 출처 정책 <br>
- 사이트 A를 가지고 있으면 사이트 A에서만 가지고 온다. <br>
- 앞서 언급된 보안 위험 등으로 브라우저는 기본적으로 SOP를 따른다. <br>
- 외부에서 얻는 데이터는 항상 같은 Orgin이어야 인식한다. <br>

### ⭐️ Orgin

> Protocol + Host + Port<br>

    이 세 가지까지 같으면 동일 origin출처<br>

> An "origin" is defined by the combination of the protocol (e.g., HTTP or HTTPS), domain, and port. Two pages are considered to have the same origin if all three components match. <br>

## ✅ CORS

> Cross Orgin Resource Sharing <br>
> 그래서 원래 Orgin이 다르면 그 Resource는 들고 올 수 없는데, 이 제한을 풀어주는 것 <br>

왜냐하면 프론트 서버와 백엔드 서버는 다를 수밖에 없는데, <br>
같은 서버에서 온 리소스만 받을 수 있다면 프론트와 백엔드는 소통할 수가 없음! <br>
프론트와 백엔드를 항상 서로 배포해야함... <br>
따라서 경우에 따라 SOP를 풀어주는 것도 필요하다. <br>

### 💡 CORS 방법

#### 1. 브라우저 플러그인<br>

    브라우저에 플러그인만 추가하면 쉽게 해결할 수 있지만, 문제는 새로운 기기가 추가될 떄마다 플러그인 일일이 추가해주어야 한다. <br>

#### 2. 백엔드 전역 보안 설정

```java
//safety configuation에 새로운 Bean 추가
    @Bean
    public CorsConfigurationSource corsConfigurationSource(){
        CorsConfiguration configuration= new CorsConfiguration();
        configuration.setAllowedOrigins(List.of("http://localhost:63342"));
        configuration.setAllowCredentials(true); //token을 주고받을 때 필요
        configuration.addExposedHeader("X-Auth-Token"); //token
        configuration.addAllowedHeader("*"); // header다 된다. wildcard *
        configuration.setAllowedMethods(Arrays.asList("GET", "PUT", "POST", "FETCH", "DELETE", "OPTIONS"));
        configuration.setMaxAge(3600L); //얼마나 오래동안 허용할 것인가 1시간

        UrlBasedCorsConfigurationSource source= new UrlBasedCorsConfigurationSource();
        source.registerCorsConfiguration("/**", configuration); //모든 api에 적용할거야
        return source;
    }

//그리고 같은 파일안에 있는 filterChain에 CORS추가
@Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception{
        //로그인 설정 구현
        http.headers().frameOptions().sameOrigin()
                .and()
                .formLogin().disable()
                .csrf().disable()
                .httpBasic().disable()
                //⭐️ CORS 허용
                .cors().configurationSource(corsConfigurationSource())
                .and()
                .rememberMe().disable() //아이디비번 기억하시겠습니까? disable
                .sessionManagement().sessionCreationPolicy(SessionCreationPolicy.STATELESS) //session 사용 disable
                .and() //여기서부터 role에 따라 항공 예약 시스템 접근 허용해주는 로직
                .authorizeRequests()
                    .antMatchers("/resources/static/**", "/v1/api/sign/*").permitAll() //로그인 안 했어도 허용
                    .antMatchers("/v1/api/air-reservation/tickets/*").hasRole("USER") //항공예약시스템은 USER만 접근 가능하다.
                .and()
                .exceptionHandling() // 여기서부터 예외처리
                .authenticationEntryPoint(new CustomAuthenticationEntryPoint()) //인증실패
                .accessDeniedHandler(new CustomerAccessDeniedHandler()) //인가 실패
                .and()
                //여기서부터 jwt 설정
                //JwtAuthenticationFilter가 먼저 필터 실행된다.
                .addFilterBefore(new JwtAuthenticationFilter(jwtTokenProvider), UsernamePasswordAuthenticationFilter.class);



    return http.build();
    }
```
