# Common (공통)

## 세션 (Session)

**한줄설명:** 서버에 저장되는 사용자 상태 정보

**상세설명:**
- 특징:
  - 서버에 저장 (보안 우수)
  - 세션 ID는 클라이언트에서 쿠키로 관리
  - 발행 주체: 서버
  - 저장 장소: 서버 (메모리, 데이터베이스, 파일 등)
  - 보안: 쿠키보다 안전 (민감 데이터 직접 저장하지 않음)

- 동작:
  ```
  1. 사용자 로그인
  2. 서버가 세션 생성 (Session ID = abc123)
  3. 세션 ID를 쿠키로 클라이언트에 전송
  4. 클라이언트가 이후 요청에 쿠키 자동 포함
  5. 서버가 쿠키의 세션 ID로 사용자 확인
  ```

- 만료:
  - 일정 시간 활동 없으면 자동 만료
  - 로그아웃 시 즉시 삭제

**리뷰:** 전통적인 인증 방식. 서버 부하 주의 필요

---

## 쿠키 (Cookie)

**한줄설명:** 클라이언트(브라우저)에 저장되는 데이터

**상세설명:**
- 특징:
  - 클라이언트에 저장 (로컬 스토리지)
  - 서버가 발행하지만 클라이언트가 관리
  - 자동으로 요청에 포함됨
  - 만료 날짜 설정 가능

- 쿠키 종류:
  1. **Session Cookie**: 브라우저 종료 시 삭제
  2. **Persistent Cookie**: 명시된 만료일까지 유지
  3. **Secure Cookie**: HTTPS에서만 전송
  4. **HttpOnly Cookie**: JavaScript에서 접근 불가능

- 쿠키 설정:
  ```http
  Set-Cookie: sessionId=abc123; Path=/; Expires=Wed, 09 Jun 2025 10:18:14 GMT; HttpOnly; Secure
  ```

- 크기 제한:
  - 개당 최대 4KB
  - 도메인당 최대 20개

- 세션 vs 쿠키:
  | 항목 | 세션 | 쿠키 |
  |------|------|------|
  | 저장위치 | 서버 | 클라이언트 |
  | 보안 | 우수 | 취약 |
  | 서버부하 | 높음 | 낮음 |
  | 속도 | 상대적 느림 | 빠름 |

**리뷰:** 사용자 추적과 상태 유지의 기본 메커니즘

---

## 아나콘다 (Anaconda)

**한줄설명:** Python 패키지 통합 관리 환경

**상세설명:**
- 특징:
  - Python과 필요한 라이브러리를 한 번에 설치
  - 가상환경 관리 기능 포함
  - AI/ML 라이브러리 기본 포함 (NumPy, Pandas, Scikit-learn 등)
  - 패키지 매니저: conda

- 필요성:
  - 여러 프로젝트 동시 진행 시 라이브러리 버전 충돌 가능
  - 가상환경으로 프로젝트별 독립적 환경 구성
  - 다양한 라이브러리 일괄 관리

- 사용:
  ```bash
  conda create -n myproject python=3.9
  conda activate myproject
  conda install numpy pandas
  conda list  # 설치된 패키지 확인
  ```

**리뷰:** Python 데이터 과학 개발의 사실상 표준

---

## 이식성 (Portability)

**한줄설명:** 프로그램이나 시스템이 특정 환경에 종속되지 않고 다양한 환경에서도 잘 작동하는 능력

**상세설명:**
- 중요성:
  - 사용자 환경이 모두 다름 (OS, 브라우저, 하드웨어)
  - 개발 환경과 프로덕션 환경이 다름
  - 이식성 없으면 많은 사용자를 수용할 수 없음

- 높은 이식성 예:
  - 웹 애플리케이션 (모든 브라우저에서 작동)
  - 컨테이너 (Docker)
  - Java (JVM이 있으면 모든 OS에서 작동)

- 낮은 이식성 예:
  - Windows only 소프트웨어
  - 특정 브라우저만 지원
  - OS 특화 프로그램

**리뷰:** 사용자 경험과 서비스 범위에 직결되는 중요한 개념

---

## 형상관리도구 (SCM - Source Code Management)

**한줄설명:** 소스코드의 변경 이력을 관리하고 협업을 도와주는 도구

**상세설명:**
- 목적:
  - 소프트웨어 개발 중 발생하는 모든 **변경 사항(형상)**을 추적하고 기록
  - 변경 이력 확인 (Who, When, What, Why)
  - 이전 버전으로 되돌리기
  - 여러 개발자의 작업 병합
  - 다른 사람의 작업과 비교

- 종류:
  1. **중앙집중형 (Centralized)**:
     - 중앙 서버에 모든 이력 저장
     - 예: SVN, CVS
     - 특징: 중앙 서버 의존, 느린 로컬 작업

  2. **분산형 (Distributed)**:
     - 각 개발자가 완전한 저장소 보유
     - 예: Git, Mercurial
     - 특징: 오프라인 작업 가능, 빠른 성능

**리뷰:** 현대 소프트웨어 개발의 필수 기초

---

## Git

**한줄설명:** 로컬에서 작동하는 분산형 형상관리 도구

**상세설명:**
- 특징:
  - Linus Torvalds가 Linux 커널 개발용으로 만듦
  - 완전한 저장소를 로컬에 보유
  - 오프라인에서도 작업 가능
  - 매우 빠른 성능
  - 강력한 브랜치 관리

- 기본 개념:
  - **Repository (저장소)**: .git 폴더
  - **Working Directory**: 실제 작업 폴더
  - **Staging Area (Index)**: 커밋할 변경사항 모음
  - **Commit**: 스냅샷 저장
  - **Branch**: 독립적 개발 라인

- 기본 명령:
  ```bash
  git init              # 저장소 초기화
  git add .             # 변경사항 스테이징
  git commit -m "msg"   # 커밋
  git push              # 원격 저장소에 업로드
  git pull              # 원격 저장소에서 다운로드
  git branch feature    # 브랜치 생성
  git merge feature     # 브랜치 병합
  ```

**리뷰:** 현재 가장 널리 사용되는 형상관리 도구

---

## GitHub

**한줄설명:** Git 저장소를 인터넷에 공유하고 협업할 수 있게 해주는 플랫폼

**상세설명:**
- 기능:
  - 원격 저장소 호스팅
  - 협업 기능 (Pull Request, Code Review)
  - Issue 트래킹
  - CI/CD 통합 (GitHub Actions)
  - 위키, 프로젝트 관리 도구

