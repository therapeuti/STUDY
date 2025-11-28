# Frontend (프론트엔드)

## HTML (HyperText Markup Language)

**한줄설명:** 웹 페이지를 생성하는 데 사용되는 표준 마크업 언어

**상세설명:**
- HTML은 웹 브라우저에게 문서의 구조와 내용을 전달하여 웹 페이지를 표시
- 웹 브라우저에서 표현할 수 있는 언어: HTML / CSS / JavaScript
- 태그를 사용한 구조화된 마크업
- 문서의 의미 있는 구조를 나타냄

**리뷰:** 웹 개발의 기초. 시맨틱 태그 사용으로 접근성과 SEO 향상

---

## CSS (Cascading Style Sheet)

**한줄설명:** 웹 페이지의 디자인과 레이아웃을 제어하기 위해 개발된 스타일 시트 언어

**상세설명:**
- HTML의 요소들에 시각적 스타일을 적용
- 색상, 폰트, 레이아웃, 애니메이션 등 제어
- 캐스케이딩: 여러 규칙이 적용될 때 우선순위에 따라 결정
- 반응형 웹 디자인 지원 (미디어 쿼리)

**리뷰:** 웹 디자인의 핵심. Flexbox, Grid 등 현대적 레이아웃 기법 숙지 필수

---

## 마크업 언어 (Markup Language)

**한줄설명:** 문서나 데이터의 구조를 설명해주는 언어

**상세설명:**
- 예시: HTML, XML, Markdown
- 데이터 자체보다는 데이터의 구조와 의미에 집중
- 프로그래밍 언어가 아닌 표시 언어

**리뷰:** 다양한 마크업 언어를 이해하면 웹 기술 학습에 도움

---

## 시맨틱 태그 (Semantic Tag)

**한줄설명:** 웹 문서의 구조와 의미를 더 명확하게 전달하기 위해 사용되는 HTML 태그

**상세설명:**
- 의미 있는 태그: `<header>`, `<nav>`, `<main>`, `<article>`, `<section>`, `<footer>` 등
- 기존의 무의미한 `<div>`를 대체
- 이점:
  - 웹 페이지의 가독성 향상
  - 접근성(Accessibility) 향상
  - 검색 엔진 최적화(SEO) 개선
  - 유지보수성 증가

**리뷰:** 현대 웹 개발의 필수 요소. 반드시 의미에 맞는 태그를 사용할 것

---

## 픽셀 (Pixel)

**한줄설명:** 이미지를 구성하는 최소 단위

**상세설명:**
- Picture Element의 약자
- 디지털 이미지의 가장 작은 화소 단위
- 해상도: 픽셀의 수로 표현 (예: 1920x1080)
- 화면의 각 픽셀은 RGB 색상값으로 표현

**리뷰:** 이미지 작업과 반응형 웹 디자인을 이해하는 데 기본적인 개념

---

## 해상도 (Resolution)

**한줄설명:** 이미지를 세밀하게 표현할 수 있는 정도, 픽셀의 수

**상세설명:**
- 높은 해상도: 더 많은 픽셀 = 더 선명한 이미지
- 표시 방식: 가로 x 세로 (예: 1920 x 1080)
- DPI (Dots Per Inch): 인쇄 해상도의 단위
- 웹: 72 DPI, 인쇄: 300 DPI 이상 권장

**리뷰:** 이미지 최적화와 반응형 디자인에서 중요한 개념

---

## 미니파이 (Minify)

**한줄설명:** HTML, CSS, JavaScript와 같은 코드 파일의 불필요한 문자, 공백, 주석을 제거하여 파일 크기를 줄이는 방법

**상세설명:**
- 파일 크기 감소로 로딩 속도 향상
- 보안 향상 (코드 난독화 효과)
- 빌드 도구가 자동으로 처리 (Webpack, Gulp 등)
- 예:
  ```javascript
  // Before minify
  function helloWorld() {
    console.log("Hello World");
  }

  // After minify
  function helloWorld(){console.log("Hello World")}
  ```

**리뷰:** 프로덕션 배포 시 필수 과정

---

## 하이퍼텍스트 (Hypertext)

**한줄설명:** 문서 안의 특정 단어나 구절에 다른 문서나 정보로 연결되는 링크를 포함한 텍스트

**상세설명:**
- 단순 텍스트와 달리 비선형 읽기 가능
- 웹의 기본 개념
- HTML의 "HT"가 Hypertext를 의미

**리뷰:** 웹이 혁신적인 이유는 하이퍼텍스트의 개념 때문

---

## 하이퍼링크 (Hyperlink)

**한줄설명:** 다른 페이지와 연결되는 것

