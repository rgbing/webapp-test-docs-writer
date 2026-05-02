---
name: webapp-test-docs-writer
description: |
  Write test scenarios and test cases for web service verification. Generate test documents based on functional specs, API specs, and code analysis for Unit/Integration/API/E2E/Security/Performance/Accessibility testing.
  웹서비스 검증을 위한 테스트 시나리오 및 테스트 케이스 작성. 기능 명세서, API 스펙, 코드 분석 기반으로 Unit/Integration/API/E2E/Security/Performance/Accessibility 테스트 문서 생성.
  为Web服务验证编写测试场景和测试用例。基于功能规范、API规范和代码分析生成单元测试/集成测试/API测试/E2E测试/安全测试/性能测试/无障碍测试文档。
  Triggers: "테스트 케이스 작성", "테스트 시나리오", "QA 문서", "test case", "test scenario", "write tests", "QA documentation", "测试用例", "测试场景", "测试文档", "编写测试", "测试用例编写"
---

# Webapp Test Docs Writer

Write test scenarios and test cases for web service verification.
웹서비스 검증을 위한 테스트 시나리오/케이스 작성 스킬.
为Web服务验证编写测试场景和测试用例的技能。

## Language / 语言 / 언어

Detect user's language and respond accordingly.
사용자 언어를 감지하여 해당 언어로 응답.
检测用户语言并使用相应语言响应。

- English request → English output / 英文请求 → 英文输出 / 영문 요청 → 영문 출력
- 한글 요청 → 한글 출력 / 韩语请求 → 韩语输出
- 中文请求 → 中文输出 / Chinese request → Chinese output

## Workflow

```
1. Analyze Input    → 2. Select Test Type → 3. Derive Scenarios → 4. Write Cases → 5. Review
   输入分析            测试类型选择           场景推导            用例编写          审查
   입력 분석           테스트 유형 선택       시나리오 도출         케이스 작성       리뷰
```

### Step 0: Dedup Check (MANDATORY) / 中重复检查（必选） / 중복 체크 (필수)

Before writing any test scenario or case, perform these checks:
在编写任何测试场景或用例之前，执行以下检查：
테스트 시나리오/케이스를 작성하기 전에 반드시 아래를 확인합니다:

1. **Read dedup policy / 读取去重策略 / 중복 방지 정책 확인**: If `docs/testing/TEST_DEDUP_POLICY.md` exists, read and enforce it
2. **Search existing tests / 搜索现有测试 / 기존 테스트 검색**: `grep -r "target_endpoint_or_function" tests/ -l` / `grep -r "대상_엔드포인트_또는_함수" tests/ -l`
3. **Layer ownership / 层级所有权 / 계층 소유권 확인**: Each item belongs to ONE layer only / 每个项目仅属于一个层级 / 각 항목은 하나의 계층에만 속함
   - Pure function → unit / 纯函数 → 单元测试 | API endpoint → api / API端点 → API测试 | Browser flow → e2e / 浏览器流程 → E2E测试 | OWASP → security / OWASP → 安全测试
   - Auth 401/403 → per-feature api file only (NOT bulk security files / 不是批量安全文件 / 일괄 보안 파일 금지)
4. **If existing file found / 如果发现现有文件 / 기존 파일 발견 시**: Add TC to that file (do NOT create new file / 不要创建新文件 / 신규 파일 생성 금지)
5. **Prohibited patterns / 禁止模式 / 금지 패턴**:
   - Placeholder TC with no real assertions / 没有真实断言的占位符测试用例 / 실제 검증 없는 placeholder TC
   - Duplicate TC across layers / 跨层级重复的测试用例 / 계층 간 동일 TC 중복
   - TC for unimplemented features / 未实现功能的测试用例 / 미구현 기능에 대한 TC
   - Aggregation files bundling separate endpoints / 捆绑单独端点的聚合文件 / 개별 엔드포인트를 묶는 집합 파일