- 대안:
  - GitLab: 더 강력한 CI/CD
  - Bitbucket: 비공개 저장소 무료
  - Gitea: 자체 호스팅 용도

- Pull Request 흐름:
  ```
  1. 포크(Fork) 또는 브랜치 생성
  2. 변경사항 커밋
  3. 푸시(Push)
  4. Pull Request 생성
  5. Code Review
  6. 병합(Merge)
  ```

**리뷰:** 오픈소스 개발의 사실상 표준

---

## Repository (저장소)

**한줄설명:** 소스코드와 모든 변경 이력을 저장하는 공간

**상세설명:**
- 종류:
  1. **로컬 저장소**: 자신의 컴퓨터 (.git 폴더)
  2. **원격 저장소**: 인터넷 서버 (GitHub, GitLab)

- 구성:
  - 소스 코드
  - 커밋 이력
  - 브랜치 정보
  - 태그
  - 설정 파일

- 크기:
  - .git 폴더: 프로젝트 크기의 2-3배
  - GitHub: 무료 공개 저장소 무제한, 비공개 무료

**리뷰:** 모든 변경사항의 완전한 기록을 보존

---

## GUI (Graphic User Interface)

**한줄설명:** 그래픽 요소를 사용하여 사용자가 마우스나 터치로 조작하는 방식

**상세설명:**
- 특징:
  - 직관적이고 사용하기 쉬움
  - 시각적 피드백
  - 초보자 친화적
  - 성능 오버헤드

- 예:
  - Windows, macOS, Linux 데스크톱
  - 웹 브라우저
  - 모바일 앱

**리뷰:** 대부분의 최종 사용자 애플리케이션은 GUI 기반

---

## CLI (Command Line Interface)

**한줄설명:** 텍스트 명령어를 입력해서 조작하는 방식

**상세설명:**
- 특징:
  - 강력하고 유연함
  - 자동화 가능
  - 빠른 작업 (반복작업에 유용)
  - 원격 접속 용이
  - 낮은 성능 오버헤드

- 장점:
  ```bash
  # 파일 일괄 변환
  for file in *.txt; do
    convert "$file" "${file%.txt}.pdf"
  done
  ```

- 예:
  - Terminal, Command Prompt, PowerShell
  - SSH를 통한 서버 관리
  - Git, npm, Docker 등 개발 도구

**리뷰:** 개발자는 CLI에 능숙해야 함. 생산성 크게 향상

---

## 환경변수 (Environment Variable)

**한줄설명:** 운영체제나 실행 중인 프로그램이 참고할 수 있도록 키-값 쌍으로 저장된 설정 정보

**상세설명:**
- 특징:
  - 시스템 전체 또는 프로세스 범위에서 접근 가능
  - 설정 값을 코드 밖에서 관리
  - 개발, 테스트, 프로덕션 환경 구분 가능

- 설정 방식:
  ```bash
  # Linux/Mac
  export API_KEY=my_secret_key
  export NODE_ENV=production

  # Windows
  set DATABASE_URL=postgresql://localhost/mydb

  # .env 파일 (프로젝트별)
  API_KEY=my_secret_key
  DATABASE_URL=postgresql://localhost/mydb
  ```

- 접근 방식:
  ```python
  import os
  api_key = os.environ.get('API_KEY')
  ```

- 중요 환경변수:
  - PATH: 실행 파일 찾기 경로
  - HOME: 사용자 홈 디렉토리
  - NODE_ENV: Node.js 환경 (development/production)
  - DATABASE_URL: 데이터베이스 연결 정보

**리뷰:** 보안과 설정 관리의 기본. 민감 정보는 반드시 환경변수로 관리할 것

---

## PATH (경로)

**한줄설명:** 운영체제가 명령어를 실행할 때 해당 실행 파일을 찾기 위해 참조하는 폴더들의 목록

**상세설명:**
- 동작:
  ```bash
  $ python
  # OS가 PATH에 등록된 폴더들을 순서대로 검색
  # /usr/bin/python, /usr/local/bin/python 등에서 찾음
  ```

- 확인:
  ```bash
  echo $PATH  # Linux/Mac
  echo %PATH%  # Windows
  ```

- 설정:
  ```bash
  # Linux/Mac (.bashrc 또는 .zshrc)
  export PATH="/usr/local/bin:$PATH"

  # Windows: 시스템 환경변수 설정에서 PATH 편집
  ```

- 문제 해결:
  - 설치한 프로그램을 찾을 수 없음 → PATH에 추가
  - 잘못된 버전 사용 → PATH 순서 조정

**리뷰:** CLI 환경에서 매우 중요한 개념

---

## FIDO (Fast Identity Online)

**한줄설명:** 생체인증에 대한 표준으로, 비밀번호를 대체하는 생체 인증 기반의 국제 표준 인증 기술

**상세설명:**
- 특징:
  - 비밀번호 제거
  - 생체 인증 표준화
  - 피싱 공격 방지
  - 사용 편의성

- 인증 방식:
  - 지문 인식
  - 얼굴 인식
  - 음성 인식
  - 보안 키

- 사용:
  - Windows Hello (지문, 얼굴)
  - Apple Face ID
  - Android 생체인증
  - 금융기관 보안

**리뷰:** 미래의 인증 방식. 점차 확대될 것으로 예상

---

## Origin (원점)

**한줄설명:** Git에서 원격 저장소를 가리키는 기본 이름

**상세설명:**
- 특징:
  - 기본 원격 저장소
  - 보통 GitHub 등의 저장소
  - 여러 원격 저장소 설정 가능

- 사용:
  ```bash
  git remote -v  # 원격 저장소 확인
  git push origin main  # origin에 푸시
  git pull origin main  # origin에서 풀
  git remote add upstream https://...  # 다른 원격 저장소 추가
  ```

- 일반적인 흐름:
  ```
  원본 저장소 (upstream)
      ↓
  포크한 저장소 (origin)
      ↓
  로컬 저장소
  ```

**리뷰:** Git 협업의 기본 용어

---

## Gitflow

**한줄설명:** Git 브랜치를 체계적으로 관리하는 워크플로우 전략

**상세설명:**
- 브랜치 종류:
  1. **main**: 프로덕션 배포 가능한 안정적 코드
  2. **develop**: 다음 릴리스를 위한 개발 브랜치
  3. **feature**: 새로운 기능 개발 (develop에서 분기)
  4. **release**: 릴리스 준비 (develop에서 분기)
  5. **hotfix**: 프로덕션 버그 수정 (main에서 분기)