**상세설명:**
- HTML에서 `<a>` 태그로 구현
- 내부 링크, 외부 링크, 이메일 링크, 파일 다운로드 등
- URL을 통해 리소스를 식별하고 연결

**리뷰:** 웹의 기본 네비게이션 요소

---

## 트루칼라 (True Color)

**한줄설명:** 24비트에 해당하는 색, 디지털 이미지나 디스플레이에서 한 픽셀을 표현하는 매우 많은 색상 수

**상세설명:**
- 24비트 = 8비트 R + 8비트 G + 8비트 B
- 각 채널이 0~255 범위의 값을 가짐
- 총 색상 수: 256 x 256 x 256 = 16,777,216가지
- RGB 색상 공간에서 인간의 눈이 인식할 수 있는 대부분의 색상 표현 가능

**리뷰:** 현대 디스플레이의 표준 색상 표현 방식

---

## Lorem Ipsum

**한줄설명:** 텍스트 집어넣을 공간에 임시로 집어넣어두는 더미 텍스트

**상세설명:**
- 디자인 목업 제작 시 사용
- 실제 의미 있는 텍스트 없이 레이아웃과 디자인에만 집중 가능
- 라틴어 더미 텍스트의 표준
- 온라인 도구: Lorem Ipsum Generator

**리뷰:** 웹 디자인 프로토타이핑에서 자주 사용되는 관례

---

## 선택자 (Selector)

**한줄설명:** HTML 요소에 디자인을 적용하기 위한 방법

**상세설명:**
- 종류:
  1. **태그 선택자**: `p { }` - 모든 `<p>` 요소
  2. **클래스 선택자**: `.classname { }` - class 속성이 특정 값인 요소
  3. **ID 선택자**: `#idname { }` - id 속성이 특정 값인 요소
  4. **속성 선택자**: `input[type="text"] { }`
  5. **가상 클래스**: `:hover`, `:active`, `:nth-child()`
  6. **복합 선택자**: 자식, 형제 등의 관계 지정
- 특이도(Specificity): ID > Class > Tag

**리뷰:** CSS의 기초. 효율적인 선택자 사용이 성능에 영향

---

## ECMA 스크립트 (ECMAScript)

**한줄설명:** JavaScript를 표준화한 국제 표준 스크립트 언어

**상세설명:**
- JavaScript는 ECMAScript의 구현체
- 버전: ES5(2009), ES6/ES2015, ES2016, ... , ES2024
- 모든 브라우저는 ECMAScript 표준에 맞게 개발
- 버전별 주요 기능:
  - ES6: 클래스, 화살표 함수, Promise, 템플릿 리터럴, 구조 분해 등
  - 최신 버전: 더 나은 성능과 기능 제공

**리뷰:** JavaScript 학습 시 ES6 이상을 기준으로 학습할 것

---

## var, let, const

**한줄설명:** JavaScript의 변수 선언 키워드

### var
**특징:**
- 함수 스코프 (function scope)
- 호이스팅 발생
- 재선언, 재할당 모두 가능
- 현재는 사용 권장하지 않음

### let
**특징:**
- 블록 스코프 (block scope)
- 주어진 범위 내에서만 유효
- 재할당은 가능하지만 재선언 불가
- 현대적 변수 선언 방식

### const
**특징:**
- 블록 스코프
- 선언과 동시에 초기화 필수
- 재할당 불가능 (상수)
- 객체의 내용은 수정 가능 (참조 주소만 고정)

**리뷰:** let, const를 사용하고 var는 피할 것. 기본은 const, 필요시만 let

---

## Scope (범위)

**한줄설명:** 변수, 객체, 함수 등에 접근할 수 있는 범위

**상세설명:**
- **전역 스코프 (Global Scope)**:
  - 코드 어느 곳에서나 접근 가능
  - 최상위 레벨에서 선언된 변수
  - 과도하게 사용하면 이름 충돌 위험

- **로컬 스코프 (Local Scope)**:
  - 특정 함수나 블록 내에서만 접근 가능
  - 함수 스코프: var로 선언한 변수
  - 블록 스코프: let, const로 선언한 변수

- **스코프 체인**:
  - 변수를 찾을 때 현재 스코프 → 상위 스코프 → ... → 전역 스코프 순서로 탐색

**리뷰:** 메모리 효율성과 예기치 않은 버그 방지를 위해 스코프 이해 필수

---

## JSON (JavaScript Object Notation)

**한줄설명:** JavaScript 객체를 표현하는 경량 데이터 교환 형식

