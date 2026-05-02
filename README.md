# webapp-test-docs-writer

Web Service Test Documentation Writer Skill for Claude Code.

[![Korean](https://img.shields.io/badge/lang-한글-blue.svg)](README.ko.md)
[![Chinese](https://img.shields.io/badge/lang-中文-red.svg)](README.zh.md)

## Overview

This skill generates test scenarios and test cases for web service verification. It supports 7 test types and outputs trilingual (English/Korean/Chinese) documentation based on user's language.

## Installation

### Option 1: Symlink (Development)

```bash
# Clone the repository
git clone https://github.com/greeun/webapp-test-docs-writer.git

# Create symlink to Claude Code skills directory
ln -s $(pwd)/webapp-test-docs-writer ~/.claude/skills/webapp-test-docs-writer
```

### Option 2: From .skill Package

```bash
# Copy .skill file and extract
cp webapp-test-docs-writer.skill ~/.claude/skills/
cd ~/.claude/skills/
unzip webapp-test-docs-writer.skill -d webapp-test-docs-writer
rm webapp-test-docs-writer.skill
```

## Usage

### Trigger Keywords

| Language | Keywords |
|----------|----------|
| **English** | "test case", "test scenario", "write tests", "QA documentation" |
| **Korean** | "테스트 케이스 작성", "테스트 시나리오", "QA 문서" |
| **Chinese** | "测试用例", "测试场景", "测试文档", "编写测试", "测试用例编写" |

### Example Prompts

```
"Write test cases for the login feature"
"Create API test scenarios for user registration"
"Generate E2E test cases for checkout flow"
"Write security test cases for authentication"
```

## Test Types

| Type | Purpose | Guide |
|------|---------|-------|
| **Unit** | Individual function/module verification | `references/unit/guide.md` |
| **Integration** | Component interaction verification | `references/integration/guide.md` |
| **API** | REST/GraphQL endpoint verification | `references/api/guide.md` |
| **E2E** | Complete user flow verification | `references/e2e/guide.md` |
| **Security** | Security vulnerability verification | `references/security/guide.md` |
| **Performance** | Performance/load verification | `references/performance/guide.md` |
| **Accessibility** | WCAG compliance verification | `references/accessibility/guide.md` |

## Workflow

```
1. Analyze Input → 2. Select Test Type → 3. Derive Scenarios → 4. Write Cases → 5. Review
```

### Step 1: Analyze Input

The skill analyzes these sources:
- Functional specifications
- API specifications (OpenAPI/Swagger)
- Source code analysis

### Step 2: Select Test Type

Choose appropriate test type based on the feature being tested.

### Step 3: Derive Scenarios

Scenarios are derived from 4 perspectives:
1. **Happy Path** - Expected normal behavior
2. **Alternative** - Success via different path
3. **Exception** - Error/failure cases
4. **Boundary** - Min/max/edge conditions

### Step 4: Write Cases

Each test case includes:
- ID (e.g., TC-API-001)
- Title
- Preconditions
- Test Steps
- Expected Results
- Priority
- Test Data
- Automation feasibility

### Step 5: Review

Checklist:
- [ ] 100% requirements coverage
- [ ] Both positive/negative cases included
- [ ] Boundary tests included
- [ ] Test data is clear
- [ ] Steps are reproducible
- [ ] Expected results are verifiable

## Output Format

### Deliverables

| # | Document | Format | Description |
|---|----------|--------|-------------|
| 1 | Test Scenario Document | Markdown | Scenario list with coverage |
| 2 | Test Case Document | Markdown Table | Detailed test steps |
| 3 | Coverage Matrix | Markdown Table | Requirement-Scenario-Case mapping |

### Scenario vs Test Case

| Criteria | Scenario | Test Case |
|----------|----------|-----------|
| **Level** | High (What to test) | Low (How to test) |
| **Perspective** | Business/User | Technical/Executor |
| **Detail** | Overview | Specific steps |
| **Relation** | 1 Scenario = N Cases | N Cases ⊂ 1 Scenario |

### ID Naming Convention

```
Scenario: SC-[FEATURE]-[NNN]
Example: SC-LOGIN-001, SC-PAYMENT-003

Test Case: TC-[TYPE]-[NNN] or TC-[FEATURE]-[NNN]
Example: TC-API-001, TC-E2E-015, TC-LOGIN-007

TYPE codes:
- UNIT: Unit test
- INT: Integration test
- API: API test
- E2E: E2E test
- SEC: Security test
- PERF: Performance test
- A11Y: Accessibility test
```

### Priority Levels

| Priority | Criteria | Example |
|----------|----------|---------|
| **Critical** | Core business, service unavailable if fails | Login, Payment |
| **High** | Major function, significant UX impact | Search, Order |
| **Medium** | Supporting function, alternative exists | Filter, Sort |
| **Low** | Additional function, minimal impact | UI enhancement |

## Sample Output

### Test Scenario Document

```markdown
# Login Feature Test Scenarios

## Overview
| Item | Content |
|------|---------|
| **Test Target** | User Authentication System |
| **Test Scope** | Login, Social Login, Account Lock |
| **Test Type** | API, E2E |

## Scenario List

| ID | Scenario | Flow Type | Priority | Cases |
|----|----------|-----------|----------|-------|
| SC-LOGIN-001 | Login with valid credentials | Happy Path | Critical | 3 |
| SC-LOGIN-002 | Login failure with invalid credentials | Exception | High | 4 |
```

### Test Case Document

```markdown
## TC-API-001: Email + Password Normal Login

| Item | Content |
|------|---------|
| **Priority** | Critical |
| **Preconditions** | - Valid account exists<br>- Logged out state |
| **Test Data** | `{"email": "test@example.com", "password": "Pass123!"}` |

### Test Steps

| # | Step | Expected Result |
|---|------|-----------------|
| 1 | Call POST /api/auth/login | 200 OK |
| 2 | Check response body | Contains accessToken |

### Meta Info
- Automation: Possible (Jest + Supertest)
- Related Requirement: REQ-AUTH-001
```

## File Structure

```
webapp-test-docs-writer/
├── SKILL.md                          # Main skill definition
├── README.md                         # This file (English)
├── README.ko.md                      # Korean documentation
├── README.zh.md                      # Chinese documentation
└── references/
    ├── templates.md                  # Common templates
    ├── unit/guide.md                 # Unit test guide
    ├── integration/guide.md          # Integration test guide
    ├── api/guide.md                  # API test guide
    ├── e2e/guide.md                  # E2E test guide
    ├── security/guide.md             # Security test guide
    ├── performance/guide.md          # Performance test guide
    └── accessibility/guide.md        # Accessibility test guide
```

## Automation Tools Reference

| Test Type | Tools |
|-----------|-------|
| **Unit** | Jest, Vitest, pytest, JUnit |
| **Integration** | Supertest, TestClient, Spring Boot Test |
| **API** | Postman/Newman, REST Assured, httpx |
| **E2E** | Playwright, Cypress, Selenium |
| **Security** | OWASP ZAP, Burp Suite, sqlmap |
| **Performance** | k6, JMeter, Gatling, Locust |
| **Accessibility** | axe DevTools, WAVE, Lighthouse |

## License

MIT License

## Author

Created with Claude Code skill-wizard.
