# Security (보안)

## OpenID

**한줄설명:** 여러 웹사이트에서 하나의 계정으로 로그인할 수 있게 해주는 인증 시스템

**상세설명:**
- 특징:
  - 중앙의 OpenID 제공자에서 인증
  - 개별 서비스가 인증 처리하지 않음
  - 사용자는 하나의 계정만 관리
- 현재 사용:
  - OAuth2 + OpenID Connect (OIDC) 조합
  - SNS 로그인 (Google, Facebook, GitHub 등)
- 장점:
  - 사용자 편의성
  - 보안 강화 (OpenID 제공자에서 관리)
  - 서비스 개발 간편화

**리뷰:** 현대 웹 로그인의 표준 방식

---

## OAuth2

**한줄설명:** 다른 서비스에 내 계정 정보를 제공하지 않고 권한만 위임해서 접근할 수 있게 하는 프로토콜

**상세설명:**
- 문제 상황:
  - A 서비스가 B 서비스의 사용자 정보에 접근하려면?
  - 기존: B의 비밀번호를 A에게 알려줌 (위험)
  - OAuth2: 권한 위임으로 해결

- 주요 개념:
  - **Resource Owner**: 사용자
  - **Client**: 권한을 요청하는 애플리케이션
  - **Authorization Server**: 권한을 부여하는 서버 (Google, Facebook)
  - **Resource Server**: 사용자 정보를 가진 서버

- 흐름:
  1. 사용자가 "Google로 로그인" 클릭
  2. 클라이언트가 Google Authorization Server로 리다이렉트
  3. 사용자가 권한 승인
  4. Authorization Server가 Access Token 발급
  5. 클라이언트가 Access Token으로 리소스 접근

- 사용 사례:
  - SNS 로그인
  - API 권한 위임
  - 제3자 애플리케이션에 데이터 접근 권한

**리뷰:** 현대 인증/인가의 표준. 깊은 이해 필수

---

## MFA (Multi-Factor Authentication - 다중 인증)

**한줄설명:** 보안 강화를 위해 두 가지 이상의 인증 수단을 요구하는 방법

**상세설명:**
- 인증 수단:
  1. **지식 기반 (Something You Know)**:
     - 비밀번호
     - 보안 질문

  2. **소유 기반 (Something You Have)**:
     - 휴대폰 (OTP, SMS)
     - 하드웨어 토큰
     - 앱 기반 인증 (Google Authenticator)

  3. **생체 인증 (Something You Are)**:
     - 지문
     - 얼굴 인식
     - 홍채 인식

- 2FA (Two-Factor Authentication):
  - 가장 일반적: 비밀번호 + OTP
  - 예: 은행 로그인 시 비밀번호 + 휴대폰 인증

- 장점:
  - 보안성 크게 향상
  - 비밀번호 탈취 시에도 계정 보호

**리뷰:** 금융, 이메일 등 중요 계정에 필수

---

## PKI (Public Key Infrastructure - 공개키 기반 구조)

**한줄설명:** 암호화와 인증을 위한 공개키-비공개키 쌍을 관리하는 체계

**상세설명:**
- 구성 요소:
  - **공개키 (Public Key)**: 누구에게나 공개, 암호화에 사용
  - **비공개키 (Private Key)**: 본인만 보유, 복호화 및 서명에 사용
  - **인증서 (Certificate)**: 공개키의 소유자 정보 검증
  - **CA (Certificate Authority)**: 인증서 발급 기관

- 사용 사례:
  - HTTPS 통신 (웹 서버 인증)
  - 전자 서명
  - SSH 인증
  - VPN 연결

- 원리:
  ```
  송신자: 메시지 + 비공개키 → 암호화 → 수신자에게 전송
  수신자: 수신한 메시지 + 송신자 공개키 → 복호화 → 검증
  ```

**리뷰:** HTTPS와 전자서명의 기반 기술

---

## 바이러스