### Step 1: Analyze Input / 输入分析 / 입력 분석

| Source / 来源 / 소스 | Check / 检查事项 / 확인 사항 |
|---------------------|----------------------------|
| **Functional Spec / 功能规范 / 기능 명세서** | Requirements, user stories, acceptance criteria / 需求、用户故事、验收标准 / 요구사항, 사용자 스토리, 인수 조건 |
| **API Spec / API规范 / API 스펙** | Endpoints, request/response schema, status codes / 端点、请求/响应模式、状态码 / 엔드포인트, 요청/응답 스키마, 상태코드 |
| **Code / 代码 / 코드** | Business logic, branching, exception handling / 业务逻辑、分支、异常处理 / 비즈니스 로직, 분기 조건, 예외 처리 |

### Step 2: Select Test Type / 选择测试类型 / 테스트 유형 선택

| Type / 类型 / 유형 | Purpose / 目的 / 목적 | Guide / 指南 / 가이드 |
|--------------------|---------------------|----------------------|
| **Unit** / 单元测试 | Verify individual functions/modules / 验证单个函数/模块 / 개별 함수/모듈 검증 | [references/unit/](references/unit/) |
| **Integration** / 集成测试 | Verify component interactions / 验证组件交互 / 컴포넌트 간 연동 검증 | [references/integration/](references/integration/) |
| **API** / API测试 | Verify REST/GraphQL endpoints / 验证REST/GraphQL端点 / REST/GraphQL 엔드포인트 검증 | [references/api/](references/api/) |
| **E2E** / 端到端测试 | Verify complete user flows / 验证完整用户流程 / 전체 사용자 흐름 검증 | [references/e2e/](references/e2e/) |
| **Security** / 安全测试 | Verify security vulnerabilities / 验证安全漏洞 / 보안 취약점 검증 | [references/security/](references/security/) |
| **Performance** / 性能测试 | Verify performance/load / 验证性能/负载 / 성능/부하 검증 | [references/performance/](references/performance/) |
| **Accessibility** / 无障碍测试 | Verify WCAG compliance / 验证WCAG合规性 / 접근성(WCAG) 검증 | [references/accessibility/](references/accessibility/) |

### Step 3: Derive Scenarios / 推导场景 / 시나리오 도출

For each feature, derive scenarios from these perspectives:
对于每个功能，从以下角度推导场景：
각 기능에 대해 다음 관점으로 시나리오 도출:

1. **Happy Path / 正常路径 / 정상 흐름** - Expected behavior / 预期行为 / 기대대로 동작
2. **Alternative / 替代路径 / 대안 흐름** - Success via different path / 通过不同路径成功 / 다른 경로로 성공
3. **Exception / 异常路径 / 예외 흐름** - Error/failure cases / 错误/失败案例 / 오류/실패 케이스
4. **Boundary / 边界值 / 경계값** - Min/max/boundary conditions / 最小/最大/边界条件 / 최소/최대/경계 조건

### Step 4: Write Cases / 编写用例 / 케이스 작성

Use templates from [references/templates.md](references/templates.md).
使用 [references/templates.md](references/templates.md) 中的模板。

**Required fields / 必填字段 / 필수 항목:**

| Field / 字段 / 항목 | Description / 说明 / 설명 |
|--------------------|--------------------------|
| ID | Unique identifier (e.g., TC-API-001) / 唯一标识符（如：TC-API-001） / 고유 식별자 |
| Title / 标题 / 제목 | Clear test purpose / 清晰的测试目的 / 테스트 목적 명확히 표현 |
| Preconditions / 前置条件 / 전제조건 | Required state before test / 测试前所需状态 / 테스트 전 필요한 상태 |
| Test Steps / 测试步骤 / 테스트 단계 | Sequential execution steps / 顺序执行步骤 / 순차적 실행 단계 |
| Expected Results / 预期结果 / 예상 결과 | Expected outcome per step / 每个步骤的预期结果 / 각 단계별 기대 결과 |
| Priority / 优先级 / 우선순위 | Critical / High / Medium / Low / 关键/高/中/低 |
| Test Data / 测试数据 / 테스트 데이터 | Input data and examples / 输入数据和示例 / 입력 데이터 및 예시 |
| Automation / 自动化可能性 / 자동화 가능성 | Automation feasibility / 自动化可行性 / 자동화 적합 여부 |

