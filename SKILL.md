---
name: webapp-test-docs-writer
description: |
  Write test scenarios and test cases for web service verification. Generate test documents based on functional specs, API specs, and code analysis for Unit/Integration/API/E2E/Security/Performance/Accessibility testing.
  웹서비스 검증을 위한 테스트 시나리오 및 테스트 케이스 작성. 기능 명세서, API 스펙, 코드 분석 기반으로 Unit/Integration/API/E2E/Security/Performance/Accessibility 테스트 문서 생성.
  Triggers: "테스트 케이스 작성", "테스트 시나리오", "QA 문서", "test case", "test scenario", "write tests", "QA documentation"
---

# Webapp Test Docs Writer

Write test scenarios and test cases for web service verification.
웹서비스 검증을 위한 테스트 시나리오/케이스 작성 스킬.

## Language / 언어

Detect user's language and respond accordingly.
사용자 언어를 감지하여 해당 언어로 응답.

- English request → English output
- 한글 요청 → 한글 출력

## Workflow

```
1. Analyze Input    → 2. Select Test Type → 3. Derive Scenarios → 4. Write Cases → 5. Review
   입력 분석           테스트 유형 선택       시나리오 도출         케이스 작성       리뷰
```

### Step 0: Dedup Check (MANDATORY) / 중복 체크 (필수)

Before writing any test scenario or case, perform these checks:
테스트 시나리오/케이스를 작성하기 전에 반드시 아래를 확인합니다:

1. **Read dedup policy / 중복 방지 정책 확인**: If `docs/testing/TEST_DEDUP_POLICY.md` exists, read and enforce it
2. **Search existing tests / 기존 테스트 검색**: `grep -r "대상_엔드포인트_또는_함수" tests/ -l`
3. **Layer ownership / 계층 소유권 확인**: Each item belongs to ONE layer only
   - Pure function → unit | API endpoint → api | Browser flow → e2e | OWASP → security
   - Auth 401/403 → per-feature api file only (NOT bulk security files / 일괄 보안 파일 금지)
4. **If existing file found / 기존 파일 발견 시**: Add TC to that file (do NOT create new file / 신규 파일 생성 금지)
5. **Prohibited patterns / 금지 패턴**:
   - Placeholder TC with no real assertions / 실제 검증 없는 placeholder TC
   - Duplicate TC across layers / 계층 간 동일 TC 중복
   - TC for unimplemented features / 미구현 기능에 대한 TC
   - Aggregation files bundling separate endpoints / 개별 엔드포인트를 묶는 집합 파일

### Step 1: Analyze Input / 입력 분석

| Source / 소스 | Check / 확인 사항 |
|---------------|-------------------|
| **Functional Spec / 기능 명세서** | Requirements, user stories, acceptance criteria / 요구사항, 사용자 스토리, 인수 조건 |
| **API Spec** | Endpoints, request/response schema, status codes / 엔드포인트, 요청/응답 스키마, 상태코드 |
| **Code / 코드** | Business logic, branching, exception handling / 비즈니스 로직, 분기 조건, 예외 처리 |

### Step 2: Select Test Type / 테스트 유형 선택

| Type / 유형 | Purpose / 목적 | Guide / 가이드 |
|-------------|----------------|----------------|
| **Unit** | Verify individual functions/modules / 개별 함수/모듈 검증 | [references/unit/](references/unit/) |
| **Integration** | Verify component interactions / 컴포넌트 간 연동 검증 | [references/integration/](references/integration/) |
| **API** | Verify REST/GraphQL endpoints / REST/GraphQL 엔드포인트 검증 | [references/api/](references/api/) |
| **E2E** | Verify complete user flows / 전체 사용자 흐름 검증 | [references/e2e/](references/e2e/) |
| **Security** | Verify security vulnerabilities / 보안 취약점 검증 | [references/security/](references/security/) |
| **Performance** | Verify performance/load / 성능/부하 검증 | [references/performance/](references/performance/) |
| **Accessibility** | Verify WCAG compliance / 접근성(WCAG) 검증 | [references/accessibility/](references/accessibility/) |