**한줄설명:** 자기 자신을 복제하여 컴퓨터 시스템을 해치는 악성 소프트웨어

**상세설명:**
- 특징:
  - 자기 복제 능력
  - 다른 프로그램에 감염
  - 숙주 프로그램 필요
  - 사용자 행동으로 확산 (파일 실행, USB 등)

- 피해:
  - 성능 저하
  - 파일 손상
  - 데이터 유출
  - 시스템 마비

- 방지:
  - 신뢰할 수 있는 소스에서만 다운로드
  - 백신 소프트웨어 설치
  - 정기적 업데이트

**리뷰:** 기본적인 악성 소프트웨어 개념

---

## 랜섬웨어 (Ransomware)

**한줄설명:** 파일을 암호화하여 사용 불가능하게 만들고 복구 비용을 요구하는 악성 소프트웨어

**상세설명:**
- 작동 방식:
  1. 시스템 감염
  2. 중요 파일 암호화
  3. 복구를 위해 금액 요구
  4. 지불하면 복호화 키 제공 (약속)

- 특징:
  - 높은 피해액
  - 신속한 확산
  - 암호화 강력함 (거의 복구 불가능)
  - 추적 어려움 (암호화폐 거래)

- 방지:
  - 정기적 백업
  - 최신 보안 패치
  - 의심 파일 실행 금지
  - 보안 소프트웨어 설치

**리뷰:** 현대의 가장 위험한 위협 중 하나

---

## 악성코드 (Malware)

**한줄설명:** 컴퓨터 시스템에 해를 끼치도록 설계된 모든 악의적 소프트웨어의 총칭

**상세설명:**
- 종류:
  1. **바이러스**: 자기 복제, 다른 프로그램 감염
  2. **웜**: 자기 복제만 함 (독립 실행)
  3. **트로얀목마**: 정상 프로그램으로 위장
  4. **랜섬웨어**: 파일 암호화 후 돈 요구
  5. **스파이웨어**: 사용자 정보 수집
  6. **애드웨어**: 광고 표시
  7. **루트킷**: 시스템 권한 탈취
  8. **보트넷**: 감염된 컴퓨터들의 네트워크

**리뷰:** 악성코드의 다양한 유형 이해 필요

---

## 암호화 (Encryption)

**한줄설명:** 원본 데이터를 알 수 없는 형태로 변환하여 허가된 사람만 읽을 수 있도록 하는 기술

**상세설명:**
- 종류:
  1. **대칭키 암호화 (Symmetric Encryption)**:
     - 같은 키로 암호화/복호화
     - 빠르지만 키 관리 어려움
     - 예: AES, DES

  2. **비대칭키 암호화 (Asymmetric Encryption)**:
     - 공개키로 암호화, 비공개키로 복호화
     - 느리지만 안전
     - 예: RSA, ECC

- 사용:
  - 통신 보안 (HTTPS)
  - 저장 데이터 보안
  - 인증 및 서명

**리뷰:** 정보보안의 핵심 기술

---

## 복호화 (Decryption)

**한줄설명:** 암호화된 데이터를 원본 형태로 변환하는 과정

**상세설명:**
- 적법한 복호화:
  - 올바른 키를 가진 경우만 가능
  - 암호화의 역 과정

- 불법 복호화 (공격):
  - 무작위 대입 (Brute Force)
  - 암호 분석 (Cryptanalysis)
  - 키 탈취

**리뷰:** 암호화와 쌍을 이루는 개념

---

## 단방향 암호화

**한줄설명:** 원본 데이터를 고정된 형태로 변환하여 역으로 원본을 추출할 수 없는 암호화

**상세설명:**
- 특징:
  - 복호화 불가능 (의도적 설계)
  - 같은 입력값은 항상 같은 출력
  - 작은 입력 변화도 완전히 다른 출력 (Avalanche Effect)

- 사용:
  - 비밀번호 저장
  - 데이터 무결성 검증 (해시)
  - 메시지 인증 코드 (MAC)