**상세설명:**
- 인간이 읽기 쉬운 텍스트 형식
- 데이터 직렬화 표준
- 구조:
  ```json
  {
    "name": "John",
    "age": 30,
    "hobbies": ["reading", "coding"],
    "address": {
      "city": "Seoul",
      "country": "Korea"
    }
  }
  ```
- API 응답의 표준 형식
- XML의 대안으로 널리 사용

**리뷰:** 웹 개발에서 필수적인 데이터 형식

---

## 일치 연산자 (=== vs ==)

**한줄설명:** JavaScript에서 값과 타입을 비교하는 연산자

**상세설명:**
- **==** (동등 연산자):
  - 값만 비교
  - 타입 강제 변환 발생
  - 예: `"5" == 5` → true
  - 예측 불가능한 동작 가능

- **===** (일치 연산자):
  - 값과 타입 모두 비교
  - 타입 강제 변환 없음
  - 예: `"5" === 5` → false
  - 명확하고 안전한 비교

**리뷰:** JavaScript에서는 항상 ===를 사용할 것. 버그 방지의 기본

---

## DOM (Document Object Model)

**한줄설명:** 웹페이지의 구조를 트리 구조의 객체 모델로 표현해서 프로그래밍 언어가 접근하고 조작할 수 있도록 하는 인터페이스

**상세설명:**
- HTML을 읽어서(파싱) 프로그래밍하기 편한 자료구조 형태로 저장
- 트리 구조:
  ```
  document
  └── html
      ├── head
      └── body
          ├── div
          └── p
  ```
- JavaScript에서 DOM에 접근:
  ```javascript
  document.getElementById('id')
  document.querySelector('.class')
  document.querySelectorAll('div')
  ```
- DOM 조작:
  - 요소 선택
  - 속성 변경
  - 이벤트 처리
  - 컨텐츠 수정
- `<script>` 태그 안에서 DOM 정보를 가져오고, 변경하며 동적 컨텐츠 생성 가능

**리뷰:** JavaScript 기본. 실제 프로젝트에서 가장 많이 사용되는 개념

---

## 파싱 (Parsing)

**한줄설명:** 문서(HTML, JSON 등)를 읽고 해석하여 구조화된 데이터로 변환하는 과정

**상세설명:**
- 브라우저가 HTML을 파싱하여 DOM 생성
- JSON 파싱: `JSON.parse()`
- 컴파일러와 인터프리터도 파싱 수행
- 문법 오류 검사 포함

**리뷰:** 웹 렌더링 과정의 초기 단계

---

## jQuery

**한줄설명:** DOM 조작과 이벤트 처리를 더 쉽게 해주는 JavaScript 라이브러리

**상세설명:**
- 크로스 브라우저 호환성 제공
- 간결한 문법으로 DOM 조작 간편화
- 과거에는 매우 인기 있었으나 현재는 React, Vue 등 프레임워크 선호
- 레거시 프로젝트에서 여전히 사용됨

**리뷰:** 역사적 중요성은 크지만 현대 개발에서는 프레임워크 사용이 표준

---

## TypeScript

**한줄설명:** JavaScript에 정적 타입을 추가한 프로그래밍 언어

**상세설명:**
- JavaScript의 슈퍼셋
- JavaScript의 자유로움으로 인한 단점 해결:
  - 타입 안정성: 예기치 않은 타입 에러 방지
  - 자동 완성과 IDE 지원 개선
  - 코드 가독성 증가
- 컴파일: TypeScript → JavaScript로 변환 후 실행
- 프로덕션 프로젝트에서 점점 더 많이 사용되는 추세

**리뷰:** 엔터프라이즈급 JavaScript 개발의 사실상 표준

---

## 익명 함수 (Anonymous Function)

**한줄설명:** 이름이 없는 함수

**상세설명:**
- 콜백 함수로 많이 사용
- 화살표 함수 (Arrow Function)로도 표현 가능
- 예:
  ```javascript
  // 기존 방식
  const result = function(x, y) {
    return x + y;
  };

  // 화살표 함수
  const result = (x, y) => x + y;
  ```
- IIFE (Immediately Invoked Function Expression)에도 사용

**리뷰:** 함수형 프로그래밍의 기초

---

## 코딩 스탠다드 (Coding Standard)

**한줄설명:** 코드 스타일, 포매팅, 주석 등에 대한 규칙

**상세설명:**
- 일관된 코드 스타일
- 가독성 향상
- 팀 프로젝트의 필수 요소
- 자동화 도구: ESLint, Prettier 등으로 강제
- 대표적 스탠다드:
  - Airbnb JavaScript Style Guide
  - Google JavaScript Style Guide