- 흐름:
  ```
  main (v1.0.0)
    ↓
  develop
    ├─ feature/login
    ├─ feature/signup
    └─ feature/payment

  develop → release/v1.1.0 → main (v1.1.0 릴리스)

  main의 버그 → hotfix/critical-bug → main & develop
  ```

- 장점:
  - 명확한 브랜치 구조
  - 릴리스 관리 체계적
  - 팀 협업 용이

- 단점:
  - 복잡도 높음
  - 빈번한 merge 필요

**리뷰:** 중규모 이상 프로젝트에서 널리 사용되는 표준

---

## SEO (Search Engine Optimization)

**한줄설명:** 검색엔진 최적화 - 웹사이트가 검색 결과에서 높이 노출되도록 하는 기법

**상세설명:**
- On-page SEO:
  - 제목 (Title), 메타 설명 (Meta Description)
  - 헤더 태그 (H1, H2, H3)
  - 키워드 사용
  - 이미지 alt 텍스트
  - URL 구조

- Off-page SEO:
  - 백링크 (다른 사이트에서의 링크)
  - 소셜 미디어 공유
  - 브랜드 언급

- Technical SEO:
  - 페이지 로딩 속도
  - 모바일 반응형 디자인
  - 사이트맵
  - 시맨틱 HTML 마크업

- 도구:
  - Google Search Console
  - Google Analytics
  - Lighthouse

**리뷰:** 웹 비즈니스의 필수 요소

---

## 웹 접근성 (Web Accessibility)

**한줄설명:** 장애인을 포함한 모든 사용자가 웹사이트를 동등하게 이용할 수 있도록 하는 설계

**상세설명:**
- 종류:
  1. **시각 장애**: 스크린 리더 지원
  2. **청각 장애**: 자막, 수어 제공
  3. **지체 장애**: 키보드 네비게이션
  4. **인지 장애**: 명확한 언어, 단순한 구조

- 기술적 구현:
  - 시맨틱 HTML 마크업
  - ARIA (Accessible Rich Internet Applications) 속성
  - 이미지 alt 텍스트
  - 색상만으로 정보 전달 금지
  - 충분한 명도 대비
  - 키보드 네비게이션 지원

- 표준:
  - WCAG (Web Content Accessibility Guidelines)
  - WCAG 2.1 AA 레벨 권장

**리뷰:** 법적 요구사항일 뿐 아니라 윤리적 책임

---

## KIOSK (키오스크)

**한줄설명:** 터치 스크린 기반의 셀프 서비스 대형 기계

**상세설명:**
- 특징:
  - 사용자가 직접 조작
  - 직원 개입 최소화
  - 24시간 운영 가능
  - 운영 비용 절감

- 사용 예:
  - 카페/식당 주문
  - 영화표 예매
  - 은행 업무
  - 공항 체크인
  - 지하철 승차권

- 개발:
  - 하드웨어: 터치 스크린, 키보드, 결제 단말
  - 소프트웨어: UI/UX 최적화 필수 (직관성)
  - 네트워크: 결제, 주문 처리

**리뷰:** 점점 더 많은 서비스에서 도입되는 추세

---

## MDN (Mozilla Developer Network)

**한줄설명:** Mozilla에서 운영하는 웹 기술(HTML, CSS, JavaScript 등)에 대한 공식 개발자 문서 사이트

**상세설명:**
- 특징:
  - 완전하고 신뢰할 수 있는 문서
  - 다양한 언어 지원 (한국어 포함)
  - 예제 코드 풍부
  - 커뮤니티 기여
  - 무료

- 주요 섹션:
  - HTML 레퍼런스
  - CSS 레퍼런스
  - JavaScript 가이드
  - Web API 문서
  - 웹 개발 학습

- URL: https://developer.mozilla.org/

**리뷰:** 웹 개발자의 첫 번째 참고 자료

---

## 모질라 (Mozilla)

**한줄설명:** 웹 브라우저와 웹 기술 개발을 주도하는 비영리 단체

**상세설명:**
- 역사:
  - 원래 Netscape 커뮤니티에서 시작
  - Netscape Navigator: 과거 가장 인기 있는 브라우저
  - Microsoft Internet Explorer에 밀려남
  - 1998년 Mozilla 재설립

- 주요 제품:
  - **Firefox**: 브라우저 (현재 주력)
  - **Thunderbird**: 이메일 클라이언트
  - MDN: 개발자 문서

- 활동:
  - 웹 표준 개발
  - 웹 개방성 및 자유도 옹호
  - 개인정보 보호 강화

**리뷰:** 웹 개방성의 대표 주자

---

## 16진수 (Hexadecimal)

**한줄설명:** 0~15까지 숫자를 0~F로 표현하는 진법

**상세설명:**
- 기수법:
  - 10진수: 0-9 (기수 10)
  - 16진수: 0-9, A-F (기수 16)
  - 표기법: 0x로 시작 (예: 0xFF)

- 변환:
  ```
  16진수 FF = 15×16¹ + 15×16⁰ = 240 + 15 = 255 (10진수)
  ```

- 특징:
  - 한 자리 16진수 = 4비트
  - 한 글자 16진수 = 8비트 (1바이트)
  - 2자리 16진수: 00~FF (0~255)

- 사용:
  - 색상 표현: #RRGGBB (예: #FF0000 = 빨강)
  - 메모리 주소
  - 바이너리 데이터 표현
  - UUID, 해시값 표시

- 예:
  ```
  #FF0000: Red (255, 0, 0)
  #00FF00: Green (0, 255, 0)
  #0000FF: Blue (0, 0, 255)
  #FFFFFF: White (255, 255, 255)
  #000000: Black (0, 0, 0)
  ```

**리뷰:** 프로그래밍에서 자주 사용되므로 빠른 변환 능력 필수

---

## 헥스코드 (HEX Color Code)

**한줄설명:** #rrggbb 형태로 각 색상을 16진수로 표현한 색상 코드

**상세설명:**
- 형식: #RRGGBB
  - RR: Red (00~FF = 0~255)
  - GG: Green (00~FF = 0~255)
  - BB: Blue (00~FF = 0~255)

- 범위:
  - 최소: #000000 (검정)
  - 최대: #FFFFFF (흰색)
  - 총 색상 수: 256 × 256 × 256 = 16,777,216가지

- 예:
  ```
  #FF0000: 빨강
  #00FF00: 초록
  #0000FF: 파랑
  #FFFF00: 노랑 (빨강 + 초록)
  #FF00FF: 마젠타 (빨강 + 파랑)
  #00FFFF: 시안 (초록 + 파랑)
  #808080: 회색
  ```

