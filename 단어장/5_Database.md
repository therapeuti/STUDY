# Database (데이터베이스)

## 데이터베이스 (Database)

**한줄설명:** 관련있는 정보들의 체계적인 집합

**상세설명:**
- 정보를 효율적으로 저장, 관리, 검색할 수 있도록 구조화된 데이터 모음
- 특징:
  - **구조화**: 정해진 형식(스키마)에 따라 저장
  - **지속성**: 프로그램 종료 후에도 데이터 유지
  - **접근성**: 빠르고 쉬운 데이터 검색
  - **공유성**: 여러 사용자/애플리케이션이 동시 접근 가능

**리뷰:** 현대 애플리케이션의 필수 요소

---

## DBMS (Database Management System)

**한줄설명:** 데이터베이스를 생성, 관리, 접근할 수 있게 해주는 소프트웨어

**상세설명:**
- 기능:
  - 데이터 정의 (DDL)
  - 데이터 조작 (DML)
  - 데이터 제어 (DCL)
  - 트랜잭션 관리
  - 백업 및 복구

- 종류:
  - **관계형 DBMS (RDBMS)**: MySQL, PostgreSQL, Oracle, SQL Server
  - **비관계형 DBMS (NoSQL)**: MongoDB, Redis, Cassandra
  - **검색 엔진**: Elasticsearch, Solr

**리뷰:** 데이터베이스 선택은 프로젝트 특성에 따라 결정

---

## Race Condition (경합 상태)

**한줄설명:** 두 개 이상의 프로세스나 스레드가 동시에 같은 자원에 접근하려고 할 때 발생하는 오류 상황

**상세설명:**
- 예시:
  ```
  계좌 잔액: 1000원
  스레드 1: 500원 출금 (현재값 읽음 → 계산 → 저장)
  스레드 2: 300원 출금 (동시 실행)

  예상 결과: 200원
  실제 결과: 500원 또는 700원 (동시성 문제)
  ```

- 해결 방법:
  - **동기화 (Synchronization)**: 한 번에 하나의 스레드만 접근
  - **뮤텍스 (Mutex)**: 상호배제 락
  - **세마포어 (Semaphore)**: 신호 기반 접근 제어
  - **트랜잭션**: 데이터베이스 레벨의 동시성 제어

**리뷰:** 멀티스레드 프로그래밍에서 매우 중요한 개념

---

## 임계 영역 (Critical Section)

**한줄설명:** Race Condition에 대한 해결 방안으로, 동시에 접근하면 안 되는 코드 영역

**상세설명:**
- 특징:
  - 한 번에 하나의 스레드/프로세스만 실행 가능
  - 이전 스레드가 완료되어야 다음 스레드 실행

- 구현 방법:
  - 뮤텍스 락
  - 세마포어
  - 원자적(Atomic) 연산

**리뷰:** 동시성 제어의 기본 개념

---

## 세마포어 (Semaphore)

**한줄설명:** 신호를 기반으로 여러 자원에 대한 동시 접근을 제어하는 메커니즘

**상세설명:**
- 특징:
  - 정수값으로 자원의 개수 표현
  - wait() (P 연산): 세마포어 감소
  - signal() (V 연산): 세마포어 증가
  - 0 이하가 되면 대기

- 종류:
  - **이진 세마포어**: 0 또는 1 (뮤텍스와 유사)
  - **일반 세마포어**: 모든 정수값 가능

- 예시:
  ```
  세마포어 = 3 (3개의 자원)
  스레드 1: wait() → 세마포어 = 2
  스레드 2: wait() → 세마포어 = 1
  스레드 3: wait() → 세마포어 = 0
  스레드 4: wait() → 대기 (세마포어가 0)
  스레드 1: signal() → 세마포어 = 1
  스레드 4: wait() → 세마포어 = 0
  ```

**리뷰:** 운영체제 수준의 동시성 제어 메커니즘

---

## 뮤텍스 (Mutex - Mutual Exclusion)

**한줄설명:** 상호배제를 통해 한 번에 하나의 스레드만 임계 영역에 접근하도록 하는 락

**상세설명:**
- 특징:
  - 이진 값 (Lock/Unlock)
  - Lock을 획득한 스레드만 Unlock 가능
  - Unlock 후 다른 스레드가 Lock 획득 가능

