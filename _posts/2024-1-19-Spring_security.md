---
title: Spring Security
categories: [JAVA, Spring]
tags: [security] # TAG names should always be lowercase
---

## ✅ Spring Security

> JAVA 기반 보안 프레임워크

- Authentication <br>
- Authorization <br>
- Session Control <br>
- CSRF 크로스 사이트 요청 위조 방지 <br>

#### ☑️ Spring Security 필수 개념

- 접근 주체: 누가 접근하는가? <br>
- **인증** Authentication: **증명** <br>
  유저가 누구인지 아는 것 <br>
- **인가** Authorization: **허락** <br>
  유저의 권한을 확인해 허락해 주는 것 <br>

#### ☑️ Spring Security 과정

## ✅ User Detail 구현 JWT 구현

```java
//1️⃣먼저 entity, repository구현
//entity
public class CustomUserDetailService implements UserDetailsService {
    private final UserPrincipalRepository userPrincipalRepository; //userEmail이 여기 있음

    @Override
    public UserDetails loadUserByUsername(String email) throws UsernameNotFoundException {
        UserPrincipal userPrincipal = userPrincipalRepository.findByEmailFetchJoin(email).orElseThrow(()-> new NotFoundException("No such user"));
        CustomUserDetails customUserDetails= CustomUserDetails.builder()
                .userId(userPrincipal.getUser().getUserId())
                .email(userPrincipal.getEmail())
                .password(userPrincipal.getPassword())
                .authorities(userPrincipal.getUserPrincipalRoles().stream().map(UserPrincipalRoles::getRoles).map(Roles::getName).collect(Collectors.toList()))
                .build();

        return  customUserDetails;
    }
}
//repository
//메소드 정의는 repository, JPA이니까 query 사용 가능
@Repository
public interface UserPrincipalRepository extends JpaRepository<UserPrincipal, Integer> {
@Query("SELECT up FROM UserPrincipal up JOIN up.userPrincipalRoles upr JOIN FETCH upr.roles WHERE up.email = :email") //N+1문제 해결 위해 JPQL, join.FETCH
 Optional <UserPrincipal> findByEmailFetchJoin(String email);

}

//그 다음 2️⃣ security Sevice구현
@Service
@RequiredArgsConstructor
@Primary
public class CustomUserDetailService implements UserDetailsService {
    private final UserPrincipalRepository userPrincipalRepository; //userEmail이 여기 있음

    @Override
    public UserDetails loadUserByUsername(String email) throws UsernameNotFoundException {
        UserPrincipal userPrincipal = userPrincipalRepository.findByEmailFetchJoin(email).orElseThrow(()-> new NotFoundException("No such user"));
        CustomUserDetails customUserDetails= CustomUserDetails.builder()
                .userId(userPrincipal.getUser().getUserId())
                .email(userPrincipal.getEmail())
                .password(userPrincipal.getPassword())
                .authorities(userPrincipal.getUserPrincipalRoles().stream().map(UserPrincipalRoles::getRoles).map(Roles::getName).collect(Collectors.toList()))
                .build();

        return  customUserDetails;
    }
}


```

## ✅ JWT 구현

1️⃣ filter을 구현한다.<br>
그리고 filter에 필요한 메소드들을 2️⃣ jwtTokenProvider에 구현한다.<br>

