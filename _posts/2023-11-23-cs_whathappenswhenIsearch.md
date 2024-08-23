---
title: What happens when I click on a URL?
categories: [Computer Science, Network]
tags: [network]
---

### 1. Input URL, press Enter

### 2. Web browser translates URL

- If URL is incorrect, use Web browser's default search engine to search the URL

### 3. If URL is correct, encode URL

- URL uses `US-ASCII`
- If there is a letter that is not `US-ASCII`, encode
- Domain name uses `Punnycode` encoding
- Use `Percent encoding` for path lower than domain name

### 2. Check `HSTS` list

> Http Strict Transport Security <br>

- `HSTS list` enforces use of `HTTPS`
- check `HSTS list` to see if `HTTPS` is needed
- if on `HSTS list`, need to request for `HTTPS`
- if not on `HSTS list`, request for `HTTP`

### 3. Browser checks for DNS entry corresponding IP address of website in cache

- Browser cache
- OS cache
- Router cache
- ISP cache

- 항상 DNS서버에 접속해서 찾으려면 시간이 오래걸리니 <br>
- `로컬 캐시` 또는 `DNS캐시`에 저장해 두었다가 <br>
- `로컬 캐시` 또는 `DNS캐시`에 1차적으로 접속해서 IP주소 확인 <br>

### 4. If not found in cache, ISP DNS server initiates DNS query to find IP address of server with the domain name

- 없으면 DNS서버 접속
- DNS서버 안에 도메인과 `IP address`가 매핑이 되어있는데
- 우리가 요청하면 도메인에 연결된 `IP address`를 가져와 접속하게 된다.

<https://soheeparklee.github.io/posts/n-dns/> <br>

### 5. Get MAC address associated with IP address with ARP

> ARP: Address Resolution Protocol <br>

- devices use ARP to map an IP address to a MAC address

### 6. Browser initiates TCP connection

- `3-way-handshake` to start connection
- `SYN`
- `ACK`
- `4-way-handstake` to terminate connection

### 7. If HTTPS, add SSL(TLS) handshake

### 8. Browser sends `HTTP request` to the web server

### 9. Server sends response

- response in JSON, XML, HTML

### 10. Rendering by web browser

- When server responds with resource(HTML, CSS, JS)
- Redering by creating `DOM Tree`, CCSSOM Tree, Render Tree
  - DOM: HTML
  - CCSSOM(Cascading Style Sheets Object Model): CSS style
  - Render Tree: DOM ➕ CSSSOM
