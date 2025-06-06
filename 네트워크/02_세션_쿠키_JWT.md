# 🔐 세션, 쿠키, JWT 정리

> 면접 준비 + 실무 이해용 CS 개념 정리  

---

## 📚 목차

1. [세션(Session) vs 쿠키(Cookie)](#-1-세션session-vs-쿠키cookie)
2. [JWT (JSON Web Token)](#-2-jwt-json-web-token)
3. [JWT vs 세션 차이점 정리](#-3-jwt-vs-세션-차이점)
4. [상황별 추천 인증 방식](#-4-상황별-추천-인증-방식)

---

## 📌 1. 세션(Session) vs 쿠키(Cookie)

### 🍪 쿠키(Cookie)
- 클라이언트(브라우저)에 저장되는 **작은 데이터 조각** (최대 4KB)
- 사용 예: 로그인 상태 유지, 자동 로그인, 방문 기록 등
- `서버 → 클라이언트`: `Set-Cookie` 헤더로 쿠키 전송  
- `클라이언트 → 서버`: 요청 시마다 쿠키 자동 전송

### 🪪 세션(Session)
- 서버에 저장되는 사용자 상태 정보
- 클라이언트는 세션 ID만 가지고 있음 (보통 쿠키에 저장)
- 실제 인증 정보는 서버 메모리 or DB에 있음

### ✅ 비교 정리

| 항목       | 세션                          | 쿠키                          |
|------------|-------------------------------|-------------------------------|
| 저장 위치  | 서버                          | 클라이언트(브라우저)         |
| 보안       | 비교적 안전                   | 탈취 위험 있음                |
| 용량 제한  | 제한 없음                     | 4KB 이하                      |
| 유지 방식  | 세션 ID로 서버 정보 조회      | 클라이언트가 직접 저장        |
| 속도       | 느림 (서버 접근 필요)         | 빠름 (로컬 접근)             |

---

## 🔐 2. JWT (JSON Web Token)

### ✅ JWT란?
- 사용자 인증 정보를 JSON 형식으로 인코딩한 **토큰 기반 인증 방식**
- **Stateless 인증** (서버가 상태를 저장하지 않음)
- 자체적으로 정보, 만료시간 등을 담고 있음

### 🧩 구조
Header.Payload.Signature

- Header: 서명 알고리즘, 타입 (ex. JWT)
- Payload: 사용자 정보 (ex. userId, role)
- Signature: 위 정보를 비밀키로 서명한 값 (위조 방지용)

### 📌 인증 흐름

1. 로그인 성공 시 서버가 JWT 발급
2. 클라이언트가 JWT를 저장 (localStorage, sessionStorage, Cookie 등)
3. 요청 시 `Authorization: Bearer <JWT>` 헤더로 전송
4. 서버가 토큰을 검증하여 사용자 식별

---

## 🆚 3. JWT vs 세션 차이점

| 항목       | 세션 기반 인증                | JWT 기반 인증                  |
|------------|-------------------------------|---------------------------------|
| 상태 관리  | Stateful (서버가 상태 기억)    | Stateless (서버는 상태 기억 X) |
| 저장 위치  | 세션 ID는 클라이언트에, 정보는 서버 | 토큰 전체가 클라이언트에 저장 |
| 서버 부하  | 사용자 수가 많아지면 서버 부하 ↑ | 서버 확장에 유리                |
| 보안       | 비교적 안전                    | 탈취 시 위험 → HTTPS 필수      |
| 인증 처리  | 세션 ID로 서버 정보 조회       | 토큰만으로 인증 처리 가능       |

---

## 🎯 4. 상황별 추천 인증 방식

| 상황             | 추천 방식      |
|------------------|----------------|
| 일반적인 웹 로그인 | 세션 기반      |
| 모바일 앱, API 서버 | JWT 기반       |
| 서버 간 인증       | JWT 기반       |
| 보안 민감한 서비스 | 세션 + HTTPS  |

---

## ✨ 요약

- 쿠키: 클라이언트 저장용 (자동 전송)
- 세션: 서버 저장, 세션 ID로 사용자 구분
- JWT: 자체적으로 사용자 정보 담긴 토큰, 서버는 상태 저장 X  
- JWT는 확장성과 유연성에서 강점 있지만, **보안 설정 필수**

---




