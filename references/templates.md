# Test Case Common Templates / 테스트 케이스 공통 템플릿 / 测试用例通用模板

## Scenario vs Case / 시나리오 vs 케이스 구분 / 场景 vs 用例 区分

| Criteria / 구분 / 标准 | Test Scenario / 테스트 시나리오 / 测试场景 | Test Case / 테스트 케이스 / 测试用例 |
|-------------------------|--------------------------------------------|-------------------------------------|
| **Level / 수준 / 层级** | High-level (What to test) / 상위 / 高层 | Low-level (How to test) / 하위 / 低层 |
| **Perspective / 관점 / 视角** | Business/User / 비즈니스/사용자 / 业务/用户 | Executor/Technical / 실행자/기술 / 执行者/技术 |
| **Detail / 상세도 / 细节程度** | Overview / 개괄적 설명 / 概述 | Specific steps / 구체적 단계 / 具体步骤 |
| **Relation / 관계 / 关系** | 1 Scenario = N Cases | N Cases ⊂ 1 Scenario |
| **Question / 질문 / 问题** | "What situation to test?" / "어떤 상황을 테스트?" / "测试什么情况？" | "How to test?" / "어떻게 테스트?" / "如何测试？" |

### Hierarchy / 계층 구조 / 层级结构

```
Feature / 기능 / 功能
└── Test Scenario / 테스트 시나리오 / 测试场景 - "What" to test? / "무엇을" 테스트? / "测试什么"？
    └── Test Case / 테스트 케이스 / 测试用例 - "How" to test? / "어떻게" 테스트? / "如何测试"？
        └── Test Step / 테스트 단계 / 测试步骤 - Execution procedure / 실행 절차 / 执行程序
```

### Example: Login Feature / 예시: 로그인 기능 / 示例：登录功能

**Scenarios / 시나리오 / 场景 (3)**

| ID | Scenario / 시나리오 | Type / 유형 |
|----|---------------------|-------------|
| SC-LOGIN-001 | Successful login with valid credentials / 유효한 자격증명으로 로그인 성공 | Happy Path |
| SC-LOGIN-002 | Login failure with invalid credentials / 잘못된 자격증명으로 로그인 실패 | Exception |
| SC-LOGIN-003 | Login attempt with locked account / 계정 잠금 상태에서 로그인 시도 | Exception |

**Cases for SC-LOGIN-001 / 케이스 (SC-LOGIN-001 → 3)**

| ID | Case / 케이스 | Input / 입력 | Expected Result / 예상 결과 |
|----|---------------|--------------|----------------------------|
| TC-LOGIN-001 | Email+Password login / 이메일+비밀번호 정상 로그인 | valid@test.com / Pass123! | Redirect to main page / 메인 페이지 이동 |
| TC-LOGIN-002 | Social login (Google) / 소셜 로그인 | OAuth auth | Redirect to main page / 메인 페이지 이동 |
| TC-LOGIN-003 | Auto-login enabled / 자동 로그인 체크 후 로그인 | Checkbox selected | Session 7 days / 세션 7일 유지 |

**Cases for SC-LOGIN-002 / 케이스 (SC-LOGIN-002 → 4)**

| ID | Case / 케이스 | Input / 입력 | Expected Result / 예상 결과 |
|----|---------------|--------------|----------------------------|
| TC-LOGIN-004 | Non-existent email / 존재하지 않는 이메일 | wrong@test.com | "Invalid email or password" / "이메일 또는 비밀번호 오류" |
| TC-LOGIN-005 | Wrong password / 잘못된 비밀번호 | valid@test.com / wrong | "Invalid email or password" / "이메일 또는 비밀번호 오류" |
| TC-LOGIN-006 | Invalid email format / 이메일 형식 오류 | invalid-email | "Invalid email format" / "이메일 형식이 올바르지 않습니다" |
| TC-LOGIN-007 | Empty password / 비밀번호 빈값 | valid@test.com / (empty) | "Enter password" / "비밀번호를 입력하세요" |

**Full Structure / 전체 구조 / 完整结构**

```
Login Feature / 로그인 기능 / 登录功能
├── SC-LOGIN-001: Successful login / 정상 로그인 / 成功登录
│   ├── TC-LOGIN-001: Email+Password / 이메일+비밀번호 / 邮箱+密码
│   ├── TC-LOGIN-002: Social login / 소셜 로그인 / 社交登录
│   └── TC-LOGIN-003: Auto-login / 자동 로그인 / 自动登录
├── SC-LOGIN-002: Login failure / 로그인 실패 / 登录失败
│   ├── TC-LOGIN-004: Non-existent email / 없는 이메일 / 不存在的邮箱
│   ├── TC-LOGIN-005: Wrong password / 잘못된 비밀번호 / 错误密码
│   ├── TC-LOGIN-006: Invalid email format / 이메일 형식 오류 / 邮箱格式错误
│   └── TC-LOGIN-007: Empty password / 비밀번호 빈값 / 密码为空
└── SC-LOGIN-003: Account locked / 계정 잠금 / 账户锁定
    ├── TC-LOGIN-008: Lock triggered / 잠금 발생 / 触发锁定
    └── TC-LOGIN-009: Lock released / 잠금 해제 / 解除锁定
```

---

## ID Naming Convention / ID 명명 규칙

### Scenario ID / 시나리오 ID
```
SC-[FEATURE]-[NNN]

Example / 예: SC-LOGIN-001, SC-PAYMENT-003, SC-SEARCH-002
```

