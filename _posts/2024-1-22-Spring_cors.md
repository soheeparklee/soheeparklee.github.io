---
title: CORS_XXS, CSRF, SQL injection
categories: [AWS, Deploy]
tags: [xxs, csrf, injection, cross, scripting, forgery] # TAG names should always be lowercase
---

## ⭐️ Orgin이란?

> Orgin = Protocol + Host + Port <br>

이 세 가지가 같으면 동일 origin출처로 인식함<br>
orgin구분은 **브라우저**가 한다. 서버가 하는 일이 아님 ❌<br>

<img width="714" alt="Screenshot 2024-05-31 at 00 04 57" src="https://github.com/soheeparklee/sc_FrontBackTryout/assets/97790983/bf0040fa-dbbd-4e85-87ba-e7ada7203513">
출처: https://inpa.tistory.com/entry/WEB-📚-CORS-💯-정리-해결-방법-👏 [Inpa Dev 👨‍💻:티스토리]

## ⭐️ Proxy란?

> 클라이언트와 서버 사이의 중계 대리점 <br>
> CORS 에러가 뜰 때, 모든 출처를 허용한 **서버 대리점**을 통해 요청하면 에러가 안 날 것이다.<br>
> 프록시 서버를 구축하면 CORS 에러를 해결 할 수 있을 것이다. <br>

## ✅ SOP

> SOP: Same Orgin Policy <br>
> 웹 브라우저의 동일 출처 정책 <br>
> prevent web pages from making **requests** to a different domain than the one that **served** the web page. <br>
>
> javascript 엔진 표준 스펙에 존재하는 보안 규칙 <br>
> 동일한 출처에서만 리소스를 공유할 수 있다. <br>

- 같은 출처 정책 <br>
- **같은 서버**에서만 리소스를 불러올 수 있다.
- 사이트 A를 가지고 있으면 사이트 A에서만 가지고 온다. <br>
- 앞서 언급된 보안 위험 등으로 브라우저는 기본적으로 SOP를 따른다. <br>
- 외부에서 얻는 데이터는 항상 **같은 Orgin**이어야 인식한다. <br>

- SOP는 브라우저가 어떤 사이트에 접속중일 때 스크립트 내 `<script></script>`에서 초기화되는 다른 도메인에 대한 HTTP 요청 제한
- 예를 들어 네이버에 접속중인데 `<script></script>`코드에 구글로 보내는 HTTP요청이 있다면, SOP에 대의 제한

- 👍🏻 만약 이런 제약이 없다면, XXS, CSRF 등의 방법을 이용해 개인 정보를 가로챌 수 있다.
- 👍🏻 특정 정보를 다른 도메인으로 탈취하는 것을 막는다.

## 🛑 XXS

> Cross Site Scripting <br>
> 사용자가 **웹 페이지에 악성 스크립트를 삽입**하여 의도치 않은 명령을 하거나 해킹에 사용하는 것 <br>
> 상대방의 쿠키를 가져오기 <br>

- 삽입한 악성 스크립트로 쿠키를 빼가거나, 내가 원하지 않는 사이트로 접속하도록 만들 수 있음. <br>

1. Attacker identify input vulnerability in trusted website <br>
2. Attacker craft URL to perform code injection <br>
3. Client clicks on link <br>
4. Trusted site return page with malicious code <br>
5. Malicious code run on client browser <br>
   (Browser see this link is from trusted site, so trust) <br>

- Non-persistent XXS: server side XXS
- Persistent XXS: server side XXS
- DOM XXS: client side XXS

### 💊 XXS 해결 방법

- input validation
- 웹 페이지 작성 시 스크립트를 등록할 수 없도록 설정하기 <br>
- 중요 cookie HTTP ONLY 및 Secure 설정 <br>
  그래서 중요 cookie는 스크립트로도 쿠키를 빼갈 수 없도록 설정 <br>

## 🛑 CSRF

> Cross Site Request Forgery <br>
> 사용자의 **섹션이나 토큰을 이용해 다른 명령(request)**을 실행하도록 한다. <br>
> 상대방 쿠키는 상대방이 그대로 가지고 있고, 상대방에게 원하지 않은 request요청을 하도록 만들기 <br>

> tries to target victim to unintentionally carry out an action on website

- 예를 들어 피싱 메일 <br>
- 메일을 받아서 클릭하면(get요청) 비밀번호가 바뀌어버리는 일이 발생할 수 있음. <br>
- 이미 로그인한 유저 사이트 가서 아이디/비번 바꾸기

### 💊 CSRF 해결 방법

- **HTTP Refere**r: Host이름 비교하고 확인하기 <br>
  백엔드에서 Referer 검증을 통해 승인된 도메인으로 요청시에만 처리
  해커(메일에서)가 비밀번호 바꾸려고 하는 것인지, 호스트가 비밀번호 바꾸려고 하는 것인지 확인 <br>
- **CAPTCHA**로 사람 실행 확인 <br>
  ~신호등이 나와 있는 사진 클릭하세요 <br>
  사람인지 확인하기 <br>
- **Security Token**

## 🛑 SQL injection

> 서버로 보낼 때, 정상적인 요청값 대신 악의적인 DB SQL문을 주입하는 것<br>