**리뷰:** 비밀번호는 반드시 단방향 암호화로 저장할 것

---

## 해시 (Hash)

**한줄설명:** 임의의 길이의 데이터를 고정된 길이의 고유한 값으로 변환하는 함수

**상세설명:**
- 특징:
  - 단방향 (역 계산 불가능)
  - 결정론적 (같은 입력은 항상 같은 출력)
  - 고정 길이 출력
  - 입력의 작은 변화도 다른 출력
  - 충돌 저항성 (두 입력이 같은 해시값을 가질 가능성 극히 낮음)

- 대표 해시 함수:
  - **MD5**: 취약함 (사용 금지)
  - **SHA-1**: 약간 취약함 (권장하지 않음)
  - **SHA-256**: 안전함 (권장)
  - **SHA-3**: 최신, 매우 안전

- 사용:
  ```python
  import hashlib
  password = "mypassword"
  hashed = hashlib.sha256(password.encode()).hexdigest()
  # hashed = "8d969eef6ecad3c29a3a873fba2d9dada3d1abe5ff3f1890f40e3dce4f61b1ad"
  ```

**리뷰:** 비밀번호 저장의 표준 방식

---

## OWASP Top 10

**한줄설명:** 웹 애플리케이션의 가장 취약한 보안 위협 상위 10가지

**상세설명:**
- OWASP (Open Web Application Security Project)에서 2년마다 발표
- 2021년 기준:
  1. **Broken Access Control**: 접근 제어 오류
  2. **Cryptographic Failures**: 암호화 실패
  3. **Injection**: SQL Injection, 명령어 Injection 등
  4. **Insecure Design**: 보안을 고려하지 않은 설계
  5. **Security Misconfiguration**: 잘못된 보안 설정
  6. **Vulnerable Components**: 취약한 의존성 라이브러리
  7. **Identification Failures**: 인증 실패
  8. **Software Data Integrity Failures**: 데이터 무결성 실패
  9. **Logging & Monitoring Failures**: 로깅 및 모니터링 부족
  10. **SSRF (Server-Side Request Forgery)**: 서버 측 요청 위조

**리뷰:** 웹 개발자는 필수적으로 숙지해야 할 보안 위협

---

## 시큐어 코딩 (Secure Coding)

**한줄설명:** 보안 취약점을 고려하여 안전하게 코드를 작성하는 방식

**상세설명:**
- 원칙:
  1. **입력값 검증**: 모든 입력값을 의심하고 검증
  2. **최소 권한**: 필요한 최소한의 권한만 부여
  3. **기본 보안**: 보안을 기본 가정 (보안은 추가 아님)
  4. **오류 처리**: 민감 정보 노출 금지
  5. **암호화**: 민감한 데이터는 암호화

- 예시:
  ```python
  # 취약한 코드
  username = request.args.get('username')
  query = f"SELECT * FROM users WHERE username = '{username}'"
  db.execute(query)

  # 안전한 코드 (매개변수화된 쿼리)
  username = request.args.get('username')
  query = "SELECT * FROM users WHERE username = ?"
  db.execute(query, (username,))
  ```

**리뷰:** 모든 개발자가 의식적으로 실천해야 할 습관

---

## 입력값 검증 (Input Validation)

**한줄설명:** 사용자로부터 받은 모든 입력이 예상하는 형식과 범위인지 확인하는 과정

**상세설명:**
- 검증 항목:
  - 데이터 타입 (숫자, 문자 등)
  - 길이 (최소/최대 길이)
  - 형식 (이메일, 전화번호 등)
  - 범위 (최소/최대 값)
  - 허용된 값만 (Whitelist)

- 예시:
  ```python
  def validate_email(email):
      import re
      pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
      return re.match(pattern, email) is not None

  def validate_age(age):
      try:
          age = int(age)
          return 0 <= age <= 150
      except ValueError:
          return False
  ```