- 구현:
  ```python
  mutex = threading.Lock()

  with mutex:  # Lock 획득
      # 임계 영역
      shared_resource = new_value
  # Lock 해제
  ```

**리뷰:** 가장 기본적인 동시성 제어 방식

---

## 트랜잭션 (Transaction)

**한줄설명:** 하나의 논리적 작업 단위로 모두 성공하거나 모두 실패해야 하는 작업 모음

**상세설명:**
- ACID 특성:
  1. **원자성 (Atomicity)**: All or Nothing
     - 트랜잭션의 모든 작업이 완료되거나 모두 롤백
     - 부분 완료 상태 불가능

  2. **일관성 (Consistency)**: 데이터베이스 무결성 유지
     - 트랜잭션 전후로 데이터베이스 상태가 일관성 있음
     - 정의된 규칙과 제약 조건 위반 불가능

  3. **독립성 (Isolation)**: 트랜잭션 간 독립성
     - 동시 실행되는 트랜잭션들이 서로 영향 미치지 않음
     - Isolation Level로 제어 (Read Uncommitted, Read Committed, Repeatable Read, Serializable)

  4. **영속성 (Durability)**: 커밋된 데이터는 영구 저장
     - 트랜잭션 완료 후 전원이 꺼져도 데이터 유지
     - 로그와 백업으로 보장

- 예시: 계좌 이체
  ```
  BEGIN TRANSACTION
    UPDATE accounts SET balance = balance - 500 WHERE id = 1
    UPDATE accounts SET balance = balance + 500 WHERE id = 2
  COMMIT

  → 둘 다 성공하거나 둘 다 실패
  ```

**리뷰:** 데이터 무결성의 가장 중요한 개념. 면접 필출

---

## RDB (Relational Database - 관계형 데이터베이스)

**한줄설명:** 행과 열로 이루어진 테이블 형태로 데이터를 저장하고, 테이블 간의 관계를 통해 데이터를 관리하는 데이터베이스

**상세설명:**
- 구성 요소:
  - **테이블 (Table)**: 데이터를 저장하는 기본 단위
  - **열 (Column)**: 속성 또는 필드 (예: id, name, email)
  - **행 (Row)**: 각 데이터 레코드
  - **키 (Key)**: 데이터 식별 및 테이블 연결

- 특징:
  - 구조화된 데이터
  - 강력한 일관성 (ACID)
  - 정규화를 통한 중복 제거
  - SQL을 통한 표준화된 접근

- 대표 DBMS: MySQL, PostgreSQL, Oracle, SQL Server, MariaDB

**리뷰:** 전통적이고 가장 널리 사용되는 데이터베이스 모델

---

## NoSQL (Not Only SQL - 비관계형 데이터베이스)

**한줄설명:** 관계형 데이터베이스의 단점을 보완하기 위해 개발된 비관계형 데이터베이스

**상세설명:**
- 등장 배경:
  - 대규모 데이터 처리 (빅데이터)
  - 비정형 데이터 처리
  - 높은 확장성 필요
  - 빠른 성능 필요

- 종류:
  1. **Document DB**: MongoDB, CouchDB
     - JSON/BSON 형식의 문서 저장
     - 유연한 스키마

  2. **Key-Value DB**: Redis, Memcached
     - 키와 값의 쌍으로 저장
     - 빠른 접근

  3. **Column Family DB**: HBase, Cassandra
     - 컬럼 기반 저장
     - 대규모 분산 처리

  4. **Graph DB**: Neo4j
     - 노드와 엣지로 관계 표현
     - 복잡한 관계 쿼리에 효율적

- 특징:
  - 유연한 스키마
  - 높은 확장성 (수평 확장)
  - BASE 특성 (Basically Available, Soft-state, Eventually consistent)

**리뷰:** 빅데이터 시대에 중요해진 기술

---

## 3V (빅데이터 특성)

**한줄설명:** 빅데이터의 핵심 특징 3가지

**상세설명:**
1. **Volume (크기)**:
   - 처리해야 할 데이터의 양이 매우 큼
   - 테라바이트 이상의 규모
   - 전통적 DBMS로는 처리 어려움

2. **Velocity (속도)**:
   - 데이터 생성과 처리 속도가 빠름
   - 실시간 데이터 처리 필요
   - 스트리밍 데이터 처리