### Step 3: Derive Scenarios / 시나리오 도출

For each feature, derive scenarios from these perspectives:
각 기능에 대해 다음 관점으로 시나리오 도출:

1. **Happy Path / 정상 흐름** - Expected behavior / 기대대로 동작
2. **Alternative / 대안 흐름** - Success via different path / 다른 경로로 성공
3. **Exception / 예외 흐름** - Error/failure cases / 오류/실패 케이스
4. **Boundary / 경계값** - Min/max/boundary conditions / 최소/최대/경계 조건

### Step 4: Write Cases / 케이스 작성

Use templates from [references/templates.md](references/templates.md).

**Required fields / 필수 항목:**

| Field / 항목 | Description / 설명 |
|--------------|-------------------|
| ID | Unique identifier (e.g., TC-API-001) / 고유 식별자 |
| Title / 제목 | Clear test purpose / 테스트 목적 명확히 표현 |
| Preconditions / 전제조건 | Required state before test / 테스트 전 필요한 상태 |
| Test Steps / 테스트 단계 | Sequential execution steps / 순차적 실행 단계 |
| Expected Results / 예상 결과 | Expected outcome per step / 각 단계별 기대 결과 |
| Priority / 우선순위 | Critical / High / Medium / Low |
| Test Data / 테스트 데이터 | Input data and examples / 입력 데이터 및 예시 |
| Automation / 자동화 가능성 | Automation feasibility / 자동화 적합 여부 |

### Step 5: Review Checklist / 리뷰 체크리스트

- [ ] 100% requirements coverage / 요구사항 100% 커버리지
- [ ] Both positive/negative cases / 긍정/부정 케이스 모두 포함
- [ ] Boundary tests included / 경계값 테스트 포함
- [ ] Test data is clear / 테스트 데이터 명확
- [ ] Steps are reproducible / 단계가 재현 가능
- [ ] Expected results are verifiable / 예상 결과가 검증 가능

## Output Format / 출력 형식

### Scenario Document / 시나리오 문서

```markdown
# [Feature] Test Scenarios / [기능명] 테스트 시나리오

## Overview / 개요
| Item / 항목 | Content / 내용 |
|-------------|----------------|
| Target / 대상 | [Test target / 테스트 대상] |
| Scope / 범위 | [Test scope / 테스트 범위] |
| Test Type / 테스트 유형 | [Unit/Integration/API/E2E/Security/Performance/Accessibility] |

## Scenario List / 시나리오 목록

| ID | Scenario / 시나리오 | Type / 유형 | Priority / 우선순위 |
|----|---------------------|-------------|---------------------|
| SC-001 | [Description / 설명] | Happy Path | High |
```

### Test Case Document / 테스트 케이스 문서

```markdown
## TC-[TYPE]-[NNN]: [Test Title / 테스트 제목]

| Item / 항목 | Content / 내용 |
|-------------|----------------|
| **Priority / 우선순위** | High |
| **Preconditions / 전제조건** | - Condition 1 / 조건 1<br>- Condition 2 / 조건 2 |
| **Test Data / 테스트 데이터** | `{"key": "value"}` |

### Test Steps / 테스트 단계

| # | Step / 단계 | Expected Result / 예상 결과 |
|---|-------------|----------------------------|
| 1 | [Action / 액션] | [Result / 결과] |
| 2 | [Action / 액션] | [Result / 결과] |

### Meta Info / 메타 정보
- Automation / 자동화: Possible / 가능 | Not possible / 불가능
- Related Requirement / 관련 요구사항: REQ-001
- Notes / 비고: [Additional info / 추가 정보]
```

## Quick Start

When user requests test writing / 사용자가 테스트 작성 요청 시:

1. Identify test target (feature/API/page) / 테스트 대상 파악
2. Refer to relevant test type guide / 해당 테스트 유형 가이드 참조
3. Derive scenarios then write cases / 시나리오 도출 후 케이스 작성
4. Output in Markdown table format / Markdown 테이블 형식으로 출력
