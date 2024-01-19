---
title: WAS, Servlet
categories: [JAVA, Spring]
tags: [was, thread, servelt, controller, socket, stream] # TAG names should always be lowercase
---

WAS 🟰 WEB ➕ 서블릿 컨테이너<br>
<br>
WAS 내부에 디스패치 서블릿 내부동작이 일어나고 이 안에 스프링이 또 있음 <br>
따라서 스프링을 개발할 떄 우리는 서블릿 컨테이너의 일부를 구현하는 것이다. <br>

## ✅ WAS

> WAS: Web Application Server <br>
> client 요청을 받아 의미 있는 웹 애플리케이션을 실행하는 서버 <br>

### ✔️ WAS의 web서버가 하는 역할

<img width="625" alt="스크린샷 2024-01-08 오후 2 21 35" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/c71af60a-15a0-4910-bb36-a8c309895d11">

- 정적인 파일을 받아 처리(항상 같은 input, output이 나오는 것들, 이미지, 영상 등) <br>
- 동적인 요청은 **서블릿 컨테이너**로 위임 <br>

## ✅ 서블릿 컨테이너(🟰 웹 컨테이너)

> 대표적인 구현체: tomcat

1. 프로토콜 요청/응답 처리 <br>
2. 쓰레드 풀 관리 <br>
3. 스프링 지원 런타임 컴포넌트 <br>

### ☑️ Servlet

> **Servlet:** 클라이언트 **요청을 처리** & 서버에서 **동적인 웹 페이지**를 생성하는데 사용되는 주체

<img width="793" alt="스크린샷 2024-01-08 오후 2 27 46" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/18de6c9f-c7ab-4135-bfca-87a1e3e3d63e">

#### ✔️ Protocol 관련 Servlet

WAS는 HTTP뿐만 아니라 다양한 프로토콜 지원<br>

#### ✔️ Server framework 관련 Servlet

WAS는 스프링과 그 외 다양한 프레임워크 지원 <br>
스프링 ➡️ 디스패치 세브렛이 처리해준다. <br>

## ✅ 서블릿 컨테이너와 스프링 컨테이너

![코딩공책-15](https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/fef6c9ec-702d-49ec-a558-dbb22863d10d)

#### ✔️ 서버 소켓

서버는 무조건 서버 소켓을 열어두고 있어야 한다. <br>
서블릿 컨테이너가 연다. <br>
포트 열어서 서버에서 주고받을 준비 <br>

#### ✔️ 입출력 stream

stream을 통해서 데이터 주고받기 <br>

#### ✔️ 쓰레드 풀

쓰레드 풀도 미리 생성해둔다. <br>
미리 쓰레드 사용하려고 생성해 둔 pool <br>
멀티 쓰레딩 시작하면 미리 만들어 둔 객체를 주며 "이거 써!" 한다. <br>
사용 후 쓰레드 풀에 반환 <br>

<img width="781" alt="스크린샷 2024-01-08 오후 2 44 31" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/814f9f41-f834-4bed-ab72-b2570724f41f">

1. WAS(🟰tomcat)이 켜진다. <br>
2. 서버 소켓 OPEN(port 8080) <br>
3. thread pool 만들어 놓는다. <br>
4. Web browser에서 서버 소켓이 열린 것을 확인하고 HTTP GET API요청을 보낸다. <br>
5. 이 요청을 Web이 가장 먼저 만나는데, 자신이 처리할 수 있는 정적인 것이면 처리, 처리 못하면 서블릿 컨테이너로 넘긴다. <br>
6. thread pool에서 thread를 할당받는다. <br>
7. 입출력 stream을 연다. <br>
   👍🏻 데이터 주고받을 준비 완료 <br>
8. 소켓 통해서 정보 받음 <br>
9. 정보가 HTTP Protocol로 왔으면 Protocol 관련 서블렛 컨테이너에서 처리 <br>
10. 어떤 프레임워크 쓰는지에 따라 server framework 서블렛에서 처리 <br>
11. HTTP method, URI보고 해당하는 controller에 매핑되어 처리 <br>
    👍🏻 데이터 받기 끝 <br>
12. 데이터 보낼때는 반대. <br>
13. controller가 보낸다. <br>
14. HTTP에서 소켓으로 가서 데이터 보내고 <br>
15. 사용한 thread반환 <br>

## ✅ 디스패치 서블렛의 내부 동작 흐름

> HTTP method, URI보고 컨트롤러 정하게 되는데,
> 컨트롤러마다 처리 방법이 다르다.

<img width="722" alt="스크린샷 2024-01-08 오후 2 59 44" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/3cc2e4e7-c75a-4b56-a23d-bb315e749907">

#### ✔️ SSR controller ➡️ @Controller

![코딩공책-17](https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/9a087749-d195-4afc-b2e9-dc24ffe74905)

#### ✔️ CSR controller

![코딩공책-18](https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/b408b23a-0837-4c63-8450-3cc5a38155df)

## ✅ Spring MVC Pattern ➡️ @RestController

> Model View Controller

디스패치 서블렛: **프론트 컨트롤러 패턴**을 구현했다. <br>
각각의 역할을 객체에게 매핑하여(주어서) 수행 <br>
프론트 컨트롤러 패턴인 이유는 어떤 요청이 와도 앞에서 servlet이 매핑을 통해 관리한다. <br>

## ✅ WAS는 HTTP요청 시, Servelt Request/Response를 만든다.