- 다른 표현:
  ```css
  /* 헥스코드 */
  color: #FF0000;

  /* RGB */
  color: rgb(255, 0, 0);

  /* RGBA (알파 투명도) */
  color: rgba(255, 0, 0, 0.5);

  /* 색상 이름 */
  color: red;
  ```

**리뷰:** 웹 개발에서 가장 널리 사용되는 색상 표현 방식

---

## IEEE (Institute of Electrical and Electronics Engineers)

**한줄설명:** 국제 표준화 기구로, 전기, 전자, 통신, 컴퓨터 분야의 표준을 제정하는 조직

**상세설명:**
- 기능:
  - 기술 표준 개발
  - 교육 및 전문성 인증
  - 학술지 발행
  - 컨퍼런스 개최

- 주요 표준:
  - IEEE 802.11: Wi-Fi
  - IEEE 802.3: 이더넷
  - IEEE 754: 부동소수점 수 표준
  - IEEE 802.15: Bluetooth

**리뷰:** 기술 표준의 주요 제정 기관

---

## Deprecated (더 이상 사용 권장하지 않음)

**한줄설명:** 구 버전에 있던 기능으로 새 버전에서는 더 이상 지원하지 않는 경우에 나타나는 경고

**상세설명:**
- 의미:
  - 기능이 곧 제거될 예정
  - 더 이상 업데이트되지 않음
  - 대체 기능 사용 권장

- 예:
  ```html
  <!-- Deprecated: HTML4 -->
  <center>Text</center>

  <!-- 대체: CSS -->
  <p style="text-align: center;">Text</p>

  <!-- JavaScript -->
  // Deprecated
  var x = 10;
  // 사용 권장: let, const
  let x = 10;
  const y = 20;
  ```

- 실행:
  - 여전히 작동할 수 있음
  - 브라우저 콘솔에 경고 표시
  - 언제 제거될지 알 수 없음

**리뷰:** 코드 작성 시 deprecated 기능 피할 것

---

## CDN (Content Delivery Network)

**한줄설명:** 지리적으로 분산된 서버들로 콘텐츠를 빠르게 전달하는 네트워크

**상세설명:**
- 특징:
  - 전 세계에 많은 서버 (PoP - Point of Presence)
  - 사용자에 가장 가까운 서버에서 콘텐츠 제공
  - 빠른 로딩 속도
  - 원본 서버 부하 감소

- 장점:
  - 페이지 로딩 속도 향상
  - 대역폭 비용 절감
  - 장애 복구력 (Failover)
  - 보안 강화 (DDoS 방어)

- 캐싱 대상:
  - 이미지, CSS, JavaScript 등 정적 파일
  - 동영상 스트리밍
  - API 응답

- 주요 CDN 서비스:
  - Cloudflare
  - AWS CloudFront
  - Google Cloud CDN
  - Akamai

**리뷰:** 글로벌 서비스 제공 시 필수

---

## 생성형 AI (Generative AI)

**한줄설명:** 확률 기반으로 다음 단어를 예측하는 모델로 텍스트, 이미지, 음성 등을 생성하는 AI

**상세설명:**
- 원리:
  - 대규모 데이터 학습
  - 확률 분포 학습
  - 다음 토큰 예측
  - 반복해서 생성

- 모델:
  - **LLM (Large Language Model)**: GPT, Claude
  - **이미지 생성**: DALL-E, Stable Diffusion
  - **음성 생성**: WaveNet, Tacotron
  - **비디오 생성**: Runway, Synthesia

- 응용:
  - 콘텐츠 작성
  - 코드 생성
  - 질문 답변
  - 이미지/비디오 생성
  - 자동화된 고객 지원

- 주의:
  - 환각 (Hallucination): 잘못된 정보 생성
  - 학습 데이터의 편향
  - 저작권 문제
  - 보안 위협

**리뷰:** 현재 AI 발전의 가장 주목할 분야

---

## DevOps

**한줄설명:** 개발(Development)과 운영(Operations)을 결합하여 소프트웨어 개발 및 제공 프로세스를 개선하는 방법론

**상세설명:**
- 목표:
  - 개발과 운영 팀 간 벽 제거
  - 배포 빈도 증가
  - 배포 시간 단축
  - 릴리스 안정성 향상
  - 빠른 문제 해결

- 핵심 기능:
  1. **자동화**: CI/CD 파이프라인
  2. **모니터링**: 실시간 로그 분석
  3. **협업**: 개발자와 운영팀 소통
  4. **Infrastructure as Code**: 인프라 코드화

- 기술:
  - Docker, Kubernetes
  - Jenkins, GitLab CI
  - Prometheus, Grafana
  - Terraform, Ansible

**리뷰:** 현대 소프트웨어 개발의 핵심 실천법

---

## 경계값 테스트 (Boundary Testing)

**한줄설명:** 변수의 경계값(최소, 최대, 임계값)에서의 동작을 테스트하는 기법

**상세설명:**
- 목적:
  - 예상 범위의 경계에서 오류 가능성 높음
  - 일반 값은 정상이지만 경계값에서 실패할 수 있음

- 예:
  ```
  나이 입력 범위: 0~150
  테스트 값: -1, 0, 1, 149, 150, 151

  배열 인덱스 범위: 0~9
  테스트 값: -1, 0, 1, 8, 9, 10
  ```

- 테스트 케이스:
  - 최소값 - 1
  - 최소값
  - 최소값 + 1
  - 최대값 - 1
  - 최대값
  - 최대값 + 1

**리뷰:** 효율적인 테스트 전략

---

## QA (Quality Assurance)

**한줄설명:** 제품의 품질을 보장하기 위한 활동

**상세설명:**
- 범위:
  - 요구사항 검증
  - 테스트 계획 수립
  - 테스트 실행 (수동, 자동)
  - 결함 리포팅
  - 성능 및 보안 검사

- 테스트 유형:
  - 기능 테스트 (정상 동작 확인)
  - 호환성 테스트 (다양한 환경)
  - 성능 테스트 (속도, 메모리)
  - 보안 테스트 (취약점 검사)
  - 사용성 테스트 (UX 평가)

- 프로세스:
  ```
  개발 → QA 테스트 → 결함 발견 → 개발자 수정 → QA 재테스트 → 출시
  ```

**리뷰:** 높은 품질 제품의 필수 요소

---

## 이진 탐색 (Binary Search)

**한줄설명:** 탐색 범위를 반으로 줄여가며 정렬된 배열에서 데이터를 찾는 효율적인 알고리즘

**상세설명:**
- 동작 원리:
  1. 중간값 확인
  2. 찾는 값과 비교
  3. 범위를 절반으로 축소
  4. 반복

