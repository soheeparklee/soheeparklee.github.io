---
title: Cookie, Session, JWT
categories: [JAVA, Spring]
tags: [cookie, session, jwt] # TAG names should always be lowercase
---

## ✅ HTTP stateless 무상태성

> HTTP는 우리를 기억하지 못한다.
> 따라서 HTTP의 모든 요청은 별개의 요청이다.

내가 로그인해서 이 서비스에 가입된 것을 증명해도, HTTP는 나를 기억하지 못함!<br>
➡️ 따라서 HTTP 요청 떄마다 누군가 보내거나 보관하고 있어야 한다.<br>
<br>

- Cookie: client가 정보 가지고 있음<br>
- Session: server가 정보 가지고 있음<br>
- JWT 토큰: client가 정보 가지고 있음<br>

## ✅ Cookie

- 브라우저에 저장되는 작은 테스트 조각(정보)
- (클라이언트가 어떤 상품을 보고 있는지, 어떤 상품을 장바구니에 넣었는지, 다크모드로 보고있는지 등등...)
- 보안이 중요한 비밀번호같은 정보는 Cookie에 저장하지 않는다. ❌
- key, value로 저장된다.
- 정보가 Cookie에 저장되어 있으면 서버를 rerun하면 모든 정보가 사라진다.

## ✅ Session

<img width="461" alt="Screenshot 2024-09-03 at 23 41 56" src="https://github.com/user-attachments/assets/c021ddab-2782-496f-9d20-9cc9a182da28">

- 세션은 쿠키를 기반으로 한다.
- 일정 기간동안 클라이언트에게서 들어오는 요구 = 하나의 상태
- 상태를 유지
- 👎🏻 session is saved on **server's DB or memory**, taking up lot of space
- 👎🏻 might result in server DB, memory overhead
- 👎🏻 session makes server scalability difficult

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

## Cookie 🆚 Session

#### Cookie

- stored at: client memory/harddisk
- format: text
- expire: set when saving cookie(default: when broswer ends)
- resoruce: use client resource
- size: 20 per domain, 4KB per cookie

#### Session

- stored at: server memory
- format: object
- expire: when client logs out, expires when there is no response
- resoruce: use server resource
- size: unlimited

## ✅ Token

- stateless
- server does not remember like session
- server issue token to client
- client shows this token when **requesting** to server

> 정보가 토큰에 저장되어 있기 떄문에 서버를 rerun해도 정보가 남아있다! <br>

1️⃣ 클라이언트가 로그인을 한다. <br>
2️⃣ 서버는 클라이언트에게 **토큰**을 준다. <br>
3️⃣ 토큰 안에는 **암호화된 정보**가 가득하다. <br>
4️⃣ 클라이언트는 이 토큰을 들고 있다가 **새로운 요청을 보낼 때** 토큰도 보여준다. <br>
5️⃣ 서버는 토큰을 검증하여 클라이언트에게 응답을 준다. <br>

> **What is inside Token?** <br>
>
> > - digital signature made by server with server's private key <br>
> > - server can verify token's digital signature with public key <br>

> **What is the benefits of using token?**
>
> > - 👍🏻 server overhead problem solved(problem of session) <br>
> > - 👍🏻 can scale up server(problem of session) <br>
> > - 👍🏻 can be used as OAUTH <br>
> > - 👍🏻 encrypted, thus prevent forging(problem of cookie) <br>

## ✅ JWT

> Json Web Token <br>
> used for authorization <br>

- `Json format`을 사용한다. `(문자열로 구성)`
- location: can be placed in URL, HTTP header(`Json format`)
- 사용자 속성을 정의하는 claim 기반의 Web Token
- 정보를 알아볼 수 없게 encoding되어 있다.
- 알려지면 안되는 비밀번호같은 중요한 정보 가득❗️

1️⃣ 서버는 클라이언트를 authenticate <br>
2️⃣ 인증이 되면, 서버는 `비밀키`, `공개키`를 생성하고 <br>
− `헤더와 페이로드` `인코딩`한다음<br>
− 둘을 합친 `문자열`을 `비밀키`로 서명하여<br>
− `JWT`생성<br>
− 그리고 클라이언트에게 보낸다<br>
3️⃣ 클라이언트는 다음 요청시 이 `JWT`를 서버에게 보낸다 <br>
4️⃣ 서버는 `JWT`의 서명을 `공개키`로 검증 <br>

