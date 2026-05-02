# Test Writer 技能安装报告

## 📋 执行摘要

| 项目 | 详情 |
|------|------|
| **技能名称** | webapp-test-docs-writer |
| **描述** | Web Service Test Documentation Writer - Write test scenarios and test cases for web service verification |
| **版本** | 1.0.0 |
| **来源** | https://github.com/greeun/webapp-test-docs-writer |
| **作者** | greeun |
| **许可证** | MIT License |
| **安装时间** | 2026-05-02 01:33 |
| **状态** | ✅ 已安装并启用 |
| **安装位置** | `/home/iijadmin/.hermes/skills/test-writer/` |

## 🎯 技能概述

**Webapp Test Docs Writer** 是一个专业的测试文档编写技能，用于生成 Web 服务验证的测试场景和测试用例。

### 核心特性

1. ✅ **7 种测试类型支持** - Unit, Integration, API, E2E, Security, Performance, Accessibility
2. ✅ **双语支持** - 英语和韩语自动检测和响应
3. ✅ **完整的工作流** - 分析 → 选择类型 → 推导场景 → 编写用例 → 审查
4. ✅ **详细的指南** - 每种测试类型都有专门的指南文档
5. ✅ **模板化输出** - 标准化的测试场景和测试用例格式
6. ✅ **中重复检查** - 强制性去重策略，避免重复测试
7. ✅ **自动化友好** - 标记自动化可行性，支持主流测试工具

### 语言支持

- **English** → English output
- **한글** → 한글 출력

## 📦 安装内容

### 文件结构

```
~/.hermes/skills/test-writer/
├── SKILL.md                      # 主技能文档 (7.8 KB, 154 行)
├── README.md                     # 英文文档 (6.9 KB, 238 行)
├── README.ko.md                  # 韩语文档 (7.4 KB)
├── .gitignore                    # Git 忽略文件
└── references/                   # 参考文档目录
    ├── templates.md              # 公共模板 (8.9 KB, 192 行)
    ├── unit/guide.md             # 单元测试指南
    ├── integration/guide.md      # 集成测试指南
    ├── api/guide.md              # API 测试指南
    ├── e2e/guide.md              # E2E 测试指南
    ├── security/guide.md         # 安全测试指南
    ├── performance/guide.md      # 性能测试指南
    └── accessibility/guide.md    # 可访问性测试指南
```

### 文件统计

| 类型 | 数量 | 总大小 |
|------|------|--------|
| **主文档** | 1 | 7.8 KB |
| **README 文件** | 2 | 14.3 KB |
| **模板文档** | 1 | 8.9 KB |
| **测试指南** | 7 | ~21 KB |
| **配置文件** | 1 | 8 B |
| **总计** | **12** | **~52 KB** |

## 🚀 7 种测试类型

### 1. Unit (单元测试)

**目的**: 验证单个函数/模块

**测试目标**:
- 纯函数逻辑
- 边界条件
- 异常处理
- 输入验证

**指南**: `references/unit/guide.md`

---

### 2. Integration (集成测试)

**目的**: 验证组件间交互

**测试目标**:
- 数据库集成
- 外部 API 调用
- 消息队列
- 缓存交互

**指南**: `references/integration/guide.md`

---

### 3. API (API 测试)

**目的**: 验证 REST/GraphQL 端点

**测试目标**:
- HTTP 方法 (GET, POST, PUT, DELETE, PATCH)
- 请求参数 (path, query, body, header)
- 响应 (status code, body, header)
- 认证/授权
- 错误响应

**指南**: `references/api/guide.md`

---

### 4. E2E (端到端测试)

**目的**: 验证完整的用户流程

**测试目标**:
- 用户注册到登录
- 购物车到结账
- 完整业务流程
- 跨页面导航

**指南**: `references/e2e/guide.md`

---

### 5. Security (安全测试)

**目的**: 验证安全漏洞

**测试目标**:
- 认证绕过
- 授权检查
- SQL 注入
- XSS 攻击
- CSRF 保护

**指南**: `references/security/guide.md`

---

### 6. Performance (性能测试)

**目的**: 验证性能/负载

**测试目标**:
- 响应时间
- 并发用户
- 吞吐量
- 资源使用

**指南**: `references/performance/guide.md`

---

### 7. Accessibility (可访问性测试)

**目的**: 验证 WCAG 合规性

**测试目标**:
- 键盘导航
- 屏幕阅读器
- 颜色对比度
- ARIA 标签

**指南**: `references/accessibility/guide.md`

## 🔄 5 步工作流

### Step 0: 中重复检查 (MANDATORY) / Dedup Check (必需)

在编写任何测试场景或用例之前，必须执行以下检查：

1. **读取去重策略**: 如果 `docs/testing/TEST_DEDUP_POLICY.md` 存在，读取并执行
2. **搜索现有测试**: `grep -r "目标_端点_或_函数" tests/ -l`
3. **层级所有权确认**: 每个项目只属于一个层级
   - 纯函数 → unit
   - API 端点 → api
   - 浏览器流程 → e2e
   - OWASP → security
   - Auth 401/403 → 每个功能的 api 文件（禁止批量安全文件）