**리뷰:** 면접에서 "회사의 코딩 스탠다드는 무엇인가?"라는 질문이 나올 수 있음

---

## 네이밍 컨벤션 (Naming Convention)

**한줄설명:** 변수, 함수, 클래스 등의 이름을 짓는 규칙

**상세설명:**
- JavaScript 관례:
  - 변수, 함수: camelCase (예: userName, getUserInfo)
  - 클래스, 컴포넌트: PascalCase (예: User, UserInfo)
  - 상수: UPPER_SNAKE_CASE (예: MAX_SIZE)
  - 의미 있는 이름 사용 (약자나 무의미한 이름 피하기)

- 이점:
  - 코드 가독성 향상
  - 오해 감소
  - 협업 효율성 증대

**리뷰:** 프로젝션 전에 팀의 네이밍 컨벤션을 파악할 것

---

## JavaScript

**한줄설명:** 웹 브라우저에서 동적 웹 페이지를 만들기 위한 프로그래밍 언어

**상세설명:**
- 역사:
  - 1995년 Netscape에서 개발
  - 원래 이름: LiveScript
  - Java가 당시 글로벌 인기 언어여서 JavaScript로 이름 변경
- 특징:
  - 동적 타입 언어
  - 프로토타입 기반 객체 지향
  - 함수형 프로그래밍 지원
  - 단일 스레드 기반 비동기 처리
- 실행 환경:
  - 브라우저 (Client-side)
  - Node.js (Server-side)

**리뷰:** 웹 개발의 필수 언어. 지속적인 진화와 개선

---

## 정적 컨텐츠 (Static Content)

**한줄설명:** 항상 같은 내용을 보여주는 웹 페이지

**상세설명:**
- 예: HTML, CSS, 이미지 파일
- 서버에서 별도의 처리 없이 그대로 전송
- 빠른 로딩 속도
- 상호작용 불가능

**리뷰:** 동적 컨텐츠와의 구분 필요

---

## 동적 컨텐츠 (Dynamic Content)

**한줄설명:** 볼 때마다, 사용자마다 달라지는 페이지

**상세설명:**
- 사용자 입력, 현재 시간, 데이터베이스 데이터 등에 따라 변동
- 서버에서 처리 후 결과를 전송하거나 클라이언트에서 JavaScript로 생성
- 상호작용 가능
- 현대 웹의 표준

**리뷰:** SPA(Single Page Application), PWA 등의 기반

---

## 모달 (Modal)

**한줄설명:** 팝업창처럼 떠가지고 사용자가 뭔가를 해야하는 윈도우

**상세설명:**
- 새 창이 아닌 오버레이 방식
- 사용자가 처리할 때까지 배경은 비활성화
- 예: 확인 다이얼로그, 로그인 폼
- 특징:
  - 사용자 집중도 향상
  - 하지만 과용하면 UX 악화 가능

**리뷰:** 사용자 경험을 고려하여 적절히 사용할 것

---

## 이벤트 전파 (Event Propagation)

**한줄설명:** 이벤트가 DOM 트리를 따라 전파되는 방식

**상세설명:**
- **이벤트 캡처링**: 최상위에서 대상까지 내려오는 단계
- **이벤트 버블링**: 대상에서 최상위까지 올라가는 단계
- **이벤트 타겟**: 실제 이벤트가 발생한 요소

**리뷰:** 이벤트 처리 시 중요한 개념

---

## 이벤트 버블링 (Event Bubbling)

**한줄설명:** 하위요소의 이벤트 발생 시 상위요소의 이벤트도 발생하는 이벤트 전파

**상세설명:**
- 예:
  ```html
  <div id="parent">
    <button id="child">Click me</button>
  </div>
  ```
  버튼 클릭 → 버튼의 click 이벤트 발생 → 부모의 click 이벤트도 발생

- 방지 방법:
  ```javascript
  event.stopPropagation()
  ```

**리뷰:** 복잡한 이벤트 처리 시 반드시 고려해야 할 개념

---

## React (리액트)

**한줄설명:** Facebook에서 개발한 JavaScript 라이브러리로 UI를 컴포넌트 기반으로 구성

**상세설명:**
- 특징:
  - **컴포넌트화**: 재사용 가능한 UI 단위로 분해
  - **Virtual DOM**: 효율적인 렌더링
  - **단방향 데이터 바인딩**: 데이터 흐름이 명확
  - **JSX**: HTML과 JavaScript를 혼합한 문법
- 장점:
  - 여러 사람이 각 기능을 나누어서 개발 가능
  - 컴포넌트 재사용성 높음
  - 큰 프로젝트에 적합

