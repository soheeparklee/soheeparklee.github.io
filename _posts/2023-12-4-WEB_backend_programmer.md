---
title: What does a backend programmer do?
categories: [Computer Science, WEB]
tags: [backend] # TAG names should always be lowercase
---

## ✅ 백엔드의 주요 업무

### 주문업무

- 비즈니스 요구 설계 및 구현(고객 요구사항 확인)
- 필터링
- 예외 처리(고객 1차 대응, 위험 지역 같은 경우 서버에서 차단해버림)
- 문제: 대용량 트래픽 부하 문제, 트래픽이 몰림(고객 주문이 한꺼번에 몰려서 고객이 대기해야 하는 경우)
- 해결: 서버 구현 기술:비즈니스 요구 설계: Spring Boot, 필터링: Spring Security, 트래픽 부하: 로드 밸런싱

### 창고 업무

- 모델링, DB 설계(물건 입고 시, 검색 및 분류)
- CRUD(물품 요청 시, 해당 물품 픽킹)
- DB관리, 용량 관리(물품 관리 및 폐기)
- 문제: 데이터 정합성 문제(실제 재고 수량, 기록된 수량 불일치 문제)
- 해결: MySQL, mongoDB, JPA

### 배송 업무

- HTTP 응답 방식/필드 결정(물품 출고 시, 물품에 맞는 포장)
- 프로토콜 선택, 포워딩(신속하고 정확하게 물품 배송)
- 문제: HTTP 보안 문제(배송 과정 중 물품 파손)
- 해결: HTTPS, SMTP, 쿠키 동의