- 예:
  ```
  배열: [1, 3, 5, 7, 9, 11, 13, 15]
  찾는 값: 7

  Step 1: 중간값 7 (인덱스 3) → 찾음! 완료
  ```

- 시간 복잡도: **O(log₂n)**
  - n개 데이터: log₂n번의 탐색으로 충분
  - 예: 1,000,000개 데이터 → 약 20번의 비교

- 선형 탐색과 비교:
  - 선형 탐색: O(n) - 순서대로 확인
  - 이진 탐색: O(log n) - 훨씬 빠름

- 조건:
  - 데이터가 **정렬**되어 있어야 함
  - 랜덤 액세스 가능해야 함

**리뷰:** 알고리즘 면접 필출 주제. 구현도 연습할 것

---

## 순차 검색 (Sequential/Linear Search)

**한줄설명:** 데이터를 처음부터 끝까지 순서대로 하나씩 확인하는 검색 방법

**상세설명:**
- 동작:
  ```
  배열: [3, 1, 4, 1, 5, 9]
  찾는 값: 4

  3 → 1 → 4 (찾음!) → 중지
  ```

- 시간 복잡도: **O(n)**
  - 최악의 경우 모든 요소 확인
  - 평균 n/2번 비교

- 장점:
  - 구현 간단
  - 정렬 불필요
  - 링크드 리스트에도 사용 가능

- 단점:
  - 느린 속도 (대규모 데이터)

**리뷰:** 기초이지만 실제로는 이진 탐색이 더 자주 사용됨

---

## SI (System Integration)

**한줄설명:** 서로 다른 시스템(하드웨어, 소프트웨어)을 하나의 통합된 시스템으로 구축하는 작업

**상세설명:**
- 범위:
  - 하드웨어 설치 및 구성
  - 소프트웨어 설치 및 통합
  - 네트워크 구축
  - 데이터 마이그레이션
  - 보안 및 백업 구성

- SI 회사:
  - 클라이언트로부터 프로젝트 외주 수락
  - 시스템 구축 및 통합
  - 유지보수 서비스 제공
  - 대규모 ERP, 전산시스템 등 담당

- 특징:
  - 높은 비용 (수십억 원 대)
  - 오래 걸림 (수개월~수년)
  - 클라이언트별 커스터마이징
  - 기술적으로 배울 기회 적음

- 한국에서의 입장:
  - 많은 IT 회사가 SI 사업 중심
  - 급여는 높지만 기술 성장에 한계
  - 최근 스타트업과 기술 회사로의 전환 추세

**리뷰:** SI 경험은 좋으나 장기 경력으로는 추천하지 않는 경향

---

## 동기 방식 (Synchronous)

**한줄설명:** 요청을 보낸 후 응답이 올 때까지 기다리는 블로킹 방식

**상세설명:**
- 특징:
  - 순차적 실행
  - 앞의 작업이 완료되어야 다음 작업 시작
  - 응답을 받을 때까지 블로킹

- 예:
  ```python
  result = database.query()  # 완료될 때까지 대기
  print(result)              # 쿼리 완료 후 실행
  ```

- 장점:
  - 프로그래밍 간단
  - 디버깅 용이
  - 예측 가능한 동작

- 단점:
  - 느린 성능
  - 응답 시간이 긴 작업에서 병목

**리뷰:** 기본적인 프로그래밍 방식

---

## 비동기 방식 (Asynchronous)

**한줄설명:** 요청을 보낸 후 기다리지 않고 다음 작업을 수행하며, 응답은 나중에 처리하는 논블로킹 방식

**상세설명:**
- 특징:
  - 동시에 여러 작업 처리
  - 응답을 기다리지 않음
  - 콜백, Promise, async/await로 구현

- 예:
  ```javascript
  // 콜백 방식
  database.query(function(result) {
    console.log(result);
  });
  console.log("Query 시작");  // 먼저 실행됨

  // Promise 방식
  database.query()
    .then(result => console.log(result))

  // async/await 방식
  const result = await database.query();
  console.log(result);
  ```

- 대부분의 언어는 기본 동기:
  - JavaScript는 비동기 기반 (이벤트 루프)
  - Python, Java도 비동기 지원 (asyncio, CompletableFuture)

- 장점:
  - 빠른 응답 시간
  - 동시 처리 가능
  - 높은 성능

- 단점:
  - 프로그래밍 복잡
  - 디버깅 어려움
  - Callback Hell 가능

**리뷰:** 현대 웹/앱 개발의 필수 개념

---

## 예외 처리 (Exception Handling)

**한줄설명:** 프로그램 실행 중 발생할 수 있는 예상치 못한 상황(오류)을 처리하여 프로그램이 중단되지 않도록 하는 기법

**상세설명:**
- 목적:
  - 프로그램 크래시 방지
  - 오류 정보 수집
  - 복구 가능한 오류 처리
  - 사용자 경험 향상

- 문법:
  ```python
  try:
      # 오류 발생 가능한 코드
      result = 10 / 0
  except ZeroDivisionError:
      # 특정 오류 처리 (구체적일수록 좋음)
      print("0으로 나눌 수 없습니다")
  except Exception:
      # 모든 오류 처리 (마지막에만)
      print("알 수 없는 오류")
  finally:
      # 오류 여부와 관계없이 항상 실행
      print("정리 작업")
  ```

- 베스트 프랙티스:
  - try는 좁을수록 좋음 (최소한의 코드만)
  - except는 구체적일수록 좋음 (넓은 범위 피하기)
  - 모든 Exception을 catch하지 말 것 (의도적 raise도 있음)
  - 로깅: 오류 정보 기록

- 커스텀 예외:
  ```python
  class InvalidAgeError(Exception):
      pass

  if age < 0:
      raise InvalidAgeError("나이는 음수일 수 없습니다")
  ```

**리뷰:** 견고한 프로그래밍의 필수 요소

---

## 콜백 함수 (Callback Function)

**한줄설명:** 다른 함수의 인수로 전달되어 나중에 호출되는 함수

**상세설명:**
- 특징:
  - 어떤 작업이 완료된 후에 나중에 호출됨
  - 비동기 작업에서 주로 사용
  - 실행 순서 제어 가능

- 예:
  ```javascript
  // 콜백 함수
  function processData(data, callback) {
    setTimeout(() => {
      const result = data * 2;
      callback(result);  // 나중에 호출
    }, 1000);
  }

  processData(5, (result) => {
    console.log(result);  // 1초 후 10 출력
  });
  ```