4. **发现现有文件**: 添加 TC 到该文件（禁止创建新文件）
5. **禁止模式**:
   - 没有真实断言的占位符 TC
   - 跨层级重复 TC
   - 未实现功能的 TC
   - 捆绑单独端点的聚合文件

---

### Step 1: 分析输入 / Analyze Input

| 来源 | 确认事项 |
|------|----------|
| **功能规格** | 需求、用户故事、验收条件 |
| **API 规格** | 端点、请求/响应模式、状态码 |
| **代码** | 业务逻辑、分支条件、异常处理 |

---

### Step 2: 选择测试类型 / Select Test Type

根据被测试的功能选择适当的测试类型。

---

### Step 3: 推导场景 / Derive Scenarios

从以下角度为每个功能推导场景：

1. **Happy Path (正常流程)** - 预期行为
2. **Alternative (替代流程)** - 通过不同路径成功
3. **Exception (异常流程)** - 错误/失败案例
4. **Boundary (边界值)** - 最小/最大/边界条件

---

### Step 4: 编写用例 / Write Cases

使用 `references/templates.md` 中的模板。

**必填字段**:

| 字段 | 说明 |
|------|------|
| ID | 唯一标识符 (例如: TC-API-001) |
| 标题 | 清晰的测试目的 |
| 前提条件 | 测试前所需状态 |
| 测试步骤 | 顺序执行步骤 |
| 预期结果 | 每个步骤的预期结果 |
| 优先级 | Critical / High / Medium / Low |
| 测试数据 | 输入数据和示例 |
| 自动化可能性 | 自动化可行性 |

---

### Step 5: 审查清单 / Review Checklist

- [ ] 100% 需求覆盖率
- [ ] 包含正负案例
- [ ] 包含边界测试
- [ ] 测试数据清晰
- [ ] 步骤可重现
- [ ] 预期结果可验证

## 📝 输出格式

### 场景文档

```markdown
# [功能名] 测试场景

## 概述
| 项目 | 内容 |
|------|------|
| 目标 | [测试目标] |
| 范围 | [测试范围] |
| 测试类型 | [Unit/Integration/API/E2E/Security/Performance/Accessibility] |

## 场景列表

| ID | 场景 | 类型 | 优先级 |
|----|------|------|--------|
| SC-001 | [描述] | Happy Path | High |
```

### 测试用例文档

```markdown
## TC-[TYPE]-[NNN]: [测试标题]

| 项目 | 内容 |
|------|------|
| **优先级** | High |
| **前提条件** | - 条件 1<br>- 条件 2 |
| **测试数据** | `{"key": "value"}` |

### 测试步骤

| # | 步骤 | 预期结果 |
|---|------|----------|
| 1 | [操作] | [结果] |
| 2 | [操作] | [结果] |

### 元信息
- 自动化: 可能 / 不可能
- 相关需求: REQ-001
- 备注: [附加信息]
```

## 🎯 触发关键词

| 语言 | 关键词 |
|------|--------|
| **English** | "test case", "test scenario", "write tests", "QA documentation" |
| **Korean** | "테스트 케이스 작성", "테스트 시나리오", "QA 문서" |

## 📚 自动化工具参考

| 测试类型 | 工具 |
|----------|------|
| **Unit** | Jest, Vitest, pytest, JUnit |
| **Integration** | Supertest, TestClient, Spring Boot Test |
| **API** | Postman/Newman, REST Assured, httpx |
| **E2E** | Playwright, Cypress, Selenium |
| **Security** | OWASP ZAP, Burp Suite, sqlmap |
| **Performance** | k6, JMeter, Gatling, Locust |
| **Accessibility** | axe DevTools, WAVE, Lighthouse |

## ✅ 安装验证

### 安装清单

| 检查项 | 状态 | 详情 |
|--------|------|------|
| 技能目录创建 | ✅ 通过 | `/home/iijadmin/.hermes/skills/test-writer/` 存在 |
| SKILL.md 创建 | ✅ 通过 | 7,795 字节 (154 行) |
| README.md 创建 | ✅ 通过 | 6,852 字节 (238 行) |
| README.ko.md 创建 | ✅ 通过 | 7,400 字节 |
| references 目录创建 | ✅ 通过 | 包含 7 个测试指南 |
| templates.md 创建 | ✅ 通过 | 8,896 字节 (192 行) |
| YAML frontmatter | ✅ 通过 | 所有必需字段存在 |
| 技能加载 | ✅ 通过 | skill_view 成功加载 |
| 技能列表 | ✅ 通过 | 出现在 hermes skills list |
| 技能启用 | ✅ 通过 | 状态为 enabled |

### 功能验证

