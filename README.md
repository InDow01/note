# 🛡️ Web Vulnerability & Secure Coding Study

> **Project**: GGaera Collection Vulnerability Assessment
> **Based on**: 주요정보통신기반시설 기술적 취약점 분석·평가 상세가이드 (2021)
> **Enhanced with**: 2026년 최신 보안 트렌드 & Cloud Native Security Insight

이 저장소는 **Java/Spring/Tomcat** 환경에서 웹 애플리케이션의 주요 취약점(1~28번 항목)을 진단하고, 이에 대한 시큐어 코딩(Secure Coding) 및 인프라 대응 방안을 정리한 기술 문서입니다.

---

## 📚 목차 (Table of Contents)

### 1️⃣ 입력 데이터 검증 및 표현 (Injection & Input Validation)
사용자의 악의적인 입력값을 신뢰하여 발생하는 치명적인 취약점들을 다룹니다.
- **04. OS Command Injection**: `ProcessBuilder` 사용 시 파라미터 격리 및 구조적 분리.
- **05. SQL Injection**: MyBatis/PreparedStatement를 활용한 바인딩 변수 처리.
- **10. 악성 콘텐츠 (Malicious Content)**: XSS 방지 및 사용자 입력값의 무해화(Sanitization).

### 2️⃣ 인증 및 접근 제어 (Authentication & Access Control)
"누구인가(AuthN)"와 "무엇을 할 수 있는가(AuthZ)"를 검증하는 보안의 핵심입니다.
- **13. 불충분한 인증 (Insufficient Authentication)**: 중요 페이지 접근 시 서버 사이드 세션 검증 (Forceful Browsing 방어).
- **14. 취약한 패스워드 복구**: 본인 확인 로직 강화 및 로직 우회(IDOR) 차단.
- **17. 불충분한 인가 (Insufficient Authorization)**: URL 접근 제어 및 데이터 소유권 검증 (수직/수평적 권한 상승 방지).
- **24. 관리자 페이지 노출**: `WEB-INF` 구조 활용 및 IP 기반 접근 통제(Allow-List).

### 3️⃣ 세션 관리 (Session Management)
사용자의 연결 상태를 유지하는 세션의 생명주기를 안전하게 관리합니다.
- **16. 취약한 세션 예측**: `SecureRandom`(CSPRNG)을 이용한 예측 불가능한 세션 ID 생성.
- **18. 불충분한 세션 만료**: 로그아웃 시 `session.invalidate()` 및 서버 메모리 소거.
- **19. 세션 고정 (Session Fixation)**: 로그인 성공 시 세션 ID 재발급(Migration).

### 4️⃣ 파일 및 리소스 관리 (File & Resource Security)
파일 업로드/다운로드 기능을 통한 시스템 장악 시도를 방어합니다.
- **22. 파일 업로드 (File Upload)**: **[Critical]** 확장자 화이트리스트, 파일명 난수화, 실행 권한 제거, 저장 경로 분리.
- **23. 불충분한 파일 다운로드**: DB 식별자 기반 다운로드 구현 및 경로 순회 문자(`../`) 차단.
- **25. 경로 추적 (Path Traversal)**: `getCanonicalPath()`를 이용한 절대 경로 검증으로 우회 공격 차단.
- **26. 위치 공개 (Unnecessary Files)**: 불필요한 백업 파일(`.bak`, `.git`) 및 디렉터리 리스팅 제거.

### 5️⃣ 데이터 보호 및 설정 (Data Protection & Configuration)
중요 정보의 노출을 막고 안전한 통신 환경을 구축합니다.
- **08. 디렉터리 인덱싱**: 웹 서버(Apache/Tomcat) 설정(`listings=false`)을 통한 파일 목록 노출 차단.
- **09. 정보 노출**: 에러 페이지(Stack Trace) 커스텀 처리 및 주석 내 민감 정보 제거.
- **27. 데이터 평문 전송**: 전 구간 HTTPS 적용 및 Secure Cookie 설정.
- **28. 쿠키 변조 (Cookie Tampering)**: 클라이언트 측 데이터 신뢰 금지 및 HMAC 무결성 검증/서버 세션 사용.

### 6️⃣ 비즈니스 로직 및 서비스 (Business Logic & Service)
애플리케이션의 흐름을 악용하는 논리적 허점을 방어합니다.
- **20. 자동화 공격 (Automated Attack)**: CAPTCHA, 계정 잠금(Lockout), Rate Limiting 적용.
- **21. 불충분한 프로세스 검증**: 결제/인증 로직의 순서 검증 및 상태(State) 기반 트랜잭션 관리.

---

## 💡 Key Highlights (Deep Dive)

### 🛡️ 2021 vs 2026 Standard Comparison
본 프로젝트는 2021년 가이드라인을 준수하되, 최신 2026년 보안 트렌드를 반영하여 진단 깊이를 더했습니다.

| 항목 | 2021년 기준 (Legacy) | 2026년 기준 (Modern) |
| :--- | :--- | :--- |
| **인증/인가** | URL 및 페이지 접근 통제 여부 | API 파라미터 변조(IDOR) 및 로직 무결성 검증 |
| **파일 업로드** | 확장자 필터링(블랙/화이트) | 실행 환경 격리(Cloud/NAS) 및 파일 무해화(CDR) |
| **정보 노출** | 에러 메시지, 백업 파일 점검 | Git 메타데이터, 클라우드 Key, API 명세서 노출 점검 |
| **자동화 공격** | 캡차 적용 유무 | 캡차 우회 가능성 및 Credential Stuffing 방어 |

### 🛠️ Tech Stack & Environment
* **Language**: Java (JSP/Servlet), Python (Diagnosis Script)
* **Framework**: Spring Boot / Legacy Spring MVC
* **Server**: Apache Tomcat 9.0.12 (Hardened Config)
* **Database**: Oracle DB / MySQL
* **Tools**: Burp Suite, Wireshark, EditThisCookie

---

## 📝 License & Contact
이 문서는 개인 학습 및 프로젝트 포트폴리오 용도로 작성되었습니다.
* **Author**: InDow01