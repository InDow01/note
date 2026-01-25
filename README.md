# 🛡️ Web Security Study Notes

이 저장소는 웹 애플리케이션 취약점(OWASP Top 10, 주요정보통신기반시설 가이드라인 등)의 원리를 분석하고, **Java/Tomcat 환경**에서의 시큐어 코딩(Secure Coding) 및 실무 대응 방안을 정리한 학습 노트입니다.

> **⚠️ 가이드라인 기준 안내 (Standard Reference)**
> * 본 학습 노트는 [2021년 주요정보통신기반시설 기술적 취약점 분석·평가 상세가이드]를 기준으로 작성되었습니다.
> * 단, 개념이 모호하거나 최신 보안 트렌드 반영이 필요한 항목(예: 악성 콘텐츠 vs 파일 업로드)에 한하여 [2026년 개정 가이드라인]을 비교·분석하여 통찰(Insight)을 더했습니다.
> * *2026년 기준의 전체 가이드라인 분석은 추후 별도 프로젝트로 진행될 예정입니다.*

---

## 📚 목차 (Table of Contents)

### 1. 인젝션 (Injection)
* **04. OS Command Injection** - ProcessBuilder를 활용한 구조적 분리
* **05. SQL Injection** - PreparedStatement 및 MyBatis 시큐어 코딩

### 2. 정보 노출 및 설정 (Information Leakage & Configuration)
* **08. Directory Indexing** - Apache/Tomcat 설정(Options -Indexes) 및 리스팅 방지
* **09. Information Leakage** - 주석 관리, 에러 페이지(Stack Trace) 처리 및 불필요한 파일 삭제

### 3. 악성 콘텐츠 및 업로드 (Malicious Content & Upload)
* **10. 악성 콘텐츠 (Malicious Content)** - [User-Side] 사용자 감염 방지 및 악성코드 유포 차단
* **22. 파일 업로드 (File Upload)** - [Server-Side] 서버 장악 방지 및 웹쉘(Webshell) 차단 시큐어 코딩
    * *Deep Dive: 2026년 가이드라인(FU-14) 기준의 통합 보안 전략 분석 포함*

### 4. 인증 및 권한 관리 (Authentication & Authorization)
* **13. 불충분한 인증 (Insufficient Authentication)** - 중요 페이지 접근 통제 및 세션 검증 로직 구현 (Forceful Browsing 방어)
    * *Deep Dive: 21년(단순 인증 여부) vs 26년(인증 절차의 무결성 및 우회 방지) 기준 비교 분석*
* **14. 취약한 패스워드 복구 (Weak Password Recovery)** - 비밀번호 노출 방지 및 재설정 로직의 무결성 검증
    * *Deep Dive: 응답값(Response) 변조 및 파라미터 조작(IDOR)을 통한 인증 우회 시나리오 분석*

---

## 🛠️ 기술 스택 (Tech Stack)
* **Language**: Java (JSP/Servlet)
* **Server**: Apache Tomcat
* **Security**: Secure Coding, Input Validation, Configuration Hardening

## 📝 기여 및 참고 (Reference)
이 문서는 개인 학습용으로 작성되었으며, 실무 환경에 따라 구체적인 설정은 달라질 수 있습니다.