### ☑️ HTTP Servelt Request

- 요청 정보를 서블릿에게 전달하기 위한 객체
- 헤더/URL/메소드 등을 확인하는 메서드가 있다.
- Body Stream(input)을 읽는 메소드가 있다.
- 기존에 @RequestParam으로 받던 Input값을 HTTP Servelt Request으로 대신 받을 수 있다.

💡 원래는 HttpServletRequest해서 받아오는 것인데 @RequestParam가 일을 해 준 것이다.

```java
public class Chap109Controller {
    private final ItemService itemService;

//@RequestParam
//    @GetMapping("/items-prices")
//    public List<Item> findItemByPrices(@RequestParam("max") Integer maxValue){ //⭐️@RequestParam
//        List<Item> items=  itemService.findItemEntitiesByPriceLessThanEqualOrderByPriceAsc(maxValue);
//        return items;
//    }

    //HttpServletRequest
    @GetMapping("/items-prices")
    public List<Item> findItemByPrices(HttpServletRequest httpServletRequest){
        Integer maxValue= Integer.valueOf(httpServletRequest.getParameter("max"));
        List<Item> items=  itemService.findItemEntitiesByPriceLessThanEqualOrderByPriceAsc(maxValue);
        return items;
    }
}
```

### ☑️ HTTP Servelt Response

- 요청을 보낸 클라이언트에게 응답을 보내는 객체
- 해당 서블릿을 통해 응답 output을 전송한다.
- 기존에 @RestController로 output내보내던 작업을 HTTP Servelt Response로 할 수 있다.

💡 기존 @PathVariable은 사실 HTTP Servelt Response의 getOutputStream()로 동작하고 있던 것이다.

```java
//    @DeleteMapping("/items/{id}")
//    public String deleteItemById(@PathVariable String id) {
//        itemService.deleteItem(id);
//        return "Object with id =" + id + "has been deleted";
//    }

    @DeleteMapping("/items/{id}")
    public void deleteItemById(@PathVariable String id, HttpServletResponse httpServletResponse) throws IOException {
        itemService.deleteItem(id);
        httpServletResponse.getOutputStream().println("Object with id =" + id + "has been deleted");
    }
```

## ➕ Servelt Container안의 Web Filter

허용되지 않은 요청, 응답이 오면 filter가 걸러주거나
기록을 남기는 filter도 있고
언어가 달라 깨진채로 오면 filter가 encoding 처리해주거나 등등의 역할을 한다.

**Spring Container** **밖에** 있음
따라서 Spring의 자원은 아니다. ❌
✔️ **doFilter()메소드**로 응답/요청 동작을 한다.
Request/Response 객체에 관여한다. ⭕️
그래서 Request/Response 받은 값을 바꿀 수 있는 것임.

#### 💡 Filter 기능

- 이미지/데이터 압출 및 문자열 인코딩
- 모든 요청에 대한 로깅
- 공통 보안 및 인증/인가

```java
//모든 요청에 대한 로깅 남기는 filter
@Component
@Slf4j
public class LoggingFilter extends OncePerRequestFilter { //나만의 filter을 만들래
    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain) throws ServletException, IOException {
        String method= request.getMethod();
        String uri= request.getRequestURI();
        log.info("요청이 들어왔습니다. "+ method + uri); //⭐️controller에 이 코드를 쓰지 않고 filter에 한 번에 쓴다.
        filterChain.doFilter(request, response);
        //기존 있던 filter chain에 내 filter도 끼워주라
        //⭐️doFilter앞에 쓰면 들어올 때 Filter, 뒤에 쓰면 나갈 때 Filter
        log.info(method + uri + response.getStatus()+ "response");
    }
}
```

## ➕ Spring Container안의 Interceptor

기본적으로 filter이랑 비슷하게 걸러주거나 추가 기능을 수행해주는데
filter랑 다른 점은 **Spring Container안**에 있다는 것이다.
Interceptor은 Spring Container의 자원이다. ⭕️
✔️ 요청 : **preHandler()**
✔️ 응답: **postHandler()** 메소드로
Request/Response 객체에 관여하지 않는다. ❌
Request/Response 객체에 관여하고 싶으면 filter로 하세요...

#### ⭐️ 순서

filter ➡️ controller ➡️ (들어오기 끝) ➡️ 결과 ➡️ (나가기) ➡️ controller ➡️ interceptor ➡️ filter

#### 💡 Interceptor 기능

- API 호출 시간 로깅
- 섹션 및 쿠키 체크
- 세부적인 보안 및 인증

```java
//API 호출 시간 로깅하는 Interceptor
@Component
@Slf4j
public class RequestTimeLoggingInterceptor implements HandlerInterceptor {
    //controller 요청 전
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        long startTime= System.currentTimeMillis(); //현재 시간
        request.setAttribute("request start time" , startTime);
        return true;
    }
    //controller 요청 끝난 후

    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        long startTime= (Long) request.getAttribute("request start time");
        long endTime= System.currentTimeMillis();
        long executeTime= endTime - startTime;

        log.info("{} {} executed in {} ms", request.getMethod(), request.getRequestURI(), executeTime);
    }
}
//Interceptor을 가져오기 위해 config필요하다.
@Configuration
@RequiredArgsConstructor
public class WebConfig implements WebMvcConfigurer {
    private final RequestTimeLoggingInterceptor requestTimeLoggingInterceptor;

    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(requestTimeLoggingInterceptor);
    }
}
```