- 문제점:
  - Callback Hell: 중첩 깊어짐
  - 오류 처리 복잡
  - 코드 가독성 저하

- 해결책:
  - Promise 사용
  - async/await 사용

**리뷰:** 비동기 처리의 기초이지만 Promise/async가 더 권장됨

---

## 리팩토링 (Refactoring)

**한줄설명:** 기능 동작의 변경 없이 코드를 유지보수성이 좋게 재구성하는 것

**상세설명:**
- 목적:
  - 코드 가독성 향상
  - 유지보수성 증대
  - 버그 발생 가능성 감소
  - 성능 최적화

- 대상:
  - 중복 코드 제거
  - 긴 메서드 분해
  - 복잡한 조건문 단순화
  - 변수명/함수명 개선
  - 불필요한 코드 삭제

- 예:
  ```python
  # Before: 복잡하고 반복적
  if age >= 18 and age < 65:
      print("Working age")
  if marital == "married":
      print("married")
  if has_insurance == True:
      print("has insurance")

  # After: 간결하고 명확
  def is_working_age(age):
      return 18 <= age < 65

  def print_user_info(age, marital, has_insurance):
      if is_working_age(age):
          print("Working age")
      if marital == "married":
          print("Married")
      if has_insurance:
          print("Has insurance")
  ```

- 중요: 기능 동작 변경 금지
  - 리팩토링 후 테스트 필수
  - 단위 테스트 있으면 안전함

**리뷰:** 전문 개발자의 필수 습관. 기술 부채 해결의 방법

---

## CSV (Comma Separated Value)

**한줄설명:** 쉼표로 데이터를 구분하여 저장하는 파일 형식

**상세설명:**
- 특징:
  - 각 필드(열)를 쉼표로 구분
  - 각 레코드(행)를 줄바꿈으로 구분
  - 단순하고 가벼움
  - 모든 스프레드시트 프로그램 지원

- 예:
  ```csv
  name,age,email
  John,30,john@example.com
  Jane,28,jane@example.com
  Bob,35,bob@example.com
  ```

- 읽고 쓰기:
  ```python
  import csv

  # 읽기
  with open('data.csv', 'r') as f:
      reader = csv.DictReader(f)
      for row in reader:
          print(row['name'], row['age'])

  # 쓰기
  with open('data.csv', 'w') as f:
      writer = csv.DictWriter(f, fieldnames=['name', 'age', 'email'])
      writer.writeheader()
      writer.writerow({'name': 'John', 'age': 30, 'email': 'john@example.com'})
  ```

**리뷰:** 데이터 교환의 표준 형식. 간단하고 호환성 우수

---

## 프로그래밍 언어 분류

### 컴파일 언어 (Compiled Language)

**한줄설명:** 소스코드 전체를 기계어로 미리 변환한 후 실행하는 언어

**상세설명:**
- 과정:
  ```
  소스코드 → 컴파일러 → 기계어(실행 파일) → 실행
  ```

- 특징:
  - 컴파일 시간 필요
  - 모든 코드를 미리 오류 체크
  - 실행 속도 빠름
  - 배포 시 실행 파일만 전달

- 예: C, C++, Java, Go, Rust

- 장점:
  - 빠른 실행 속도
  - 문법/타입 오류 조기 발견
  - 최적화 가능

- 단점:
  - 개발 시간 증가 (컴파일 대기)
  - 배포 번거로움

### 인터프리터 언어 (Interpreted Language)

**한줄설명:** 소스코드를 한 줄씩 읽으면서 실행하는 언어

**상세설명:**
- 과정:
  ```
  소스코드 → 인터프리터 → 한 줄씩 해석 및 실행
  ```

- 특징:
  - 컴파일 단계 없음
  - 한 줄씩 실행 및 해석
  - 오류 발생 시 그 줄에서 중단
  - 실행 속도 상대적 느림

- 예: Python, JavaScript, Ruby, Perl

- 장점:
  - 빠른 개발
  - 유연함
  - 쉬운 디버깅

- 단점:
  - 느린 실행 속도
  - 런타임 오류 발생 가능
  - 배포 시 소스코드 필요

### Java의 위치

- Java는 특수한 경우:
  - 소스코드 → **컴파일** → 바이트코드 (.class)
  - 바이트코드 → **JVM (Java Virtual Machine)** → 해석 및 실행
  - 하이브리드 방식
  - "Write Once, Run Anywhere" (WORA)

**리뷰:** 언어 특성 이해로 선택 기준 파악

---

## 객체 지향 언어

**한줄설명:** 프로그램을 객체들의 상호작용으로 보는 프로그래밍 언어

**상세설명:**
- 대표: Java, Python, C++, C#, Ruby

- 핵심 개념:
  1. **캡슐화 (Encapsulation)**:
     - 데이터와 기능을 하나의 캡슐로 묶음
     - 외부에서의 접근 제한
     - 데이터 무결성 보장
     - 유지보수성 향상

  2. **상속 (Inheritance)**:
     - 기존 클래스의 특징을 이어받아 새로운 클래스 정의
     - 코드 재사용성 높음
     - 객체 간 계층 관계 구성
     - 예: Animal → Dog, Cat

  3. **다형성 (Polymorphism)**:
     - 같은 메서드를 사용해도 객체 타입에 따라 다르게 동작
     - 유연하고 확장 가능한 코드
     - 예: draw() 메서드가 Circle과 Square에서 다르게 동작

  4. **추상화 (Abstraction)**:
     - 복잡한 세부 내용을 숨기고 핵심 특징만 표현
     - 프로그램 구조를 간결하게
     - 인터페이스로 계약 정의

**리뷰:** 현대 프로그래밍의 표준 패러다임

---

## 오버로딩 vs 오버라이딩

### 오버로딩 (Overloading)

**한줄설명:** 같은 이름의 메서드를 매개변수 타입이나 개수만 다르게 하여 여러 개 정의

**상세설명:**
- 특징:
  - 같은 클래스 내에서만 가능
  - 반환 타입만 다른 것은 오버로딩 아님
  - 메서드 해상도는 컴파일 시간에 결정 (정적 바인딩)

- 예:
  ```java
  class Calculator {
      // 오버로딩 1: 정수 더하기
      public int add(int a, int b) {
          return a + b;
      }

      // 오버로딩 2: 실수 더하기
      public double add(double a, double b) {
          return a + b;
      }

      // 오버로딩 3: 세 개 매개변수
      public int add(int a, int b, int c) {
          return a + b + c;
      }
  }

  Calculator calc = new Calculator();
  calc.add(1, 2);              // int 버전 호출
  calc.add(1.5, 2.5);          // double 버전 호출
  calc.add(1, 2, 3);           // 3개 매개변수 버전 호출
  ```