```java
//JWT을 가능하게 하기 위해 filter을 구현해야 한다.
//1️⃣ filter을 구현한다.
//filter에서 JWT있는지 없는지 확인해주어야 하기 떄문이다.
@RequiredArgsConstructor
public class JwtAuthenticationFilter extends OncePerRequestFilter {

    private final JwtTokenProvider jwtTokenProvider;

    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain) throws ServletException, IOException {
    String jwtToken= jwtTokenProvider.resolveToken(request);
    if(jwtToken != null && jwtTokenProvider.validateToken(jwtToken)) {//jwtToken이 없거나 valid하지 않으면
        //getAuthentication하는 과정
        Authentication auth= jwtTokenProvider.getAuthentication(jwtToken);
        //jwtTokenProvider에서 준 token을 getContext로 받는다.
        // SecurityContextHolder에 저장
        SecurityContextHolder.getContext().setAuthentication(auth);
    }
        //내 필터가 더 먼저 동작해야 하므로 먼저 썼음 ⬆⬆⬆
        //왜냐하면 내 필터는 jwtToken을 받아오기 떄문
        filterChain.doFilter(request, response);
    }
}


//그리고 filter에 필요한 메소드들을 2️⃣ jwtTokenProvider에 구현한다.
//jwtTokenProvider는 config파일들이랑 있다.

//jwt에 관련된 일을 맡은 클래스
//config 폴더 안에 있음
@RequiredArgsConstructor
public class JwtTokenProvider {
    //암호화되는 JwtToken을 풀 수 있는 Signature
    private final String secretKey = Base64.getEncoder().encodeToString("sohee-password".getBytes());
    //token이 얼마 시간동안 유효할지 정하기
    private long tokenValidMillisecond= 1000L * 60 * 60; //1시간

    private final UserDetailsService userDetailsService;

    //token에서 원하는 것 가져오기
    //header에서 받아온다.
    public String resolveToken(HttpServletRequest request) {
        return request.getHeader("X-AUTH-TOKEN");
    }
    //이메일과 권한을 가지고 token을 만들기
    public String createToken(String email, List<String> roles){
        Claims claims = Jwts.claims()
                .setSubject(email);
        claims.put("roles", roles);
        Date now = new Date();
        return Jwts.builder() //Token만들 때 이런저런 조건 설정해주기
                .setClaims(claims)
                .setIssuedAt(now) //등록 claim, 언제 등록됐냐?
                .setExpiration(new Date(now.getTime() + tokenValidMillisecond)) //언제 만료되나?
                .signWith(SignatureAlgorithm.HS256, secretKey)
                .compact();
    }

    //이 token이 괜찮은 것인가?
    //claim이 괜찮은지, expire되지는 않았는지 확인
    public boolean validateToken(String jwtToken) {
        try{
            //body 들고 오기
            Claims claims= Jwts.parser().setSigningKey(secretKey).parseClaimsJws(jwtToken).getBody();
            Date now = new Date();
            return !claims.getExpiration().after(now); //지금보다 token이 expire되었으면 문제가 있는 것, after이어야 한다.
        } catch(Exception e){
            return false;
        }
    }
    //이메일을 들고 온 것으로 token을 얻음
    //그래서 token을 만들어 filter로 넘겨준다.
    public Authentication getAuthentication(String jwtToken) {
        UserDetails userDetails= userDetailsService.loadUserByUsername(getUserEmail(jwtToken));
        return new UsernamePasswordAuthenticationToken(userDetails, "", userDetails.getAuthorities());    }

    private String getUserEmail(String jwtToken) {
        return Jwts.parser()
                .setSigningKey(secretKey)
                .parseClaimsJws(jwtToken)
                .getBody()
                .getSubject();
    }
}

```

## ✅ 회원가입 구현

```java
// 1️⃣ controller
@RestController
@RequiredArgsConstructor
@RequestMapping(value= "v1/api/sign")
public class SignController {

    private final AuthService authService;


    //회원 가입
    @PostMapping(value= "/register")
    public String register(@RequestBody SignUp signupRequest){
        boolean isSuccess= authService.signUp(signupRequest);
        return isSuccess? "회원가입 성공" : "회원가입 실패";
    }
}

//2️⃣ service
@Service
@RequiredArgsConstructor
public class AuthService {
    //회원가입 서비스
    private final UserPrincipalRepository userPrincipalRepository;
    private final UserRepository userRepository;
    private final RolesRepository rolesRepository;
    private final UserPrincipalRolesRepository userPrincipalRolesRepository;

    //password 암호화위해 사용
    private PasswordEncoder passwordEncoder;

    public boolean signUp(SignUp signupRequest) {
        //이메일, 비밀번호, 이름 받아와야
        String email= signupRequest.getEmail();
        String password= signupRequest.getPassword();
        String username= signupRequest.getName();

        //1. 기존에 있는 이메일 아이디는 회원가입 안된다는 로직
        if(userPrincipalRepository.existsByEmail(email)){
            return false;
        }
        //2. 유저가 이미 DB목록에 있으면 ID만 등록하고, 없으면 유저도 만들기
        UserEntity userFound= userRepository.findByUserName(username) //유저가 이미 DB목록에 있는지 이름 찾아보기
                .orElseGet(()-> //못 찾으면 유저 엔티티에 추가해서 유저 만들기
                        userRepository.save(UserEntity.builder()
                                .userName(username)
                                .build()));
        //3. 비밀번호 등록, 기본적으로 ROLE_USER
        Roles roles= rolesRepository.findByName("ROLE_USER").orElseThrow(()-> new NotFoundException("ROLE_USER NOT FOUND"))
        UserPrincipal userPrincipal= UserPrincipal.builder()
                .email(email)
                .user(userFound)
                .password(passwordEncoder.encode(password)) //패스워드는 인코딩해서 암호화해서 넣어야 한다.
                .build();

        //4. userPrincipalRepository에 저장
        userPrincipalRepository.save(userPrincipal);
        userPrincipalRolesRepository.save(
                UserPrincipalRoles.builder()
                        .roles(roles)
                        .userPrincipal(userPrincipal)
                        .build()
        );
        return true;
    }
}

// 3️⃣ DTO
//DTO에서 userName을 받아와 role을 준다.
@Getter
@NoArgsConstructor
@AllArgsConstructor
public class SignUp {
    private String email;
    private String password;
    private String name;
}

// 4️⃣ password Encoder Config 필요
//아까 서비스에서 비밀번호 암호화 하기 위해서
@Configuration
public class PasswordEncoderConfig {
    @Bean
    public PasswordEncoder passwordEncoder(){
        return new BCryptPasswordEncoder();
    }
}

// 5️⃣ 로그인 설정 web에서 바꾸기 SecurityConfiguration⭐️⭐️⭐️
@Configuration
@EnableWebSecurity
@RequiredArgsConstructor
public class SecurityConfiguration {
    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception{
        //로그인 설정 구현
        http.headers().frameOptions().sameOrigin()
                .and()
                .formLogin().disable()
                .csrf().disable()
                .httpBasic().disable()
                .rememberMe().disable() //아이디비번 기억하시겠습니까? disable
                .sessionManagement().sessionCreationPolicy(SessionCreationPolicy.STATELESS); //session 사용 disable
    return http.build();
    }
}

```