- 위험한 공격들:
  - SQL Injection
  - XSS (Cross-Site Scripting)
  - Command Injection
  - Path Traversal

**리뷰:** 보안의 첫 번째 방어선

---

## Safety Check

**한줄설명:** 코드 실행 중에 예상치 못한 상황을 감지하고 처리하는 검증

**상세설명:**
- 종류:
  1. **Null Check**: NULL 포인터 접근 방지
  2. **Bounds Check**: 배열 범위 초과 방지
  3. **Type Check**: 타입 불일치 방지
  4. **Resource Check**: 리소스(파일, DB 연결) 할당 확인

- 예시:
  ```python
  # Null Check
  if user is None:
      raise ValueError("User not found")

  # Bounds Check
  if index < 0 or index >= len(array):
      raise IndexError("Index out of bounds")

  # Resource Check
  with open('file.txt', 'r') as f:
      data = f.read()
  # 파일이 자동으로 닫힘
  ```

**리뷰:** 런타임 오류와 보안 문제를 방지하는 기본

---

## SQL Injection (SQL 인젝션)

**한줄설명:** 입력값을 검증하지 않아 악의적인 SQL 코드가 실행되는 공격

**상세설명:**
- 원리:
  ```python
  # 취약한 코드
  username = input("Username: ")  # admin' --
  password = input("Password: ")  # anything
  query = f"SELECT * FROM users WHERE username='{username}' AND password='{password}'"
  # 실행되는 쿼리:
  # SELECT * FROM users WHERE username='admin' --' AND password='anything'
  # -- 이후는 주석 처리되어 암호 검증 무시됨
  ```

- 공격 유형:
  1. **Authentication Bypass**: 인증 우회
  2. **Data Extraction**: 데이터 탈취
  3. **Data Manipulation**: 데이터 변조
  4. **System Command**: 시스템 명령 실행

- 방어:
  ```python
  # 매개변수화된 쿼리 (Prepared Statement)
  query = "SELECT * FROM users WHERE username=? AND password=?"
  cursor.execute(query, (username, password))
  ```

**리뷰:** 가장 흔한 웹 취약점. 반드시 대비할 것

---

## XSS (Cross-Site Scripting)

**한줄설명:** 웹페이지에 악의적인 스크립트를 삽입하여 사용자의 브라우저에서 실행시키는 공격

**상세설명:**
- 종류:
  1. **Stored XSS** (저장형):
     - 악성 스크립트가 서버에 저장됨
     - 모든 방문자에게 영향
     - 댓글, 게시물에 스크립트 포함

  2. **Reflected XSS** (반사형):
     - 악성 스크립트가 URL에 포함됨
     - 특정 링크 클릭 시만 영향
     - 피싱 메일의 링크 등

  3. **DOM-based XSS**:
     - JavaScript로 DOM 조작 시 발생
     - 서버에 데이터 전송 안 함

- 예시:
  ```html
  <!-- 취약한 코드 -->
  <p>Comment: <%= comment %></p>
  <!-- 공격 페이로드 -->
  <script>alert('XSS')</script>
  <!-- 또는 -->
  <img src=x onerror="stealCookie()">

  <!-- 안전한 코드 (HTML Escape) -->
  <p>Comment: <%=h comment %></p>
  <!-- 또는 -->
  <p>Comment: <div><!-- Text content --></div></p>
  ```

- 방어:
  - 입력값 검증
  - 출력 인코딩 (HTML Escape)
  - Content Security Policy (CSP)
  - HTTP-only 쿠키

**리뷰:** 웹 개발에서 반드시 주의해야 할 공격

---

## CSRF (Cross-Site Request Forgery)

**한줄설명:** 사용자가 의도하지 않은 요청을 다른 사이트에서 강제로 실행하게 하는 공격

**상세설명:**
- 원리:
  1. 사용자가 은행 사이트에 로그인 (세션 유지)
  2. 사용자가 모르게 악의적인 사이트 방문
  3. 악의적 사이트가 은행으로 송금 요청
  4. 브라우저가 은행 세션을 자동으로 포함하여 요청 전송
  5. 요청이 실행됨