에를 들어 아이디를 입력하는데 악의적인 DB SQL문 DELETE를 넣어버림. <br>
그러면 로그인하면 테이블이 변경되거나 삭제되어 버릴 수 있음! <br>
또는 사용자의 권한을 바꿔버린다던가... <br>

### 💊 SQL injection 웹 공격 방지 방법

- 여러 IF문으로 검증 로직 추가 <br>
  아이디는 DB SQL문을 사용할 수 없도록 <br>
- JPA를 사용하면 위협이 많이 낮아짐 <br>
- Input Validation
- Sanitize user data
- Web Application Firewall

## 🛑 XML injection

> insert malicious XML <br>
> XML: Extensible Markup Language <br>
>
> > - used for data exchange in web applications <br>

- XML bomb(billion laughs attack): consume memory, crash the host
- XXE(XML Extended Entity): read local resources

### 💊 XML injection 웹 공격 방지 방법

- input validation
- sanitize user data

## ✅ CORS

> Cross Orgin Resource Sharing <br>
> 그래서 원래 Orgin이 다르면 그 Resource는 들고 올 수 없는데, 이 제한을 풀어주는 것 <br>

- 현재 접속한 도메인 말고 다른 도메인에 접근할 수 있도록 해주기

- 왜냐하면 프론트 서버와 백엔드 서버는 다를 수밖에 없는데, <br>
- **같은 서버**에서 온 리소스만 받을 수 있다면 프론트와 백엔드는 소통할 수가 없음! <br>
- 프론트와 백엔드를 항상 서로 배포해야함... <br>
- 따라서 경우에 따라 SOP를 풀어주는 것도 필요하다. <br>

## 💊 CORS 해결 방법

#### 1. 브라우저 플러그인<br>

앞서 orgin이 같은지 다른지는 **브라우저**가 판단한다고 했다.<br>
따라서 브라우저에 플러그인을 추가하면 쉽게 해결할 수 있지만, <br>
문제는 새로운 기기가 추가될 떄마다 플러그인 일일이 추가해주어야 한다. <br>
<https://chromewebstore.google.com/detail/allow-cors-access-control/lhobafahddgcelffkeicbaginigeejlf?pli=1>

#### 2. 프록시 서버 구축

#### 3. 백엔드 전역 보안 설정

- 백엔드 단에서 `응답 HTTP 헤더`에 `Access-Control-Allow-Orgin`를 추가
- 서버에서 `Access-Control-Allow-Orgin` 헤더에 허용할 출처를 기재해서 클라이언트에 응답하면 된다.

##### ✔️ 강의 code

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

##### ✔️ moviereservationbe code

```java
@Configuration
@EnableWebSecurity
@RequiredArgsConstructor
public class SecurityConfig {
    private final JwtTokenProvider jwtTokenProvider;
    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception{
        http
                .headers(h -> h.frameOptions(f -> f.sameOrigin()))
                .csrf(c->c.disable())
                .httpBasic(h->h.disable())
                .formLogin(f->f.disable())
                .rememberMe(r->r.disable())
                .sessionManagement(s->s.sessionCreationPolicy(SessionCreationPolicy.STATELESS))
                .cors(c-> c.configurationSource(corsConfig())) // ⭐️ CORS
                .authorizeRequests(a->
                        a
                                .requestMatchers("/resources/static/**", "/auth/sign-up", "/auth/login", "/auth/logout").permitAll()
                                .requestMatchers("/test").hasRole("USER")
                )
                .exceptionHandling(e->{
                    e.authenticationEntryPoint(new CustomAuthenticationEntryPoint());
                    e.accessDeniedHandler(new CustomAccessDeniedHandler());
                })
                .addFilterBefore(new JwtAuthenticationFilter(jwtTokenProvider), UsernamePasswordAuthenticationFilter.class);

        return http.build();
    }

    // ⭐️ CORS
    private CorsConfigurationSource corsConfig() {
        CorsConfiguration corsConfiguration = new CorsConfiguration();
        corsConfiguration.setAllowCredentials(false);
        corsConfiguration.setAllowedOrigins(List.of("*"));
        corsConfiguration.addAllowedHeader("*");
        corsConfiguration.addExposedHeader("Token"); //추가
        corsConfiguration.setExposedHeaders(Arrays.asList("Authorization", "Authorization-refresh", "Token"));
        corsConfiguration.setAllowedMethods(List.of("GET","PUT","POST","DELETE"));
        corsConfiguration.setMaxAge(1000L*60*60);
        UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource();
        source.registerCorsConfiguration("/**",corsConfiguration);
        return source;
    }

    @Bean
    public AuthenticationManager authenticationManager(AuthenticationConfiguration authenticationConfiguration) throws Exception{
        return authenticationConfiguration.getAuthenticationManager();
    }
}
```

## 💡 S3 CORS 해결 방법

AWS S3 bucket에 CORS(Cross-origin 리소스 공유) 규칙을 추가한다.

<img width="669" alt="Screenshot 2024-05-31 at 00 35 40" src="https://github.com/soheeparklee/sc_FrontBackTryout/assets/97790983/cae2f175-ab53-4a8d-a499-a8d8d388f52f">