3. **Variety (다양성)**:
   - 정형, 비정형 데이터 혼합
   - 다양한 포맷 (이미지, 텍스트, 센서 데이터 등)
   - 구조화되지 않은 데이터 많음

**리뷰:** 현대 데이터 분석과 AI 학습에서 매우 중요

---

## SQL (Structured Query Language)

**한줄설명:** 관계형 데이터베이스를 조작하고 관리하는 표준화된 언어

**상세설명:**
- 종류:
  1. **DDL (Data Definition Language)**: 데이터 구조 정의
     - CREATE: 테이블 생성
     - ALTER: 테이블 수정
     - DROP: 테이블 삭제

  2. **DML (Data Manipulation Language)**: 데이터 조작
     - SELECT: 조회
     - INSERT: 삽입
     - UPDATE: 수정
     - DELETE: 삭제

  3. **DCL (Data Control Language)**: 권한 제어
     - GRANT: 권한 부여
     - REVOKE: 권한 회수

- 예시:
  ```sql
  -- CREATE
  CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50),
    email VARCHAR(100)
  );

  -- INSERT
  INSERT INTO users (name, email) VALUES ('John', 'john@example.com');

  -- SELECT
  SELECT * FROM users WHERE name = 'John';

  -- UPDATE
  UPDATE users SET email = 'newemail@example.com' WHERE id = 1;

  -- DELETE
  DELETE FROM users WHERE id = 1;
  ```

**리뷰:** 데이터베이스 조작의 기본 언어

---

## Primary Key (기본키)

**한줄설명:** 테이블의 각 행을 고유하게 식별하는 열(또는 열들의 조합)

**상세설명:**
- 특징:
  - 유일성: 중복 불가
  - NOT NULL: 반드시 값 존재
  - 한 테이블에 하나만 존재 가능
  - 인덱스 자동 생성

- 종류:
  - **단일 기본키**: 하나의 열 (예: user_id)
  - **복합 기본키**: 여러 열의 조합 (예: (user_id, post_id))

- 예시:
  ```sql
  CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    email VARCHAR(100) UNIQUE
  );
  ```

**리뷰:** 데이터 무결성의 기본

---

## Foreign Key (외래키)

**한줄설명:** 다른 테이블의 기본키를 참조하여 테이블 간의 관계를 정의하는 열

**상세설명:**
- 특징:
  - 관계형 데이터베이스의 핵심 개념
  - 참조 무결성 보장
  - 기본키와 달리 중복 가능, NULL 가능
  - 자동 인덱스 생성 안 됨

- 예시:
  ```sql
  CREATE TABLE posts (
    id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(200),
    user_id INT,
    FOREIGN KEY (user_id) REFERENCES users(id)
  );
  ```
  - posts.user_id는 users.id를 참조
  - users에 없는 user_id 값 삽입 불가
  - users의 id 삭제 시 제약 확인

- 제약 옵션:
  - ON DELETE CASCADE: 부모 레코드 삭제 시 자식도 삭제
  - ON DELETE SET NULL: 부모 삭제 시 자식의 외래키를 NULL로 설정
  - ON DELETE RESTRICT: 자식이 있으면 부모 삭제 불가

**리뷰:** 데이터 관계 설정의 핵심

---

## Schema (스키마)

**한줄설명:** 데이터베이스의 구조를 정의하는 것

**상세설명:**
- 구성 요소:
  - 테이블과 각 열의 이름
  - 각 열의 데이터 타입 (INT, VARCHAR, DATE 등)
  - 제약 조건 (PRIMARY KEY, UNIQUE, NOT NULL 등)
  - 인덱스
  - 테이블 간의 관계 (Foreign Key)

- 예시:
  ```sql
  CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(50) NOT NULL UNIQUE,
    email VARCHAR(100) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
  );
  ```

**리뷰:** 데이터베이스 설계의 청사진

---

## Anomaly (이상 현상)

**한줄설명:** 정규화되지 않은 데이터베이스에서 발생하는 데이터 불일치 문제

**상세설명:**
- 종류:
  1. **삽입 이상 (Insertion Anomaly)**:
     - 새로운 데이터 삽입 시 불필요한 데이터도 함께 삽입해야 함
     - 예: 학생이 없는 강의를 저장할 수 없음

  2. **갱신 이상 (Update Anomaly)**:
     - 데이터 수정 시 같은 내용이 여러 행에 분산되어 일관성 문제
     - 예: 강의 이름 변경 시 모든 학생 레코드 수정 필요

  3. **삭제 이상 (Deletion Anomaly)**:
     - 데이터 삭제 시 의도하지 않은 정보도 함께 삭제
     - 예: 학생을 삭제하면 강의 정보도 사라짐

