# webapp-test-docs-writer

Claude Code용 웹서비스 테스트 문서 작성 스킬.

[![English](https://img.shields.io/badge/lang-English-red.svg)](README.md)
[![Chinese](https://img.shields.io/badge/lang-中文-red.svg)](README.zh.md)

## 개요

이 스킬은 웹서비스 검증을 위한 테스트 시나리오와 테스트 케이스를 생성합니다. 7가지 테스트 유형을 지원하며 사용자의 언어에 따라 영어/한글/중국어 문서를 출력합니다.

## 설치

### 방법 1: 심볼릭 링크 (개발용)

```bash
# 저장소 클론
git clone https://github.com/greeun/webapp-test-docs-writer.git

# Claude Code 스킬 디렉토리에 심볼릭 링크 생성
ln -s $(pwd)/webapp-test-docs-writer ~/.claude/skills/webapp-test-docs-writer
```

### 방법 2: .skill 패키지 사용

```bash
# .skill 파일 복사 및 압축 해제
cp webapp-test-docs-writer.skill ~/.claude/skills/
cd ~/.claude/skills/
unzip webapp-test-docs-writer.skill -d webapp-test-docs-writer
rm webapp-test-docs-writer.skill
```

## 사용법

### 트리거 키워드

| 언어 | 키워드 |
|------|--------|
| **영어** | "test case", "test scenario", "write tests", "QA documentation" |
| **한글** | "테스트 케이스 작성", "테스트 시나리오", "QA 문서" |
| **중국어** | "测试用例", "测试场景", "测试文档", "编写测试", "测试用例编写" |

### 예시 프롬프트

```
"로그인 기능 테스트 케이스 작성해줘"
"회원가입 API 테스트 시나리오 만들어줘"
"결제 흐름 E2E 테스트 케이스 생성해줘"
"인증 보안 테스트 케이스 작성해줘"
```

## 테스트 유형

| 유형 | 목적 | 가이드 |
|------|------|--------|
| **Unit** | 개별 함수/모듈 검증 | `references/unit/guide.md` |
| **Integration** | 컴포넌트 간 연동 검증 | `references/integration/guide.md` |
| **API** | REST/GraphQL 엔드포인트 검증 | `references/api/guide.md` |
| **E2E** | 전체 사용자 흐름 검증 | `references/e2e/guide.md` |
| **Security** | 보안 취약점 검증 | `references/security/guide.md` |
| **Performance** | 성능/부하 검증 | `references/performance/guide.md` |
| **Accessibility** | WCAG 준수 검증 | `references/accessibility/guide.md` |

## 워크플로우

```
1. 입력 분석 → 2. 테스트 유형 선택 → 3. 시나리오 도출 → 4. 케이스 작성 → 5. 리뷰
```

### Step 1: 입력 분석

스킬이 분석하는 소스:
- 기능 명세서
- API 스펙 (OpenAPI/Swagger)
- 소스 코드 분석

### Step 2: 테스트 유형 선택

테스트 대상 기능에 따라 적절한 테스트 유형을 선택합니다.

### Step 3: 시나리오 도출

4가지 관점에서 시나리오를 도출합니다:
1. **Happy Path (정상 흐름)** - 기대대로 동작하는 케이스
2. **Alternative (대안 흐름)** - 다른 경로로 성공하는 케이스
3. **Exception (예외 흐름)** - 오류/실패 케이스
4. **Boundary (경계값)** - 최소/최대/경계 조건

### Step 4: 케이스 작성

각 테스트 케이스에 포함되는 항목:
- ID (예: TC-API-001)
- 제목
- 전제조건
- 테스트 단계
- 예상 결과
- 우선순위
- 테스트 데이터
- 자동화 가능성

### Step 5: 리뷰

체크리스트:
- [ ] 요구사항 100% 커버리지
- [ ] 긍정/부정 케이스 모두 포함
- [ ] 경계값 테스트 포함
- [ ] 테스트 데이터 명확
- [ ] 단계가 재현 가능
- [ ] 예상 결과가 검증 가능

## 출력 형식

### 산출물

| # | 문서 | 형식 | 설명 |
|---|------|------|------|
| 1 | 테스트 시나리오 문서 | Markdown | 시나리오 목록 및 커버리지 |
| 2 | 테스트 케이스 문서 | Markdown 테이블 | 상세 테스트 단계 |
| 3 | 커버리지 매트릭스 | Markdown 테이블 | 요구사항-시나리오-케이스 매핑 |

### 시나리오 vs 테스트 케이스

| 구분 | 시나리오 | 테스트 케이스 |
|------|----------|--------------|
| **수준** | 상위 (What to test) | 하위 (How to test) |
| **관점** | 비즈니스/사용자 | 기술/실행자 |
| **상세도** | 개괄적 | 구체적 단계 |
| **관계** | 1 시나리오 = N 케이스 | N 케이스 ⊂ 1 시나리오 |

### ID 명명 규칙

```
시나리오: SC-[기능]-[NNN]
예: SC-LOGIN-001, SC-PAYMENT-003

테스트 케이스: TC-[TYPE]-[NNN] 또는 TC-[기능]-[NNN]
예: TC-API-001, TC-E2E-015, TC-LOGIN-007

TYPE 코드:
- UNIT: 단위 테스트
- INT: 통합 테스트
- API: API 테스트
- E2E: E2E 테스트
- SEC: 보안 테스트
- PERF: 성능 테스트
- A11Y: 접근성 테스트
```

### 우선순위 기준

| 우선순위 | 기준 | 예시 |
|----------|------|------|
| **Critical** | 핵심 비즈니스 기능, 실패 시 서비스 불가 | 로그인, 결제 |
| **High** | 주요 기능, 사용자 경험에 큰 영향 | 검색, 주문 |
| **Medium** | 보조 기능, 대안 경로 존재 | 필터링, 정렬 |
| **Low** | 부가 기능, 미사용 시 영향 적음 | UI 개선 |

## 출력 예시

### 테스트 시나리오 문서

```markdown
# 로그인 기능 테스트 시나리오

## 개요
| 항목 | 내용 |
|------|------|
| **테스트 대상** | 사용자 인증 시스템 |
| **테스트 범위** | 로그인, 소셜 로그인, 계정 잠금 |
| **테스트 유형** | API, E2E |

## 시나리오 목록

| ID | 시나리오 | 흐름 유형 | 우선순위 | 케이스 수 |
|----|----------|----------|----------|----------|
| SC-LOGIN-001 | 유효한 자격증명으로 로그인 | Happy Path | Critical | 3 |
| SC-LOGIN-002 | 잘못된 자격증명으로 실패 | Exception | High | 4 |
```

### 테스트 케이스 문서

```markdown
## TC-API-001: 이메일+비밀번호 정상 로그인

| 항목 | 내용 |
|------|------|
| **우선순위** | Critical |
| **전제조건** | - 유효한 계정 존재<br>- 로그아웃 상태 |
| **테스트 데이터** | `{"email": "test@example.com", "password": "Pass123!"}` |

### 테스트 단계

| # | 단계 | 예상 결과 |
|---|------|----------|
| 1 | POST /api/auth/login 호출 | 200 OK |
| 2 | 응답 body 확인 | accessToken 포함 |

### 메타 정보
- 자동화: 가능 (Jest + Supertest)
- 관련 요구사항: REQ-AUTH-001
```

## 파일 구조

```
webapp-test-docs-writer/
├── SKILL.md                          # 메인 스킬 정의
├── README.md                         # 영문 문서
├── README.ko.md                      # 한글 문서 (이 파일)
├── README.zh.md                      # 중국어 문서
└── references/
    ├── templates.md                  # 공통 템플릿
    ├── unit/guide.md                 # 단위 테스트 가이드
    ├── integration/guide.md          # 통합 테스트 가이드
    ├── api/guide.md                  # API 테스트 가이드
    ├── e2e/guide.md                  # E2E 테스트 가이드
    ├── security/guide.md             # 보안 테스트 가이드
    ├── performance/guide.md          # 성능 테스트 가이드
    └── accessibility/guide.md        # 접근성 테스트 가이드
```

## 자동화 도구 참조

| 테스트 유형 | 도구 |
|-------------|------|
| **Unit** | Jest, Vitest, pytest, JUnit |
| **Integration** | Supertest, TestClient, Spring Boot Test |
| **API** | Postman/Newman, REST Assured, httpx |
| **E2E** | Playwright, Cypress, Selenium |
| **Security** | OWASP ZAP, Burp Suite, sqlmap |
| **Performance** | k6, JMeter, Gatling, Locust |
| **Accessibility** | axe DevTools, WAVE, Lighthouse |

## 라이선스

MIT License

## 작성자

Claude Code skill-wizard로 생성됨.
