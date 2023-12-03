---
title: bundler, web framework, SPA, SSR, CSR
categories: [Web, Tools]
tags: [til, bundler, web framework, spa, ssr, csr]
---

## ✅ bundler

여러 개의 파일들의 리소스를 웹 페이지를 로드할 때마다 네트워크 요청을 보내게되면 로딩 시간을 늘리고, 이는 사용자 경험 ☹️ <br>
**bundler**
웹 애플리케이션의 모든 자원을 하나 또는 여러 개의 파일로 병합 및 압축
네트워크 요청의 수를 최소화 ➡️ 로딩 시간 ⬇️
예를 들어 Webpack, Rollup, Parcel, Vite

**benefits of using a bundler**

1. 병합(Merging)과 최소화(Minification):
   - 여러 개의 파일을 하나로 병합
   - 코드를 최소화하여 파일 크기를 줄이기
2. 모듈 시스템 지원:
   - CommonJS, AMD와 같은 모듈 시스템을 브라우저에서 사용 가능
   - 코드의 재사용성 ⬆️ 유지보수성 ⬆️
3. 트랜스파일링 지원:
   - 최신 자바스크립트 문법을 브라우저 호환 가능한 코드로 변환
   - 최신 문법을 사용하면서도 다양한 브라우저와 호환성을 유지 가능
4. 환경 변수 처리, 파일 경로 관리:

## ✅ web framework

Web frameworks provide a structured way to build and organize web applications  
웹 개발에 필요한 공통적인 기능을 미리 구현해 놓은 도구  
기본적인 부분을 매번 처음부터 개발할 필요 없이, 웹 애플리케이션의 핵심 로직에 집중

**types of web framework**

- Django (Python)
- Flask (Python)
- Ruby on Rails (Ruby)
- Express.js (JavaScript - Node.js)
- React (JavaScript - Front-end Library)
- Laravel (PHP)
- Spring Boot (Java)
- Vue.js (JavaScript - Front-end Framework)

**benefits web frameworks**

1. Structured Development
   - Web frameworks typically follow a predefined structure or architectural pattern
   - such as MVC - Model-View-Controller
   - helps developers organize code, making it more maintainable and scalable.
2. Productivity
   - come with built-in tools, utilities, and libraries
3. Abstraction of Complexity
   - high level abstractions ➡️ focus more on logic and less on the intricacies
4. Code Reusability
5. Security Features 보안
   - 웹 프레임워크는 SQL 인젝션, XSS, CSRF 등과 같은 공통적인 웹 공격에 대한 보호 메커니즘을 제공
6. Scalable

## ✅ SPA single page application

전통적인 웹 페이지: 사용자가 페이지를 이동할 때마다 서버에서 새로운 HTML을 로드하여 페이지를 새로 고침
SPA: 페이지 전환 없이(새로고침 없이) 사용자와 상호작용하면서 필요한 부분만 업데이트  
 interacts with the user by dynamically rewriting the current page, rather than loading entire new pages from the server.  
라우팅을 했을 때 서버에 HTML을 요청하는 것이 아닌 JavaScript가 새로운 HTML을 만들어서 필요한 부분을 교체  
JavaScript만을 이용해 페이지 렌더링 및 라우팅을 구현

1. 페이지마다의 HTML을 템플릿리터럴 방식으로 모듈화

2. 현재 URL 정보를 window.location.pathname으로 가져오고 어떤 페이지인지에 따라 1)에서 만든 각기 다른 HTML을 가져오도록 구현

3. 가져온 HTML을 render하는 함수를 만들어서 body 혹은 가장 루트가 되는 div에 렌더링되도록 구현해보세요.

AJAX (Asynchronous JavaScript and XML): SPAs make extensive use of AJAX to fetch data from the server asynchronously without reloading the entire page. This allows for a smoother and more responsive user experience, as only the necessary data is fetched and rendered.

API-Driven Development: SPAs often rely on APIs (Application Programming Interfaces) to retrieve and send data. The backend provides a set of APIs that the frontend uses to interact with the server, allowing for a separation between the frontend and backend concerns.

옵저버 패턴?

## ✅ SSR (Server-Side Rendering) and CSR (Client-Side Rendering)

SSR (Server-Side Rendering) and CSR (Client-Side Rendering) are two different approaches to rendering web pages
**서버 사이드 렌더링(SSR)의 장단점:**
In SSR, the initial rendering of the web page is done on the server side.  
The server sends fully rendered HTML to the client, including content and markup.
장점:

1. Faster Initial Page Load 초기 로딩 속도: SSR에서는 서버에서 렌더링된 완성된 HTML을 클라이언트에 전송하기 때문에, 초기 페이지 로딩 속도가 빠릅니다.
2. Improved SEO SEO 최적화: 렌더링된 완성된 HTML을 클라이언트에 전송하므로, 검색 엔진이 쉽게 크롤링할 수 있습니다. 이는 검색 엔진 최적화(SEO)에 유리합니다.
3. 호환성: 모든 브라우저에서 동작하므로, 이전 버전의 브라우저와의 호환성 문제가 적습니다.

단점:

1. Server Load 서버 부하: 각 사용자 요청마다 서버에서 렌더링 작업을 수행해야 하므로, 서버 부하가 클 수 있습니다.
2. Slower Subsequent Page Updates 사용자 인터랙션: 동적인 페이지 요소를 구현하기 위해 추가적인 자바스크립트 코드가 필요할 수 있습니다.

example:
Next.js (React)
Nuxt.js (Vue.js)
Angular Universal (Angular)

**클라이언트 사이드 렌더링(CSR)의 장단점:**
In CSR, the initial HTML, CSS, and JavaScript are sent to the client.
The client's browser is responsible for rendering the content dynamically.

장점:

1. Reduced Server Load 서버 부하 감소: 렌더링 작업이 클라이언트에서 수행되므로, 서버 부하가 감소합니다.
2. 사용자 인터랙션: 클라이언트에서 동적으로 페이지를 업데이트할 수 있어, 사용자 인터랙션에 좋습니다.
3. Faster Subsequent Page Updates 속도 최적화: 초기 로딩 후에는 서버에서 받아온 데이터만으로 클라이언트에서 렌더링이 이루어지므로, 전체적인 페이지 전환 속도가 빠릅니다.

단점:

1. Slower Initial Page Load 초기 로딩 속도: 클라이언트에서 자바스크립트를 다운로드하고 실행한 후 렌더링을 진행해야 하므로 초기 로딩 속도가 느릴 수 있습니다.
2. SEO Challenges SEO 최적화 문제: 검색 엔진이 자바스크립트를 실행하지 않는 경우, 렌더링되지 않은 페이지를 크롤링하게 되어 SEO에 불리할 수 있습니다.
3. 클라이언트 자원 사용: 클라이언트에서 렌더링 작업이 이루어지므로, 성능이 낮은 기기에서는 페이지 로딩 속도와 반응성이 떨어질 수 있습니다. 이로 인해 사용자 경험이 저하될 수 있습니다.
4. 호환성 문제: 자바스크립트를 기반으로 하기 때문에, 구형 브라우저와의 호환성 문제가 발생할 수 있습니다.

example:
React (with create-react-app or other setups)
Vue.js (with vue-cli or similar setups)
Angular (in default mode)