**리뷰:** 정규화의 필요성을 이해하는 데 중요

---

## 정규화 (Normalization)

**한줄설명:** 데이터 중복을 제거하고 데이터 무결성을 유지하도록 테이블을 설계하는 과정

**상세설명:**
- 목표:
  - 데이터 중복 제거
  - 이상 현상 제거
  - 데이터 무결성 향상
  - 저장 공간 절감

- 단계:
  1. **1정규형 (1NF)**:
     - 모든 속성값이 원자적(더 이상 분해 불가능)
     - 반복되는 그룹 제거

  2. **2정규형 (2NF)**:
     - 1NF 만족 + 부분 함수 종속성 제거
     - 기본키가 아닌 모든 속성이 기본키에 완전히 종속

  3. **3정규형 (3NF)**:
     - 2NF 만족 + 이행 함수 종속성 제거
     - 기본키가 아닌 속성들 간 종속성 제거

- 더 높은 정규형: BCNF, 4NF, 5NF

**리뷰:** 데이터베이스 설계의 기본. 과정을 이해하는 것이 중요

---

## 반정규화 (Denormalization)

**한줄설명:** 정규화된 데이터베이스에서 조회 성능을 향상시키기 위해 의도적으로 중복을 도입하는 과정

**상세설명:**
- 동기:
  - 정규화로 인한 조인 증가 → 성능 저하
  - 빈번한 조인이 필요한 경우 중복 데이터 저장

- 예시:
  ```sql
  -- 정규화: 조인 필요
  SELECT o.id, c.name
  FROM orders o
  JOIN customers c ON o.customer_id = c.id;

  -- 반정규화: customer_name 중복 저장
  ALTER TABLE orders ADD COLUMN customer_name VARCHAR(100);
  → 조인 없이 조회 가능하지만 데이터 중복
  ```

- 주의:
  - 데이터 일관성 문제 가능
  - 수정 시 모든 중복 데이터 업데이트 필요
  - 저장 공간 증가

**리뷰:** 성능과 일관성의 트레이드오프. 신중하게 적용할 것

---

## ERD (Entity Relationship Diagram)

**한줄설명:** 데이터베이스 설계 시 엔티티와 관계를 시각화하는 다이어그램

**상세설명:**
- 구성 요소:
  - **엔티티 (Entity)**: 테이블 (예: User, Product)
  - **속성 (Attribute)**: 열 (예: id, name, email)
  - **관계 (Relationship)**: 엔티티 간의 연결
  - **카디널리티**: 관계의 대응 관계

- 카디널리티 (Cardinality):
  - **1:1** (일대일): 한 사용자는 한 개의 프로필만 가짐
  - **1:N** (일대다): 한 사용자는 여러 개의 주문을 가짐
  - **N:M** (다대다): 한 학생은 여러 과목, 한 과목은 여러 학생

- 표기법:
  - Chen 표기법
  - Crow's Foot 표기법 (가장 널리 사용)
  - Barker 표기법

**리뷰:** 데이터베이스 설계 문서화의 표준. 시각화로 이해도 향상

---

## Index (인덱스)

**한줄설명:** 데이터베이스에서 데이터를 빠르게 검색하기 위해 생성하는 자료구조

**상세설명:**
- 특징:
  - 책의 목차처럼 빠른 검색 가능
  - 조회 속도 향상
  - 삽입/수정/삭제 속도는 느려짐 (인덱스 유지 필요)
  - 저장 공간 추가 필요

- 종류:
  - **Primary Key Index**: 자동 생성
  - **Unique Index**: 중복 값 방지
  - **Composite Index**: 여러 열 조합
  - **Full-text Index**: 텍스트 검색 최적화

- 예시:
  ```sql
  CREATE INDEX idx_email ON users(email);
  CREATE INDEX idx_user_post ON posts(user_id, created_at);
  ```

**리뷰:** 성능 최적화의 핵심. 신중하게 설계할 것

---

## 쿼리 최적화

**한줄설명:** 데이터베이스 쿼리의 실행 시간을 단축하기 위해 쿼리나 인덱스를 개선하는 과정

