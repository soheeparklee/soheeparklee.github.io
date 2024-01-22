---
title: Cookie, Section, JWT
categories: [JAVA, Spring]
tags: [cookie, session, jwt] # TAG names should always be lowercase
---

## ✅ HTTP stateless 무상태성

> HTTP는 우리를 기억하지 못한다.
> 따라서 HTTP의 모든 요청은 별개의 요청이다.

내가 로그인해서 이 서비스에 가입된 것을 증명해도, HTTP는 나를 기억하지 못함!<br>
<br>
➡️ 따라서 HTTP 요청 떄마다 누군가 보내거나 보관하고 있어야 한다.<br>
<br>

- Cookie & Section 방식: server가 정보 가지고 있음<br>
- JWT 토큰: client가 정보 가지고 있음<br>

## ✅ Cookie & Section

> 브라우저에 저장되는 작은 테스트 조각(정보) <br>
> (클라이언트가 어떤 상품을 보고 있는지, 어떤 상품을 장바구니에 넣었는지, 다크모드로 보고있는지 등등...) <br>
> 보안이 중요한 비밀번호같은 정보는 Cookie에 저장하지 않는다. ❌ <br>
> key, value로 저장된다. <br>
> 정보가 Cookie에 저장되어 있으면 서버를 rerun하면 모든 정보가 사라진다. <br>

1️⃣ 클라이언트가 로그인을 한다. <br>
2️⃣ 서버는 **세션 ID**를 클라이언트에게 준다. <br>
3️⃣ 클라이언트는 **세션 ID**를 **쿠키**에 저장한다. <br>
4️⃣ **섹션 생성** <br>
5️⃣ 서버는 섹션에 세션 ID와 클라이언트를 알고 있다. <br>

```java
@RestController
@RequestMapping("/api")
public class SessionTokenSampleController {
    @GetMapping("/set-session") //세션 만들기
    public String setSession(HttpSession httpSession){
        httpSession.setAttribute("user", "Kim");
        httpSession.setAttribute("gender", "male");
        httpSession.setAttribute("job", "actor");
        return "session set complete";
    }

    @GetMapping("/get-session") //세션 가져오기
    public String getSession(HttpSession httpSession){
        String user= (String) httpSession.getAttribute("user");
        String gender= (String) httpSession.getAttribute("gender");
        String job= (String) httpSession.getAttribute("job");
        return String.format("%s, %s, %s", user, gender, job);
    }
}

    //new Session
    //서버가 나의 세션을 관리하고 있다.
    @GetMapping("/set-session") //세션 만들기
    public String setSession2(HttpSession httpSession){
        httpSession.setAttribute("user", "Lee");
        httpSession.setAttribute("gender", "female");
        httpSession.setAttribute("job", "programmer");
        return "session set complete";
    }

    @GetMapping("/get-session") //세션 가져오기
    public String getSession2(HttpSession httpSession){
        String user= (String) httpSession.getAttribute("user");
        String gender= (String) httpSession.getAttribute("gender");
        String job= (String) httpSession.getAttribute("job");
        return String.format("%s, %s, %s", user, gender, job);
    }
```

## ✅ JWT 토큰

> cookie에 비해 client에 더 치중되어 있는 방식 <br>
> 정보가 토큰에 저장되어 있기 떄문에 서버를 rerun해도 정보가 남아있다! <br> > <br>

1️⃣ 클라이언트가 로그인을 한다. <br>
2️⃣ JWT는 클라이언트에게 **토큰**을 준다. <br>
3️⃣ 토큰 안에는 **암호화된 정보**가 가득하다. <br>
4️⃣ 클라이언트는 이 토큰을 들고 있다가 새로운 요청을 보낼 때 토큰도 보여준다. <br>
5️⃣ JWT는 토큰을 생성하고 검증하여 클라이언트에게 응답을 준다. <br>

### ☑️ JWT

> Json Web Token
> Json format을 사용한다.
> 사용자 속성을 정의하는 claim 기반의 Web Token
> 정보를 알아볼 수 없게 encoding되어 있다.
> 알려지면 안되는 비밀번호같은 중요한 정보 가득❗️

#### ✔️ JWT 구성

- Header:
  - 알고리즘: 정보들을 암호화하기 위한 알고리즘
  - 타입
- Payload: 정보(sub, name, phoneNum, gender...)
  - JSON 형태 Claim모음
    - 공개 Claim
    - 비공개 Claim
  - 등록 Claim: 이미 약속되어 있는 Claim
- Signature: 암호화된 정보를 풀 수 있는 코드
  - 유효성 검증
  - 암호화 코드
  - 알고리즘 해쉬값

```java
@RestController
@RequestMapping("/api")
public class SessionTokenSampleController {
    @GetMapping("/generate-token")
    public String generateToken(HttpServletResponse httpServletResponse){
        String jwt= Jwts.builder()
                .setSubject("token1") //claim
                .claim("user", "Park")
                .claim("gender", "male")
                .claim("job", "teacher")
                .compact();
        httpServletResponse.addHeader("Token", jwt); //header로 보내기
        return "Jwt set complete";
    }

    @GetMapping("/show-token")
    public String showToken(@RequestHeader("Token") String token){
        Claims claims = Jwts.parser()
                .parseClaimsJwt(token)
                .getBody();

        String user= (String) claims.get("user");
        String gender= (String) claims.get("gender");
        String job= (String) claims.get("job");
        return String.format("%s, %s, %s", user, gender, job);
    }
}
```

## Cookie 🆚 JWT

#### JWT

👍🏻 stateless: 토큰에 정보가 저장되어 있으니 서버나 클라이언트는 자유로움 <br>
👍🏻 분산 시스템에 유리하다: 토큰에 정보가 저장되어 있으니 여러 서버, 여러 클라이언트 모두에서 분산해 사용할 수 있음<br>
👎🏻 보안이 약하다: 토큰 탈취되면 😱<br>
👎🏻 JWT 크기 증가: 너무너무 길어지면 JWT 자체가 길어져 속도가 느려진다.<br>
💡 언제 적합할까 ❓ 다양한 플랫폼을 운영하는 서비스(모바일, PC)<br>

#### Cookie

👍🏻 보안이 유리하다: 서버에 저장되어 있으니 서버만 잘 지키면 정보 안전<br>
👍🏻 유저 관리 용이: 서버와 연결 끊어버리기만 하면 끝<br>
👎🏻 상태 유지: 서버가 상태를 계속 유지하야하는 부담<br>
👎🏻 서버 부담 큼: 서버가 여러 명의 정보를 가지고 있어야 하고, 서버에 문제생기면 큰일남 😱<br>
💡 언제 적합할까 ❓ 서버 측에서 사용자 상태관리를 해야 할 때<br>