### Step 5: Review Checklist / 审查检查清单 / 리뷰 체크리스트

- [ ] 100% requirements coverage / 100%需求覆盖 / 요구사항 100% 커버리지
- [ ] Both positive/negative cases / 正面和负面案例 / 긍정/부정 케이스 모두 포함
- [ ] Boundary tests included / 包含边界测试 / 경계값 테스트 포함
- [ ] Test data is clear / 测试数据清晰 / 테스트 데이터 명확
- [ ] Steps are reproducible / 步骤可复现 / 단계가 재현 가능
- [ ] Expected results are verifiable / 预期结果可验证 / 예상 결과가 검증 가능

## Output Format / 输出格式 / 출력 형식

### Scenario Document / 场景文档 / 시나리오 문서

```markdown
# [Feature] Test Scenarios / [功能名] 测试场景 / [기능명] 테스트 시나리오

## Overview / 概述 / 개요
| Item / 项目 / 항목 | Content / 内容 / 내용 |
|--------------------|----------------------|
| Target / 目标 / 대상 | [Test target / 测试目标 / 테스트 대상] |
| Scope / 范围 / 범위 | [Test scope / 测试范围 / 테스트 범위] |
| Test Type / 测试类型 / 테스트 유형 | [Unit/Integration/API/E2E/Security/Performance/Accessibility] |

## Scenario List / 场景列表 / 시나리오 목록

| ID | Scenario / 场景 / 시나리오 | Type / 类型 / 유형 | Priority / 优先级 / 우선순위 |
|----|---------------------------|---------------------|---------------------------|
| SC-001 | [Description / 描述 / 설명] | Happy Path | High |
```

### Test Case Document / 测试用例文档 / 테스트 케이스 문서

```markdown
## TC-[TYPE]-[NNN]: [Test Title / 测试标题 / 테스트 제목]

| Item / 项目 / 항목 | Content / 内容 / 내용 |
|--------------------|----------------------|
| **Priority / 优先级 / 우선순위** | High |
| **Preconditions / 前置条件 / 전제조건** | - Condition 1 / 条件 1 / 조건 1<br>- Condition 2 / 条件 2 / 조건 2 |
| **Test Data / 测试数据 / 테스트 데이터** | `{"key": "value"}` |

### Test Steps / 测试步骤 / 테스트 단계

| # | Step / 步骤 / 단계 | Expected Result / 预期结果 / 예상 결과 |
|---|-------------------|----------------------------------------|
| 1 | [Action / 操作 / 액션] | [Result / 结果 / 결과] |
| 2 | [Action / 操作 / 액션] | [Result / 结果 / 결과] |

### Meta Info / 元信息 / 메타 정보
- Automation / 自动化 / 자동화: Possible / 可行 / 가능 | Not possible / 不可行 / 불가능
- Related Requirement / 相关需求 / 관련 요구사항: REQ-001
- Notes / 备注 / 비고: [Additional info / 附加信息 / 추가 정보]
```

## Quick Start / 快速开始

When user requests test writing / 当用户请求编写测试时 / 사용자가 테스트 작성 요청 시:

1. Identify test target (feature/API/page) / 识别测试目标（功能/API/页面） / 테스트 대상 파악
2. Refer to relevant test type guide / 参考相关测试类型指南 / 해당 테스트 유형 가이드 참조
3. Derive scenarios then write cases / 推导场景然后编写用例 / 시나리오 도출 후 케이스 작성
4. Output in Markdown table format / 以Markdown表格格式输出 / Markdown 테이블 형식으로 출력