| 功能 | 状态 | 说明 |
|------|------|------|
| 7 种测试类型指南 | ✅ 通过 | 所有 guide.md 文件存在 |
| 公共模板 | ✅ 通过 | templates.md 完整 |
| 双语文档 | ✅ 通过 | 英语和韩语 README |
| YAML frontmatter | ✅ 通过 | name, description 完整 |
| 触发关键词 | ✅ 通过 | 英语和韩语关键词定义 |

## 📊 技能特性总结

| 特性 | 描述 | 状态 |
|------|------|------|
| **多语言支持** | 英语和韩语 | ✅ 完整 |
| **7 种测试类型** | Unit, Integration, API, E2E, Security, Performance, Accessibility | ✅ 完整 |
| **详细指南** | 每种测试类型都有专门指南 | ✅ 完整 |
| **模板化输出** | 标准化格式 | ✅ 完整 |
| **去重策略** | 强制性检查 | ✅ 完整 |
| **5 步工作流** | 清晰的流程 | ✅ 完整 |
| **自动化标记** | 标记自动化可行性 | ✅ 完整 |
| **优先级系统** | Critical/High/Medium/Low | ✅ 完整 |

## 🎯 快速开始

### 英语示例

```
"Write test cases for the login feature"
"Create API test scenarios for user registration"
"Generate E2E test cases for checkout flow"
"Write security test cases for authentication"
```

### 韩语示例

```
"로그인 기능에 대한 테스트 케이스 작성"
"사용자 등록 API 테스트 시나리오 생성"
"결제 플로우 E2E 테스트 케이스 생성"
"인증 보안 테스트 케이스 작성"
```

## 📈 与其他技能的集成

### 相关技能

- **test-driven-development** - TDD 流程
- **subagent-driven-development** - 子代理驱动开发
- **systematic-debugging** - 系统化调试
- **requesting-code-review** - 代码审查

### 工作流集成

1. 使用 **writing-plans** 编写开发计划
2. 使用 **subagent-driven-development** 实现功能
3. 使用 **test-writer** 编写测试文档
4. 使用 **test-driven-development** 遵循 TDD
5. 使用 **requesting-code-review** 进行代码审查

## ⚠️ 使用限制

### 必须遵守的规则

1. ✅ **强制性去重检查** - 编写测试前必须检查现有测试
2. ✅ **层级所有权** - 每个项目只属于一个测试层级
3. ✅ **禁止占位符** - 不允许没有真实断言的测试用例
4. ✅ **禁止跨层级重复** - 不允许在多个层级重复相同测试
5. ✅ **禁止未实现功能** - 不允许为未实现的功能编写测试
6. ✅ **禁止聚合文件** - 不允许将单独端点捆绑到聚合文件

## 📄 示例输出

### 场景示例

```markdown
# 登录功能测试场景

## 概述
| 项目 | 内容 |
|------|------|
| **测试目标** | 用户认证系统 |
| **测试范围** | 登录、社交登录、账户锁定 |
| **测试类型** | API, E2E |

## 场景列表

| ID | 场景 | 流程类型 | 优先级 | 用例数 |
|----|------|----------|--------|--------|
| SC-LOGIN-001 | 使用有效凭据登录 | Happy Path | Critical | 3 |
| SC-LOGIN-002 | 使用无效凭据登录失败 | Exception | High | 4 |
```

### 测试用例示例

```markdown
## TC-API-001: 邮箱 + 密码正常登录

| 项目 | 内容 |
|------|------|
| **优先级** | Critical |
| **前提条件** | - 有效账户存在<br>- 已登出状态 |
| **测试数据** | `{"email": "test@example.com", "password": "Pass123!"}` |

### 测试步骤

| # | 步骤 | 预期结果 |
|---|------|----------|
| 1 | 调用 POST /api/auth/login | 200 OK |
| 2 | 检查响应体 | 包含 accessToken |

### 元信息
- 自动化: 可能 (Jest + Supertest)
- 相关需求: REQ-AUTH-001
```

## 🎉 结论

**Test Writer 技能已成功安装！**

这是一个功能强大、文档完善的测试文档编写技能，提供：

1. ✅ 7 种测试类型的完整支持
2. ✅ 双语支持（英语和韩语）
3. ✅ 详细的测试指南和模板
4. ✅ 强制性去重策略
5. ✅ 标准化的输出格式
6. ✅ 自动化工具参考
7. ✅ 5 步清晰工作流

**安装位置**: `/home/iijadmin/.hermes/skills/test-writer/`

**状态**: ✅ 已安装、已启用、可使用

**下一步**:
1. 阅读完整文档: `cat ~/.hermes/skills/test-writer/README.md`
2. 查看测试指南: `cat ~/.hermes/skills/test-writer/references/api/guide.md`
3. 查看模板: `cat ~/.hermes/skills/test-writer/references/templates.md`
4. 开始使用：询问 "Write test cases for [feature]"

---

**报告生成时间**: 2026-05-02 01:35
**报告生成者**: Hermes Agent
**技能版本**: 1.0.0
**来源**: https://github.com/greeun/webapp-test-docs-writer
**许可证**: MIT License
**验证状态**: ✅ 通过