### 오버라이딩 (Overriding)

**한줄설명:** 상속받은 메서드를 자식 클래스에서 재정의하여 사용

**상세설명:**
- 특징:
  - 부모-자식 클래스 관계에서만 가능
  - 메서드 시그니처 완전히 동일
  - 메서드 해상도는 런타임에 결정 (동적 바인딩)
  - 접근 제어자는 더 공개적이거나 같아야 함

- 예:
  ```java
  class Animal {
      public void makeSound() {
          System.out.println("Some sound");
      }
  }

  class Dog extends Animal {
      @Override
      public void makeSound() {
          System.out.println("Woof!");
      }
  }

  class Cat extends Animal {
      @Override
      public void makeSound() {
          System.out.println("Meow!");
      }
  }

  Animal dog = new Dog();
  Animal cat = new Cat();
  dog.makeSound();  // "Woof!" 출력
  cat.makeSound();  // "Meow!" 출력
  ```

**리뷰:** 객체 지향의 핵심 개념. 구분이 매우 중요

---

## 스택 (Stack)

**한줄설명:** LIFO(Last In First Out, 후입선출) 방식으로 동작하는 자료구조

**상세설명:**
- 특징:
  - 마지막에 들어온 데이터가 먼저 나감
  - 위에만 접근 가능
  - Push: 데이터 삽입
  - Pop: 데이터 제거 및 반환
  - Peek: 최상단 데이터 확인 (제거 안 함)

- 시각화:
  ```
  Push 1 → [1]
  Push 2 → [1, 2]
  Push 3 → [1, 2, 3]
  Pop    → [1, 2]  (3 반환)
  Pop    → [1]     (2 반환)
  Pop    → []      (1 반환)
  ```

- 사용:
  - 함수 호출 스택 (Call Stack)
  - 괄호 매칭 검증
  - 뒤로가기 기능
  - 재귀 알고리즘

**리뷰:** 기본 자료구조. 깊이 이해 필수

---

## 큐 (Queue)

**한줄설명:** FIFO(First In First Out, 선입선출) 방식으로 동작하는 자료구조

**상세설명:**
- 특징:
  - 먼저 들어온 데이터가 먼저 나감
  - 앞에서 제거, 뒤에서 삽입
  - Enqueue: 데이터 삽입
  - Dequeue: 데이터 제거 및 반환
  - Peek: 앞의 데이터 확인

- 시각화:
  ```
  Enqueue 1 → [1]
  Enqueue 2 → [1, 2]
  Enqueue 3 → [1, 2, 3]
  Dequeue   → [2, 3]     (1 반환)
  Dequeue   → [3]        (2 반환)
  ```

- 사용:
  - 작업 스케줄링
  - 프린터 인쇄 작업 대기열
  - 너비 우선 탐색 (BFS)
  - 이벤트 처리

**리뷰:** 스택과 대비되는 중요한 자료구조

---

## 자료구조 (Data Structure)

**한줄설명:** 데이터를 효율적으로 저장하고 처리하기 위한 구조

**상세설명:**
- 기본 자료구조:
  1. **배열 (Array)**: 고정 크기, 연속 메모리
  2. **리스트 (List)**: 가변 크기, 노드 연결
  3. **스택 (Stack)**: LIFO
  4. **큐 (Queue)**: FIFO
  5. **트리 (Tree)**: 계층적 구조
  6. **그래프 (Graph)**: 노드와 간선의 집합
  7. **해시 테이블 (Hash Table)**: 키-값 매핑

- 선택 기준:
  - 접근 패턴 (빈번한 조회? 삽입/삭제?)
  - 메모리 효율
  - 시간 복잡도
  - 공간 복잡도

**리뷰:** 효율적인 알고리즘 작성의 기초

---

## 객체 (Object)

**한줄설명:** 데이터(속성)와 메서드(행위)를 하나로 묶은 단위

**상세설명:**
- 현실 세계 모델링:
  - 현실의 사물을 객체로 표현
  - 예: 자동차 객체
    - 속성: 색상, 속도, 연료
    - 메서드: 가속(), 정지(), 방향전환()

- 클래스와의 관계:
  - 클래스: 설계도 (틀)
  - 객체: 설계도로 만든 실제 물건 (인스턴스)

- 예:
  ```python
  class Car:
      def __init__(self, color, speed):
          self.color = color     # 속성
          self.speed = speed

      def accelerate(self):      # 메서드
          self.speed += 10

  car1 = Car("red", 0)          # 객체 생성
  car2 = Car("blue", 0)         # 또 다른 객체
  ```

**리뷰:** 객체 지향 프로그래밍의 기본 단위

---

## 클래스 (Class)

**한줄설명:** 객체를 생성하기 위한 설계도 또는 틀

**상세설명:**
- 구성:
  1. **속성 (Property/Attribute)**: 데이터
  2. **메서드 (Method)**: 기능/동작
  3. **생성자 (Constructor)**: 초기화
  4. **소멸자 (Destructor)**: 정리 (일부 언어)

- 예:
  ```java
  class Person {
      // 속성
      String name;
      int age;

      // 생성자
      Person(String name, int age) {
          this.name = name;
          this.age = age;
      }

      // 메서드
      void introduce() {
          System.out.println("Hello, I'm " + name);
      }
  }

  // 사용
  Person person = new Person("John", 30);
  person.introduce();  // "Hello, I'm John" 출력
  ```

**리뷰:** 객체 지향 설계의 가장 기본적인 단위

---

## 인스턴스 (Instance)

**한줄설명:** 클래스를 바탕으로 생성된 실제 객체

**상세설명:**
- 관계:
  ```
  클래스 (설계도)
     ↓
  인스턴스 (실제 물건 1)
  인스턴스 (실제 물건 2)
  인스턴스 (실제 물건 3)
  ```

- 예:
  ```python
  class Dog:
      def __init__(self, name):
          self.name = name

  dog1 = Dog("Buddy")     # 인스턴스 1
  dog2 = Dog("Max")       # 인스턴스 2
  dog3 = Dog("Charlie")   # 인스턴스 3

  # 같은 클래스에서 생성되었지만 서로 다른 인스턴스
  ```

**리뷰:** 클래스와 인스턴스의 구분은 매우 중요

---

## 모듈 (Module)

**한줄설명:** 하나의 파일로 구성된 코드 단위 또는 함수와 클래스를 묶어놓은 파일

