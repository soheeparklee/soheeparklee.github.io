---
title: What happens when I click on a URL?
categories: [Computer Science, Network]
tags: [network]
---

### 1. Input URL, press Enter

### 2. Check HSTS list

> Http Strict Transport Security <br>

- check HSTS list to see if `HTTPS` is needed
- if on HSTS list, need to request for `HTTPS`
- if not on HSTS list, request for `HTTP`

### 3. Browser checks for DNS entry corresponding IP address of website in cache

- Browser cache
- OS cache
- Router cache
- ISP cache

항상 DNS서버에 접속해서 찾으려면 시간이 오래걸리니 <br>
로컬 캐시 또는 DNS캐시에 저장해 두었다가 <br>
로컬 캐시 또는 DNS캐시에 1차적으로 접속해서 IP주소 확인 <br>

### 4. If not found in cache, ISP DNS server initiates DNS query to find IP address of server with the domain name

없으면 DNS서버 접속 <br>
DNS서버 안에 도메인과 IP가 매핑이 되어있는데 <br>
우리가 요청하면 도메인에 연결된 IP를 가져와 접속하게 된다. <br>
PC에 등록되어 있는 서버의 DNS주소에 접속해서 DNS 사용하여 IP주소를 확인한다. <br>

### 5. Get MAC address associated with IP adress with ARP

> ARP: Adress Resolution Protocol

### 6. Browser initiates TCP connection

- 3-way-handshake
- SYN
- ACK

### 7. If HTTPS, add SSL(TLS) handshake

### 8. Browser sends HTTP request to the web server

### 9. Server sends response

- response in JSON, XML, HTML

### 10. Rendering by web browser

- When server responds with resource(HTML, CSS, JS)
- Redering by creating DOM Tree, CCSSOM Tree, Render Tree
  - DOM: HTML
  - CCSSOM(Cascading Style Sheets Object Model): CSS style
  - Render Tree: DOM ➕ CSSSOM