**상세설명:**
- 기법:
  1. 불필요한 열 제거: SELECT *  대신 필요한 열만
  2. 인덱스 생성: 자주 조회하는 열에 인덱스
  3. 조인 최적화: 조인 순서와 방식 개선
  4. 부분 쿼리 대신 조인 사용
  5. 집계 함수 최적화

- 분석 도구:
  - EXPLAIN / EXPLAIN PLAN: 쿼리 실행 계획 확인
  - 느린 쿼리 로그: 오래 걸린 쿼리 추적

**리뷰:** 대규모 데이터 처리 시 필수적인 기술

---

## 뷰 (View)

**한줄설명:** 하나 이상의 테이블에서 선택한 열과 행으로 이루어진 가상의 테이블

**상세설명:**
- 특징:
  - 실제 데이터를 저장하지 않음 (쿼리만 저장)
  - 조회 시마다 쿼리 실행
  - 복잡한 쿼리를 단순화
  - 보안 향상 (특정 데이터만 노출)

- 예시:
  ```sql
  CREATE VIEW active_users AS
  SELECT id, name, email
  FROM users
  WHERE status = 'active';

  SELECT * FROM active_users;
  ```

**리뷰:** 데이터 보안과 쿼리 단순화에 유용

---

## 트리거 (Trigger)

**한줄설명:** 특정한 이벤트(INSERT, UPDATE, DELETE)가 발생할 때 자동으로 실행되는 프로시저

**상세설명:**
- 사용 예:
  - 데이터 변경 감사
  - 데이터 유효성 검증
  - 관련 테이블 자동 업데이트
  - 로그 기록

- 예시:
  ```sql
  CREATE TRIGGER update_user_modified
  AFTER UPDATE ON users
  FOR EACH ROW
  BEGIN
    UPDATE user_audit SET modified_at = NOW()
    WHERE user_id = NEW.id;
  END;
  ```

**리뷰:** 복잡한 데이터 관계 관리에 유용하지만 과용하지 말 것

---

## 저장 프로시저 (Stored Procedure)

**한줄설명:** 데이터베이스에 저장되는 재사용 가능한 SQL 코드 블록

**상세설명:**
- 특징:
  - 네트워크 왕복 감소 (성능 향상)
  - 보안 강화 (권한 제어)
  - 재사용성
  - 트랜잭션 관리 용이

- 예시:
  ```sql
  CREATE PROCEDURE transfer_money(
    FROM_ACCOUNT INT,
    TO_ACCOUNT INT,
    AMOUNT DECIMAL
  )
  BEGIN
    START TRANSACTION;
    UPDATE accounts SET balance = balance - AMOUNT
    WHERE id = FROM_ACCOUNT;

    UPDATE accounts SET balance = balance + AMOUNT
    WHERE id = TO_ACCOUNT;
    COMMIT;
  END;
  ```

**리뷰:** 복잡한 비즈니스 로직을 데이터베이스에서 처리할 때 유용

---

## 데이터베이스 백업 (Backup)

**한줄설명:** 데이터 손실에 대비하기 위해 데이터베이스를 복사하여 안전한 위치에 저장하는 과정

**상세설명:**
- 방식:
  1. **전체 백업 (Full Backup)**: 모든 데이터 백업
  2. **증분 백업 (Incremental Backup)**: 마지막 백업 이후 변경된 데이터만
  3. **차등 백업 (Differential Backup)**: 마지막 전체 백업 이후의 모든 변경

- 전략 (RPO/RTO):
  - **RPO (Recovery Point Objective)**: 허용 가능한 데이터 손실 시간
  - **RTO (Recovery Time Objective)**: 복구에 허용되는 시간

**리뷰:** 데이터 보호의 필수 요소

---

## DR 센터 (Disaster Recovery Center)

**한줄설명:** 주 데이터센터에 재해가 발생했을 때 이를 대체하는 별도의 데이터센터

**상세설명:**
- 특징:
  - 실시간 또는 정기적 데이터 동기화
  - 자동 또는 수동 장애 조치 (Failover)
  - 높은 가용성 보장
  - 비용이 높음

- 구성:
  - Active-Passive: 주 DC만 작동, DR은 대기
  - Active-Active: 양쪽 모두 작동, 부하 분산

**리뷰:** 엔터프라이즈급 시스템의 필수 요소
