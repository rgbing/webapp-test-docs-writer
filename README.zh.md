# webapp-test-docs-writer

Claude Code 的 Web 服务测试文档编写技能。

[![English](https://img.shields.io/badge/lang-English-blue.svg)](README.md)
[![Korean](https://img.shields.io/badge/lang-한글-blue.svg)](README.ko.md)
[![Chinese](https://img.shields.io/badge/lang-中文-red.svg)](README.zh.md)

## 概述

此技能为 Web 服务验证生成测试场景和测试用例。它支持 7 种测试类型，并根据用户的语言输出三语（英文/韩文/中文）文档。

## 安装

### 选项 1：符号链接（开发）

```bash
# 克隆仓库
git clone https://github.com/greeun/webapp-test-docs-writer.git

# 创建符号链接到 Claude Code 技能目录
ln -s $(pwd)/webapp-test-docs-writer ~/.claude/skills/webapp-test-docs-writer
```

### 选项 2：从 .skill 包安装

```bash
# 复制 .skill 文件并解压
cp webapp-test-docs-writer.skill ~/.claude/skills/
cd ~/.claude/skills/
unzip webapp-test-docs-writer.skill -d webapp-test-docs-writer
rm webapp-test-docs-writer.skill
```

## 使用方法

### 触发关键词

| 语言 | 关键词 |
|------|--------|
| **英文** | "test case", "test scenario", "write tests", "QA documentation" |
| **韩文** | "테스트 케이스 작성", "테스트 시나리오", "QA 문서" |
| **中文** | "测试用例", "测试场景", "测试文档", "编写测试", "测试用例编写" |

### 示例提示

```
"为登录功能编写测试用例"
"创建用户注册的 API 测试场景"
"生成结账流程的 E2E 测试用例"
"为认证功能编写安全测试用例"
```

## 测试类型

| 类型 | 用途 | 指南 |
|------|------|------|
| **单元测试** | 单个函数/模块验证 | `references/unit/guide.md` |
| **集成测试** | 组件交互验证 | `references/integration/guide.md` |
| **API 测试** | REST/GraphQL 端点验证 | `references/api/guide.md` |
| **E2E 测试** | 完整用户流程验证 | `references/e2e/guide.md` |
| **安全测试** | 安全漏洞验证 | `references/security/guide.md` |
| **性能测试** | 性能/负载验证 | `references/performance/guide.md` |
| **无障碍测试** | WCAG 合规性验证 | `references/accessibility/guide.md` |

## 工作流程

```
1. 分析输入 → 2. 选择测试类型 → 3. 推导场景 → 4. 编写用例 → 5. 审查
```

### 步骤 1：分析输入

技能分析以下来源：
- 功能规范
- API 规范（OpenAPI/Swagger）
- 源代码分析

### 步骤 2：选择测试类型

根据被测试的功能选择适当的测试类型。

### 步骤 3：推导场景

从 4 个角度推导场景：
1. **正常路径** - 预期的正常行为
2. **替代路径** - 通过不同路径成功
3. **异常路径** - 错误/失败案例
4. **边界值** - 最小/最大/边缘条件

### 步骤 4：编写用例

每个测试用例包括：
- ID（例如：TC-API-001）
- 标题
- 前置条件
- 测试步骤
- 预期结果
- 优先级
- 测试数据
- 自动化可行性

### 步骤 5：审查

检查清单：
- [ ] 100% 需求覆盖
- [ ] 包含正面和负面案例
- [ ] 包含边界测试
- [ ] 测试数据清晰
- [ ] 步骤可复现
- [ ] 预期结果可验证

## 输出格式

### 交付物

| # | 文档 | 格式 | 描述 |
|---|------|------|------|
| 1 | 测试场景文档 | Markdown | 带覆盖率的场景列表 |
| 2 | 测试用例文档 | Markdown 表格 | 详细测试步骤 |
| 3 | 覆盖率矩阵 | Markdown 表格 | 需求-场景-用例映射 |

### 场景 vs 测试用例

| 标准 | 场景 | 测试用例 |
|------|------|----------|
| **层级** | 高层（测试什么） | 低层（如何测试） |
| **视角** | 业务/用户 | 技术/执行者 |
| **细节** | 概述 | 具体步骤 |
| **关系** | 1 个场景 = N 个用例 | N 个用例 ⊂ 1 个场景 |

### ID 命名规范

```
场景：SC-[功能]-[序号]
示例：SC-LOGIN-001, SC-PAYMENT-003

测试用例：TC-[类型]-[序号] 或 TC-[功能]-[序号]
示例：TC-API-001, TC-E2E-015, TC-LOGIN-007

类型代码：
- UNIT: 单元测试
- INT: 集成测试
- API: API 测试
- E2E: E2E 测试
- SEC: 安全测试
- PERF: 性能测试
- A11Y: 无障碍测试
```

### 优先级级别

| 优先级 | 标准 | 示例 |
|--------|------|------|
| **关键** | 核心业务，失败时服务不可用 | 登录、支付 |
| **高** | 主要功能，显著的 UX 影响 | 搜索、订单 |
| **中** | 支持功能，存在替代方案 | 筛选、排序 |
| **低** | 附加功能，影响最小 | UI 增强 |

## 示例输出

### 测试场景文档

```markdown
# 登录功能测试场景

## 概述
| 项目 | 内容 |
|------|------|
| **测试目标** | 用户认证系统 |
| **测试范围** | 登录、社交登录、账户锁定 |
| **测试类型** | API、E2E |

## 场景列表

| ID | 场景 | 流程类型 | 优先级 | 用例数 |
|----|------|----------|--------|--------|
| SC-LOGIN-001 | 使用有效凭据登录 | 正常路径 | 关键 | 3 |
| SC-LOGIN-002 | 使用无效凭据登录失败 | 异常路径 | 高 | 4 |
```

### 测试用例文档

```markdown
## TC-API-001: 邮箱 + 密码正常登录

| 项目 | 内容 |
|------|------|
| **优先级** | 关键 |
| **前置条件** | - 有效账户存在<br>- 已登出状态 |
| **测试数据** | `{"email": "test@example.com", "password": "Pass123!"}` |

### 测试步骤

| # | 步骤 | 预期结果 |
|---|------|----------|
| 1 | 调用 POST /api/auth/login | 200 OK |
| 2 | 检查响应体 | 包含 accessToken |

### 元信息
- 自动化：可行（Jest + Supertest）
- 相关需求：REQ-AUTH-001
```

## 文件结构

```
webapp-test-docs-writer/
├── SKILL.md                          # 主技能定义
├── README.md                         # 此文件（英文）
├── README.ko.md                      # 韩文文档
├── README.zh.md                      # 中文文档
└── references/
    ├── templates.md                  # 通用模板
    ├── unit/guide.md                 # 单元测试指南
    ├── integration/guide.md          # 集成测试指南
    ├── api/guide.md                  # API 测试指南
    ├── e2e/guide.md                  # E2E 测试指南
    ├── security/guide.md             # 安全测试指南
    ├── performance/guide.md          # 性能测试指南
    └── accessibility/guide.md        # 无障碍测试指南
```

## 自动化工具参考

| 测试类型 | 工具 |
|----------|------|
| **单元测试** | Jest, Vitest, pytest, JUnit |
| **集成测试** | Supertest, TestClient, Spring Boot Test |
| **API 测试** | Postman/Newman, REST Assured, httpx |
| **E2E 测试** | Playwright, Cypress, Selenium |
| **安全测试** | OWASP ZAP, Burp Suite, sqlmap |
| **性能测试** | k6, JMeter, Gatling, Locust |
| **无障碍测试** | axe DevTools, WAVE, Lighthouse |

## 许可证

MIT 许可证

## 作者

使用 Claude Code skill-wizard 创建。