### Case ID / 케이스 ID
```
TC-[TYPE]-[NNN] or TC-[FEATURE]-[NNN]

TYPE (by test type / 테스트 유형별):
- UNIT: Unit test / 단위 테스트
- INT: Integration test / 통합 테스트
- API: API test / API 테스트
- E2E: E2E test / E2E 테스트
- SEC: Security test / 보안 테스트
- PERF: Performance test / 성능 테스트
- A11Y: Accessibility test / 접근성 테스트

Example / 예: TC-API-001, TC-E2E-015, TC-LOGIN-007
```

## Priority Criteria / 우선순위 기준

| Priority / 우선순위 | Criteria / 기준 | Example / 예시 |
|---------------------|-----------------|----------------|
| **Critical** | Core business function, service unavailable if fails / 핵심 비즈니스 기능, 실패 시 서비스 불가 | Login, Payment / 로그인, 결제 |
| **High** | Major function, significant UX impact / 주요 기능, 사용자 경험에 큰 영향 | Search, Order / 검색, 주문 |
| **Medium** | Supporting function, alternative exists / 보조 기능, 대안 경로 존재 | Filtering, Sorting / 필터링, 정렬 |
| **Low** | Additional function, minimal impact / 부가 기능, 미사용 시 영향 적음 | UI enhancement / UI 개선, 편의 기능 |

## Detailed Test Case Template / 테스트 케이스 상세 템플릿

```markdown
## TC-[TYPE]-[NNN]: [Test Title / 테스트 제목]

### Basic Info / 기본 정보
| Item / 항목 | Content / 내용 |
|-------------|----------------|
| **ID** | TC-TYPE-NNN |
| **Title / 제목** | Clear test purpose / 명확한 테스트 목적 |
| **Priority / 우선순위** | Critical / High / Medium / Low |
| **Test Type / 테스트 유형** | Unit / Integration / API / E2E / Security / Performance / Accessibility |
| **Related Requirement / 관련 요구사항** | REQ-XXX |

### Preconditions / 전제조건
- Condition 1 / 조건 1: [State/environment / 상태/환경 설명]
- Condition 2 / 조건 2: [Required data/settings / 필요한 데이터/설정]

### Test Data / 테스트 데이터
```json
{
  "input": {},
  "expected": {}
}
```

### Test Steps / 테스트 단계
| # | Step / 단계 | Input/Action / 입력/액션 | Expected Result / 예상 결과 |
|---|-------------|-------------------------|----------------------------|
| 1 | [Action / 동작] | [Input / 입력값] | [Result / 기대결과] |
| 2 | [Action / 동작] | [Input / 입력값] | [Result / 기대결과] |

### Meta Info / 메타 정보
| Item / 항목 | Content / 내용 |
|-------------|----------------|
| **Automation / 자동화 가능성** | Possible / 가능 | Not possible (reason) / 불가능 (사유) |
| **Automation Tool / 자동화 도구** | Jest / Playwright / k6 / etc. |
| **Environment / 실행 환경** | Local / Staging / Production |
| **Notes / 비고** | Additional info / 추가 정보 |
```

## Scenario Summary Template / 시나리오 요약 템플릿

```markdown
# [Feature] Test Scenarios / [기능명] 테스트 시나리오

## Overview / 개요
| Item / 항목 | Content / 내용 |
|-------------|----------------|
| **Test Target / 테스트 대상** | [Description / 대상 설명] |
| **Test Scope / 테스트 범위** | [Description / 범위 설명] |
| **Test Type / 테스트 유형** | [Type / 유형] |
| **Created / 작성일** | YYYY-MM-DD |

## Scenario List / 시나리오 목록

| ID | Scenario / 시나리오 | Flow Type / 흐름 유형 | Priority / 우선순위 | Cases / 케이스 수 |
|----|---------------------|----------------------|---------------------|-------------------|
| SC-001 | Normal login / 정상 로그인 | Happy Path | Critical | 3 |
| SC-002 | Wrong password / 잘못된 비밀번호 | Exception | High | 2 |
| SC-003 | Account locked / 계정 잠금 | Exception | High | 2 |

## Coverage Matrix / 커버리지 매트릭스

| Requirement / 요구사항 | Scenario / 시나리오 | Cases / 케이스 | Status / 상태 |
|------------------------|---------------------|----------------|---------------|
| REQ-001 | SC-001, SC-002 | TC-001~005 | Complete / 완료 |
| REQ-002 | SC-003 | TC-006~007 | In Progress / 진행중 |
```

## Test Result Template / 테스트 결과 템플릿

```markdown
# Test Execution Result / 테스트 실행 결과

## Summary / 요약
| Item / 항목 | Value / 값 |
|-------------|------------|
| **Execution Date / 실행일** | YYYY-MM-DD |
| **Environment / 환경** | Staging |
| **Total Cases / 전체 케이스** | 50 |
| **Passed / 성공** | 45 (90%) |
| **Failed / 실패** | 3 (6%) |
| **Skipped / 스킵** | 2 (4%) |

## Failed Cases / 실패 케이스
| ID | Title / 제목 | Failure Reason / 실패 사유 | Assignee / 담당자 |
|----|--------------|---------------------------|-------------------|
| TC-API-015 | Large file upload / 대용량 파일 업로드 | Timeout / 타임아웃 | @dev |
```