**상세설명:**
- Python에서의 모듈:
  - 하나의 .py 파일 = 하나의 모듈
  - 관련된 함수와 클래스를 한 파일에 묶음
  - 다른 파일에서 import하여 재사용

- 예:
  ```python
  # math_utils.py (모듈)
  def add(a, b):
      return a + b

  def subtract(a, b):
      return a - b

  # main.py
  from math_utils import add, subtract
  result = add(5, 3)  # 사용
  ```

- 계층:
  - **모듈**: 하나의 파일
  - **패키지**: 모듈의 묶음 (폴더)
  - **라이브러리**: 패키지의 모음
  - **프레임워크**: 규칙과 함께 제공되는 라이브러리

**리뷰:** 코드 재사용성과 구조화의 기본

---

## 라이브러리 (Library)

**한줄설명:** 특정 기능을 수행하는 코드의 모음으로 개발자가 쉽게 기능을 구현할 수 있도록 도와주는 도구

**상세설명:**
- 특징:
  - 다양한 함수의 집합
  - 외부 패키지로 설치
  - pip install로 설치 (Python)

- 선택 기준:
  - 다운로드 수 (인기도)
  - 꾸준한 유지보수 (최신 버전 업데이트)
  - 문서의 풍부함
  - 커뮤니티 크기

- 예시:
  ```bash
  pip install requests       # HTTP 요청 라이브러리
  pip install beautifulsoup4 # HTML 파싱 라이브러리
  pip install pandas         # 데이터 처리 라이브러리
  pip install numpy          # 수치 계산 라이브러리
  ```

- 저장 위치:
  - Python: 전역 (sys.path) 또는 가상환경
  - Node.js: 현재 디렉토리 (node_modules/)
  - Java: 시스템 디렉토리

**리뷰:** 바퀴를 다시 발명하지 말 것. 좋은 라이브러리 선택이 생산성 향상

---

## 프레임워크 (Framework)

**한줄설명:** 애플리케이션 개발을 위한 특정 기능을 구현하고 규칙을 세워놓은 틀

**상세설명:**
- 라이브러리와의 차이:
  - **라이브러리**: 필요한 기능만 선택적 사용
  - **프레임워크**: 정해진 구조와 규칙을 따라야 함

- 예:
  - Django: Python 웹 프레임워크
  - Spring: Java 엔터프라이즈 프레임워크
  - React: JavaScript UI 프레임워크
  - Flask: Python 마이크로 프레임워크

- 제공하는 것:
  - 프로젝트 구조 (디렉토리 구성)
  - 핵심 기능 (라우팅, 데이터베이스 접근, 인증 등)
  - 개발 규칙 (MVC, MVT 등)
  - 도구 (서버, 테스트 도구 등)

**리뷰:** 프레임워크 선택이 프로젝트 성공을 좌우함

---

## 시스템 콜 (System Call)

**한줄설명:** 프로그램이 OS의 기능(파일 열기, 네트워크 통신 등)을 사용하기 위해 커널에 요청하는 메커니즘

**상세설명:**
- 특징:
  - 유저 모드 → 커널 모드 전환
  - 권한 있는 작업 수행
  - 오버헤드 발생 (컨텍스트 스위칭)
  - 번호로 식별 (예: read = 0, write = 1)

- 예:
  ```python
  import os

  # 파일 열기 (시스템 콜)
  f = open('file.txt', 'r')

  # 파일 읽기 (시스템 콜)
  content = f.read()

  # 네트워크 통신 (시스템 콜)
  import socket
  s = socket.socket()
  ```

- 주요 시스템 콜:
  - read / write: 파일 I/O
  - open / close: 파일 열고 닫기
  - fork: 프로세스 생성
  - exec: 프로그램 실행
  - socket: 네트워크 통신

**리뷰:** 운영체제 이해의 기초

---

## UUID (Universally Unique Identifier)

**한줄설명:** 전세계적으로 유일한 식별자를 생성하기 위한 형식

**상세설명:**
- 형식: `xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`
- 예: `550e8400-e29b-41d4-a716-446655440000`

- 특징:
  - 128비트 (16바이트)
  - 16진수로 표현 (32자리)
  - 충돌 확률 극히 낮음
  - 분산 시스템에서 고유성 보장

- 버전:
  - UUID v1: 타임스탬프 + MAC 주소
  - UUID v4: 완전 랜덤 (가장 널리 사용)
  - UUID v5: 이름 기반

- 사용:
  ```python
  import uuid
  unique_id = uuid.uuid4()  # UUID v4 생성
  print(unique_id)  # 예: 550e8400-e29b-41d4-a716-446655440000
  ```

- 용도:
  - 데이터베이스 기본키
  - API 요청 추적
  - 세션 ID
  - 파일 이름

**리뷰:** 분산 시스템에서 필수적인 개념

---

## 콜 스택 (Call Stack)

**한줄설명:** 함수 호출이 일어날 때 각 호출 정보를 저장하는 스택

**상세설명:**
- 동작:
  ```python
  def a():
      b()  # a에서 b 호출

  def b():
      c()  # b에서 c 호출

  def c():
      pass  # c 실행

  a()
  ```

  호출 스택 변화:
  ```
  a() 호출    → [a]
  b() 호출    → [a, b]
  c() 호출    → [a, b, c]
  c() 반환    → [a, b]
  b() 반환    → [a]
  a() 반환    → []
  ```

- 특징:
  - 메모리 한계 있음 (스택 오버플로우)
  - 재귀 호출 깊이 제한
  - LIFO 방식 동작

**리뷰:** 함수 실행 메커니즘 이해에 필수

---

## 스택 트레이스 (Stack Trace)

**한줄설명:** 오류 발생 시 함수 호출 순서를 보여주는 기록 - 디버깅에 매우 유용

**상세설명:**
- 목적:
  - 오류 발생 지점 파악
  - 함수 호출 체인 이해
  - 빠른 디버깅

- 예:
  ```
  Traceback (most recent call last):
    File "main.py", line 10, in <module>
      a()
    File "main.py", line 3, in a
      b()
    File "main.py", line 6, in b
      c()
    File "main.py", line 9, in c
      return 1/0  # ZeroDivisionError 발생
  ZeroDivisionError: division by zero
  ```

  읽는 방법:
  - 아래에서 위로 읽음 (오류 지점 → 호출 지점)
  - c() → b() → a() → main.py 순서로 호출됨
  - c의 9번 줄에서 오류 발생

- 다른 이름:
  - Traceback (Python)
  - Stack trace (일반)
  - Back trace (디버거)

**리뷰:** 오류 해결의 가장 첫 번째 단서