## ✅ 로그인 구현

// 로그인/로그아웃 구현

```java
// 1️⃣ controller
//로그인
    @PostMapping(value= "/login")
    public String login(@RequestBody Login loginRequest, HttpServletResponse httpServletResponse){
        //response안에 token을 넣어서
        String token= authService.login(loginRequest);
        httpServletResponse.setHeader("X-AUTH-TOKEN", token);
        return "Login Success";
    }

// 2️⃣ service

public String login(Login loginRequest) {
        String email= loginRequest.getEmail();
        String password= loginRequest.getPassword();
        try {
            Authentication authentication = authenticationManager.authenticate(
                    new UsernamePasswordAuthenticationToken(email, password) //token만들 때 email, password 필요
            );
            SecurityContextHolder.getContext().setAuthentication(authentication);

            //token발행
            UserPrincipal userPrincipal = userPrincipalRepository.findByEmailFetchJoin(email)
                    .orElseThrow(() -> new NotFoundException("No user Found"));

            List<String> roles = userPrincipal.getUserPrincipalRoles()
                    .stream()
                    .map(UserPrincipalRoles::getRoles)
                    .map(Roles::getName).collect(Collectors.toList());

            return jwtTokenProvider.createToken(email, roles);
        } catch(Exception e){
            e.printStackTrace();
            throw new NotAccpetExcpetion("Login Not Possible");
        }

    }

```

## ✅ 예외처리, 코드 개선

```java
// 유저만 항공 예약 시스템에 접근할 수 있도록 인가/허락/Authorization
// SecurityConfiguration에서 권한 주기

@Configuration
@EnableWebSecurity
@RequiredArgsConstructor
public class SecurityConfiguration {

    private final JwtTokenProvider jwtTokenProvider;
    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception{
        //로그인 설정 구현
        http.headers().frameOptions().sameOrigin()
                .and()
                .formLogin().disable()
                .csrf().disable()
                .httpBasic().disable()
                .rememberMe().disable() //아이디비번 기억하시겠습니까? disable
                .sessionManagement().sessionCreationPolicy(SessionCreationPolicy.STATELESS) //session 사용 disable
                .and() //⭐️ 여기서부터 role에 따라 항공 예약 시스템 접근 허용해주는 로직
                .authorizeRequests()
                    .antMatchers("/resources/static/**", "/v1/api/sign/*").permitAll() //로그인 안 했어도 허용
                    .antMatchers("/v1/api/air-reservation/*").hasRole("USER") //항공예약시스템은 USER만 접근 가능하다.
                .and() //⭐️ 여기서부터 jwt 설정
                //JwtAuthenticationFilter가 먼저 필터 실행된다.
                .addFilterBefore(new JwtAuthenticationFilter(jwtTokenProvider), UsernamePasswordAuthenticationFilter.class);


    return http.build();
    }
    @Bean
    public AuthenticationManager authenticationManager(AuthenticationConfiguration authenticationConfiguration) throws Exception {
        return authenticationConfiguration.getAuthenticationManager();
    }
}
```