- 단점:
  - 학습 곡선이 있음
  - 간단한 프로젝트에서는 오버엔지니어링일 수 있음

**리뷰:** 현대 웹 개발의 표준. 숙련도가 중요

---

## Promise

**한줄설명:** 비동기 작업의 결과를 나타내는 객체

**상세설명:**
- 상태:
  1. **Pending**: 대기 상태, 작업이 아직 완료되지 않음
  2. **Fulfilled**: 성공 상태, 작업 완료 및 결과 반환
  3. **Rejected**: 실패 상태, 오류 발생
- 메서드:
  - `.then()`: 성공 콜백
  - `.catch()`: 실패 콜백
  - `.finally()`: 성공/실패 상관없이 실행
- 체이닝 가능: Promise Hell 해결

**리뷰:** 비동기 처리의 기초. async/await로도 표현 가능

---

## 콜백 헬 (Callback Hell)

**한줄설명:** 콜백 함수의 중첩으로 인해 코드가 깊어지고 읽기 어려워지는 상황

**상세설명:**
- 예:
  ```javascript
  // Callback Hell
  getData(function(a) {
    getMoreData(a, function(b) {
      getMoreData(b, function(c) {
        getMoreData(c, function(d) {
          // ...
        });
      });
    });
  });

  // Promise로 해결
  getData()
    .then(a => getMoreData(a))
    .then(b => getMoreData(b))
    .then(c => getMoreData(c))

  // async/await로 해결
  const a = await getData();
  const b = await getMoreData(a);
  const c = await getMoreData(b);
  ```

**리뷰:** Promise와 async/await를 사용하여 해결할 것

---

## AJAX (Asynchronous JavaScript and XML)

**한줄설명:** 페이지 새로고침 없이 비동기적으로 서버와 통신하는 기술

**상세설명:**
- XMLHttpRequest를 기반으로 구현
- 현재: 주로 JSON 사용 (XML은 거의 사용 안 함)
- 사용:
  ```javascript
  fetch('/api/data')
    .then(response => response.json())
    .then(data => console.log(data))
  ```
- 장점:
  - 페이지 새로고침 없음
  - 부분 업데이트 가능
  - 사용자 경험 향상

**리뷰:** 현대 웹 애플리케이션의 표준 통신 방식

---

## XMLHttpRequest (XHR)

**한줄설명:** 브라우저에서 서버와 비동기 통신을 하기 위한 API

**상세설명:**
- AJAX의 기반 기술
- 문법:
  ```javascript
  const xhr = new XMLHttpRequest();
  xhr.open('GET', '/api/data');
  xhr.onload = function() {
    console.log(xhr.responseText);
  };
  xhr.send();
  ```
- 현재: Fetch API나 라이브러리(axios 등)로 대체되는 추세

**리뷰:** 과거 기술이지만 기본 개념 이해 필요

---

## SOP (Same Origin Policy)

**한줄설명:** 보안을 위해 다른 출처의 리소스 접근을 제한하는 정책

**상세설명:**
- 같은 출처(Origin): 프로토콜, 도메인, 포트가 모두 같아야 함
- 예:
  - `http://example.com`에서
  - `https://example.com` (프로토콜 다름) → 다른 출처
  - `http://example.com:3000` (포트 다름) → 다른 출처
  - `http://sub.example.com` (도메인 다름) → 다른 출처
- 목적: XSS, CSRF 공격 방지

**리뷰:** 웹 보안의 기초

---

## CORS (Cross-Origin Resource Sharing)

**한줄설명:** 다른 출처의 리소스를 안전하게 공유하는 메커니즘

**상세설명:**
- SOP의 제약을 안전하게 우회
- 서버에서 CORS 헤더 설정:
  ```
  Access-Control-Allow-Origin: *
  Access-Control-Allow-Methods: GET, POST
  ```
- 브라우저가 자동으로 검증
- Preflight Request (OPTIONS 요청) 발생
- 필수 개념: 백엔드에서 CORS 설정이 필수

**리뷰:** API 개발 시 매우 중요. 자주 마주치는 문제

---

## Preflight Request

**한줄설명:** 브라우저가 CORS 요청 전에 자동으로 보내는 OPTIONS 요청

**상세설명:**
- 목적: 실제 요청이 허용되는지 서버에 미리 확인
- 발생 조건:
  - POST, PUT, DELETE 등의 메서드
  - Custom 헤더 사용
  - Content-Type이 특정 값
- 서버 응답:
  - `Access-Control-Allow-Methods`
  - `Access-Control-Allow-Headers`
  - `Access-Control-Max-Age` (캐시 시간)

**리뷰:** CORS 문제 해결 시 preflight 요청 확인이 중요