- 예시:
  ```html
  <!-- 악의적 사이트 -->
  <img src="https://bank.com/transfer?to=attacker&amount=1000">
  <!-- 또는 -->
  <form action="https://bank.com/transfer" method="POST">
    <input name="to" value="attacker">
    <input name="amount" value="1000">
  </form>
  ```

- 방어:
  - CSRF 토큰 사용
  - SameSite 쿠키 속성
  - 두 단계 인증
  - Referer/Origin 헤더 검증

**리뷰:** 상태 변화 요청(POST, PUT, DELETE)에 특히 주의

---

## CORS (Cross-Origin Resource Sharing)

**한줄설명:** 다른 출처의 리소스를 안전하게 공유하는 메커니즘

**상세설명:**
- 배경:
  - SOP (Same Origin Policy)로 다른 출처 접근 제한
  - API 활용을 위해서는 예외 필요
  - CORS로 안전하게 허용

- 작동 방식:
  - 브라우저가 자동으로 요청 헤더 추가
  - 서버가 응답 헤더로 권한 표시
  - 브라우저가 응답 헤더 확인 후 허용/차단

- 서버 설정 예:
  ```python
  from flask_cors import CORS
  CORS(app, origins=["https://trusted-site.com"])
  ```

- 또는 헤더로:
  ```
  Access-Control-Allow-Origin: https://trusted-site.com
  Access-Control-Allow-Methods: GET, POST
  Access-Control-Allow-Headers: Content-Type
  ```

**리뷰:** API 개발 시 빈번하게 마주치는 문제

---

## OWASP를 넘어선 기타 주요 위협

### DoS / DDoS 공격

**한줄설명:** 서비스를 마비시킬 목적으로 대량의 트래픽을 보내는 공격

**상세설명:**
- **DoS (Denial of Service)**:
  - 한 대의 공격자
  - 상대적으로 적은 트래픽
  - 탐지하기 쉬움

- **DDoS (Distributed DoS)**:
  - 여러 대의 감염된 컴퓨터 (봇넷) 이용
  - 대규모 트래픽
  - 추적과 방어 어려움

- 방어:
  - 속도 제한 (Rate Limiting)
  - WAF (Web Application Firewall)
  - DDoS 대응 서비스
  - 로드 밸런싱

---

### 권한 상승 (Privilege Escalation)

**한줄설명:** 낮은 권한을 가진 사용자가 높은 권한을 얻으려고 시도하는 공격

**상세설명:**
- 종류:
  - **수평 권한 상승**: 같은 레벨의 다른 사용자 권한 탈취
  - **수직 권한 상승**: 관리자 권한 획득

- 방지:
  - 최소 권한 원칙
  - 입력값 검증
  - 권한 관리 시스템 강화

---

### 데이터 유출 (Data Breach)

**한줄설명:** 보안 취약점을 통해 민감한 데이터가 무단으로 노출되는 사건

**상세설명:**
- 원인:
  - 취약한 암호화
  - 권한 관리 부실
  - 내부자 위협
  - SQL Injection 등 공격

- 영향:
  - 개인정보 노출
  - 신뢰도 하락
  - 법적 책임
  - 금전적 손실

- 대응:
  - 즉시 공지
  - 사용자 대응 (비밀번호 변경 등)
  - 법적 절차

---

## 보안 베스트 프랙티스

1. **정기적 보안 업데이트**: 패치 적용
2. **보안 감사**: 취약점 정기 검사
3. **직원 교육**: 보안 인식 제고
4. **백업**: 정기적 데이터 백업
5. **모니터링**: 비정상 활동 감시
6. **인증**: MFA 의무화
7. **암호화**: 민감 데이터 암호화
8. **로깅**: 모든 중요 이벤트 기록

**리뷰:** 보안은 지속적인 노력이 필요한 과정