### ☑️ Access Token, Refresh Token

- access token: to authenticate
- refresh token: when access token expires, to issue access key

### ☑️ JWT 구성

> Header.Payload.Signature <br>
> devided with `.` <br>

✔️ **Header** <br>

> how to `verify` JWT

- `타입 typ`: token type `"JWT"`
- `알고리즘 alg`: hash 알고리즘
- `키 kid`: key used for digital signature `private/public key`

```
{
	"typ" : "JWT",
	"alg" : "HS256"
    "kid" : "Key ID"
}
```

- 위와 같은 `JSON객체`를 `문자열`로 만들고 `UTF-8`과 `Base64 URL-Safe`로 `인코딩`하면 아래와 같이 `header` 생성

```
Base64URLSafe(UTF-8('{"alg": "ES256","kid": "Key ID"}')) -> eyJhbGciOiJFUzI1NiIsImtpZCI6IktleSBJRCJ9
```

✔️ **Payload** <br>

> JWT 정보(sub, name, phoneNum, gender...) <br>

- JSON 형태: `Claim`으로 구성
- Payload 속성들을 `Claim set`이라고 부름
- registered claim: hold information about token
- 공개 Claim
- 비공개 Claim

> What is inside payload? <br>
>
> > - Client information <br>
> > - token created date, time <br>

```
{
    "iss": "sohee.park",
    "iat": "1586364327"
}
```

- 위와 같은 `JSON객체`를 `문자열`로 만들고 `UTF-8`과 `Base64 URL-Safe`로 `인코딩`하면 아래와 같이 `payload` 생성

```
Base64URLSafe('{"iss": "sohee.park","iat": "1586364327"}') -> eyJpYXQiOjE1ODYzNjQzMjcsImlzcyI6ImppbmhvLnNoaW4ifQ
```

✔️ **Signature** <br>

> 암호화된 정보를 풀 수 있는 코드 <br>
> signed `header+payload` <br>

- use `header's alg(algorithm)` and `private key` to create signature and encode
- 유효성 검증
- 암호화 코드
- 알고리즘 해쉬값

```
Base64URLSafe(Sign('ES256', '${PRIVATE_KEY}',
'eyJhbGciOiJFUzI1NiIsImtpZCI6IktleSBJRCJ9.eyJpYXQiOjE1ODYzNjQzMjcsImlzcyI6ImppbmhvLnNoaW4ifQ'))) ->
MEQCIBSOVBBsCeZ_8vHulOvspJVFU3GADhyCHyzMiBFVyS3qAiB7Tm_MEXi2kLusOBpanIrcs2NVq24uuVDgH71M_fIQGg
```

### ⭐️ JWT JAVA

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

## Session 🆚 JWT

#### JWT

👍🏻 stateless: 토큰에 정보가 저장되어 있으니 서버나 클라이언트는 자유로움 <br>
👍🏻 분산 시스템에 유리하다: 토큰에 정보가 저장되어 있으니 여러 서버, 여러 클라이언트 모두에서 분산해 사용할 수 있음<br>
👎🏻 보안이 약하다: 토큰 탈취되면 😱<br>
👎🏻 JWT 크기 증가: 너무너무 길어지면 JWT 자체가 길어져 속도가 느려진다.<br>
💡 언제 적합할까 ❓ 다양한 플랫폼을 운영하는 서비스(모바일, PC)<br>

#### Session

👍🏻 보안이 유리하다: 서버에 저장되어 있으니 서버만 잘 지키면 정보 안전<br>
👍🏻 유저 관리 용이: 서버와 연결 끊어버리기만 하면 끝<br>
👎🏻 상태 유지: 서버가 상태를 계속 유지하야하는 부담<br>
👎🏻 서버 부담 큼: 서버가 여러 명의 정보를 가지고 있어야 하고, 서버에 문제생기면 큰일남 😱<br>
💡 언제 적합할까 ❓ 서버 측에서 사용자 상태관리를 해야 할 때<br>
