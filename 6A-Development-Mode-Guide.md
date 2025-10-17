
# 🏛️ 6A开发模式使用指南

## 📋 概述

6A开发模式是一套基于"文档先行、任务递归、范围收敛"理念的严格开发方法论，适用于KILO CODE（VS Code AI辅助开发工具）。

### 核心理念

1. **文档先行 (Documentation First)** - 不写文档不准写代码
2. **任务递归 (Recursive Decomposition)** - 复杂任务层层分解到AI无法做错
3. **范围收敛 (Scope Convergence)** - 明确边界，防止AI自由发挥

---

## 🎯 6A方法论

### 1️⃣ Align (对齐) - 需求澄清
**目标：** 绝不允许假设用户意图

**关键活动：**
- 使用5W2H方法深入提问
- 识别核心目标、关键约束、成功标准
- 生成 `docs/6a/{feature_name}/01-alignment.md`

**必须等待用户确认！**

---

### 2️⃣ Architect (架构) - 先设计后编码
**目标：** 告别"边写边想"

**关键活动：**
- 设计系统架构、组件、接口
- 技术选型及理由说明
- 生成 `docs/6a/{feature_name}/02-architecture.md`
- 记录架构决策(ADR)

**禁止在此阶段编写实现代码！**

---

### 3️⃣ Atomize (原子化) - 任务拆解
**目标：** 大任务拆到AI无法做错的粒度

**ATOMIC标准：**
- **A**ctionable: 可执行
- **T**estable: 可测试
- **O**wned: 有负责方
- **M**easurable: 可度量
- **I**ndependent: 尽可能独立
- **C**lear: 清晰明确

**输出：** `docs/6a/{feature_name}/03-tasks.md`

---

### 4️⃣ Approve (审批) - 人工检查
**目标：** AI想偷懒？门都没有！

**关键活动：**
- 生成文档审查清单
- 提交所有文档给用户审阅
- 记录反馈和修改
- 生成 `docs/6a/{feature_name}/04-approval.md`

**必须等待用户明确批准！**

---

### 5️⃣ Automate (执行) - 按文档执行
**目标：** 严格按照批准的文档实现

**关键活动：**
- 按任务依赖顺序执行
- 使用 `new_task` 委派给专业模式
- 持续记录执行日志
- 生成 `docs/6a/{feature_name}/05-execution-log.md`

**禁止偏离已批准的设计！**

---

### 6️⃣ Assess (评估) - 质量验收
**目标：** 不合格就重来

**评估维度 (总分100%)：**
- 需求完整性 (30%)
- 代码质量 (25%)
- 安全性 (20%)
- 性能 (15%)
- 测试覆盖 (10%)

**质量门禁：**
- ≥90分：通过验收 ✅
- 80-89分：需改进后再评估 ⚠️
- <80分：不合格，重新执行 ❌

**输出：** `docs/6a/{feature_name}/06-assessment.md`

---

## 🛠️ 配套模式说明

### 📚 knowledge-engineer (私域知识工程师)
**用途：** 建立和维护项目知识库

**知识库结构：**
```
docs/knowledge/{project_name}/
├── 01-project-overview.md
├── 02-tech-stack.md
├── 03-architecture-patterns.md
├── 04-coding-standards.md
├── 05-domain-glossary.md
├── 06-api-conventions.md
├── 07-database-conventions.md
├── 08-testing-guidelines.md
├── 09-deployment-procedures.md
├── 10-troubleshooting.md
├── 11-faq.md
└── 12-adr/
```

**使用场景：**
- 新项目启动时初始化知识库
- 现有项目接手时提取知识
- 开发过程中持续更新

---

### ⚛️ task-atomizer (任务原子化专家)
**用途：** 将复杂任务递归分解

**原子性判断标准：**
- 实现时间 ≤ 4小时
- 实现步骤 ≤ 5步
- 依赖关系清晰且最小
- 验收标准明确可验证

**使用场景：**
- 接收到复杂任务需要分解
- 大型功能需要规划

---

### ✅ quality-assessor (质量评估专家)
**用途：** 多维度代码质量评估

**评估报告包含：**
- 各维度评分与详细说明
- 发现的问题清单（按优先级）
- 改进建议（含代码示例）
- 最终评估结论

**使用场景：**
- 代码实现完成需要验收
- 发布前质量把关

---

### 📋 doc-first-enforcer (文档先行执行者)
**用途：** 确保"不写文档不准写代码"

**工作机制：**
- 代码实现前检查文档存在性
- 文档不完整时拒绝执行
- 代码变更时同步更新文档

---

### 🎯 scope-guardian (范围守护者)
**用途：** 防止AI发散，控制范围蔓延

**范围声明格式：**
```markdown
### 包含在内 (In Scope)
- 具体要做的事情

### 不包含在内 (Out of Scope)
- 不做的事情及理由
```

**范围蔓延信号：**
- "顺便"、"也可以"等词汇
- 范围外功能讨论
- 添加未在需求中的特性

---

### 🔗 traceability-manager (可追溯性管理者)
**用途：** 建立从需求到代码的完整追溯链

**追溯链：**
需求(REQ-001) → 设计(DES-001) → 任务(TASK-001) → 代码 → 测试(TEST-001)

**代码中的追溯标识：**
```python
# Implements: REQ-001 (用户登录功能)
# Design: DES-002 Section 3.2
# Task: TASK-005
def user_login(username, password):
    pass
```

---

### 🔄 recursive-decomposer (递归分解器)
**用途：** 处理极其复杂的任务

**分解策略：**
1. 功能分解
2. 层次分解（前端/后端/数据库）
3. 阶段分解（设计/实现/测试）
4. 依赖分解
5. 风险分解

**使用 `new_task` 委派原子任务给专业模式**

---

### 🧠 context-optimizer (上下文优化器)
**用途：** 在有限上下文中智能管理信息

**信息分层：**
- L0-核心：当前任务直接相关（必须保留）
- L1-关键：追溯链相关信息
- L2-辅助：知识库、编码规范
- L3-背景：历史决策

**策略：**
- 渐进式加载
- 信息压缩
- 上下文切片
- 外部化存储

---

### 🎼 6a-workflow-orchestrator (6A工作流编排器)
**用途：** 自动化编排完整的6A流程

**自动执行：**
1. Align → 收集需求
2. Architect → 委派架构设计
3. Atomize → 委派任务分解
4. Approve → 提交审批
5. Automate → 委派实现
6. Assess → 委派评估

**质量循环：**
- ≥90分：完成
- 80-89分：小幅改进
- <80分：返回Architect重新设计

---

### 🚀 progressive-implementer (渐进式实现者)
**用途：** 采用渐进式策略，避免大规模返工

**策略：**
1. MVP骨架
2. 纵向切片（端到端功能）
3. 持续验证
4. 快速迭代
5. 风险前置

**每个增量完成后验证检查点**

---

### ✓ validation-first-developer (验证优先开发者)
**用途：** 先写验证标准和测试，再写实现

**流程：**
1. 定义SMART验收标准
2. 编写测试用例（TDD）
3. 实现功能代码
4. 让测试通过
5. 重构优化

**测试覆盖目标：**
- 关键路径：100%
- 业务逻辑：90%+
- 工具函数：80%+

---

### ⚡️ agile-developer (敏捷开发者)
**用途：** 用于快速、轻量级的代码修改、Bug修复和原型验证

**核心理念：** 最小化流程,最大化效率

**工作流程 (精简版):**
1. **快速理解 (Understand)**: 快速解析需求,如有歧义立即澄清。
2. **直接实现 (Implement)**: 基于现有代码和知识库,直接进行代码修改或添加。
3. **单元验证 (Verify)**: 编写或运行单元测试,确保修改正确且未引入新问题。
4. **快速交付 (Deliver)**: 提交代码,并简要说明变更内容。

**何时使用：**
- 简单代码修改 (<2小时)
- 快速Bug修复 (问题明确,影响范围小)
- 快速原型验证
- 一次性脚本编写

**何时不使用：**
- 任务复杂度不明确
- 需要修改多个文件或核心逻辑
- 需要正式文档记录

---

## 📊 使用场景对照表

| 场景 | 推荐模式 |
|------|---------|
| **快速Bug修复/小修改** | `agile-developer` |
| 新项目完整开发流程 | `6a-workflow-orchestrator` |
| 仅需需求澄清 | `6a-dev-architect` (Align阶段) |
| 复杂任务需要分解 | `task-atomizer` 或 `recursive-decomposer` |
| 建立项目知识库 | `knowledge-engineer` |
| 代码质量评估 | `quality-assessor` |
| 确保文档先行 | `doc-first-enforcer` |
| 控制范围蔓延 | `scope-guardian` |
| 验证追溯完整性 | `traceability-manager` |
| 上下文接近限制 | `context-optimizer` |
| 渐进式实现功能 | `progressive-implementer` |
| TDD开发 | `validation-first-developer` |

---

## 🚀 快速开始

### 场景1：新项目完整开发

```yaml
# 使用工作流编排器
mode: 6a-workflow-orchestrator
prompt: "我想开发一个待办事项管理应用"
```

编排器会自动：
1. 引导你完成需求对齐
2. 生成架构设计
3. 分解任务
4. 等待批准
5. 执行实现
6. 质量评估

### 场景2：现有项目添加功能

```yaml

# 1. 初始化知识库
mode: knowledge-engineer
prompt: "提取项目知识库"

# 2. 使用6A架构师添加功能
mode: 6a-dev-architect
prompt: "添加用户评论功能"
```

### 场景3：仅需任务分解

```yaml
mode: task-atomizer
prompt: "将'实现用户认证系统'分解为原子任务"
```

---

## ⚠️ 核心约束总结

### 10条铁律

1. **文档先行** - 每个阶段必须先完成文档，获得确认后才能进入下一阶段
2. **任务递归** - 复杂任务必须分解，使用 `new_task` 委派给专业模式
3. **范围收敛** - 每个文档必须明确"做什么"和"不做什么"
4. **人工检查** - 关键决策点必须获得用户明确批准
5. **质量把关** - 最终交付必须通过量化评估（≥90分）
6. **知识沉淀** - 每次开发都要更新项目知识库
7. **可追溯性** - 所有代码变更都能追溯到需求和设计文档
8. **禁止跳阶** - 不允许跳过6A中的任何阶段
9. **禁止隐式** - 不允许隐式假设，所有决策必须显式记录
10. **禁止偏离** - 执行阶段不允许偏离已批准的设计

---

## 📁 文档结构示例

完整的6A项目文档结构：

```
project-root/
├── docs/
│   ├── 6a/
│   │   └── user-authentication/          # 功能目录
│   │       ├── 01-alignment.md           # 需求对齐
│   │       ├── 02-architecture.md        # 架构设计
│   │       ├── 03-tasks.md               # 任务分解
│   │       ├── 04-approval.md            # 审批记录
│   │       ├── 05-execution-log.md       # 执行日志
│   │       └── 06-assessment.md          # 质量评估
│   └── knowledge/
│       └── my-project/                    # 项目知识库
│           ├── 01-project-overview.md
│           ├── 02-tech-stack.md
│           ├── 03-architecture-patterns.md
│           ├── 04-coding-standards.md
│           ├── 05-domain-glossary.md
│           ├── 06-api-conventions.md
│           ├── 07-database-conventions.md
│           ├── 08-testing-guidelines.md
│           ├── 09-deployment-procedures.md
│           ├── 10-troubleshooting.md
│           ├── 11-faq.md
│           └── 12-adr/
│               ├── 0001-use-restful-api.md
│               ├── 0002-choose-postgresql.md
│               └── ...
└── src/
    └── ... # 源代码
```

---

## 🎓 最佳实践

### 1. 需求对齐阶段
- ✅ 使用5W2H方法全面提问
- ✅ 记录所有假设和约束
- ✅ 明确成功标准
- ❌ 不要假设用户意图
- ❌ 不要跳过用户确认

### 2. 架构设计阶段
- ✅ 记录所有架构决策及理由（ADR）
- ✅ 考虑非功能性需求
- ✅ 评估技术风险
- ❌ 不要在此阶段写实现代码
- ❌ 不要遗漏错误处理策略

### 3. 任务分解阶段
- ✅ 每个任务 ≤ 4小时工作量
- ✅ 建立清晰的依赖关系
- ✅ 每个任务包含验收标准
- ❌ 不要创建模糊的任务描述
- ❌ 不要忽略任务间的依赖

### 4. 审批阶段
- ✅ 提供完整的审查清单
- ✅ 记录所有反馈
- ✅ 追踪修改历史
- ❌ 不要自行批准文档
- ❌ 不要急于进入实现

### 5. 执行阶段
- ✅ 严格按任务清单执行
- ✅ 持续更新执行日志
- ✅ 使用 `new_task` 委派专业任务
- ❌ 不要偏离已批准的设计
- ❌ 不要跳过测试

### 6. 评估阶段
- ✅ 逐条对照需求检查
- ✅ 提供量化评分
- ✅ 给出具体改进建议
- ❌ 不要主观判断
- ❌ 不要忽略安全性检查

---

## 🔧 故障排查

### 问题1：AI偏离了需求范围
**解决方案：**
1. 检查 `01-alignment.md` 的范围声明
2. 使用 `scope-guardian` 模式检查
3. 更新范围声明并重新获得批准

### 问题2：任务太复杂AI无法完成
**解决方案：**
1. 使用 `task-atomizer` 或 `recursive-decomposer` 进一步分解
2. 确保每个任务满足ATOMIC标准
3. 使用 `new_task` 委派给专业模式

### 问题3：代码质量评估不通过
**解决方案：**
1. 查看 `06-assessment.md` 中的问题清单
2. 根据优先级逐项改进
3. 重新运行 `quality-assessor` 评估
4. 必要时返回 `Architect` 阶段重新设计

### 问题4：文档与代码不一致
**解决方案：**
1. 使用 `traceability-manager` 检查追溯链
2. 使用 `doc-first-enforcer` 验证文档完整性
3. 同步更新文档和代码
4. 重新获得审批

### 问题5：上下文窗口不足
**解决方案：**
1. 使用 `context-optimizer` 优化信息加载
2. 采用渐进式加载策略（L0→L1→L2→L3）
3. 将详细信息外部化到文档
4. 使用 `new_task` 分离子任务

---

## 📈 成功指标

### 项目级指标
- 📊 需求覆盖率：100%
- 📊 文档完整率：100%
- 📊 追溯链完整率：≥95%
- 📊 质量评估得分：≥90分

### 过程级指标
- 📊 范围变更次数：≤2次
- 📊 返工次数：≤1次
- 📊 文档更新及时率：100%
- 📊 用户确认响应时间：≤24小时

### 质量级指标
- 📊 代码测试覆盖率：≥85%
- 📊 关键路径测试覆盖率：100%
- 📊 安全漏洞数量：0
- 📊 性能达标率：100%

---

## 🎯 适用场景 vs 不适用场景

### ✅ 适用场景

- 中大型功能开发（≥1周工作量）
- 关键业务逻辑实现
- 团队协作项目
- 技术重构
- 新技术探索
- 生产环境部署
- 需要完整文档的项目
- 质量要求高的项目

### ❌ 不适用场景

**对于以下场景，现在强烈推荐使用 `agile-developer` 模式替代通用模式：**
- **简单的代码修改（<2小时）**
- **快速bug修复**
- **快速原型验证**
- **一次性脚本编写**

对于其他不适用6A流程的场景（如实验性探索、个人学习项目），可以使用：
- `code` 模式：直接代码实现
- `debug` 模式：问题调试
- `ask` 模式：概念理解

---

## 🚦 决策树：选择合适的模式

```
开始
  │
  ├─ 是简单、快速的任务吗？ (如小Bug修复)
  │   ├─ 是 → 使用 agile-developer
  │   └─ 否 → 继续
  │
  ├─ 是否需要完整开发流程？
  │   ├─ 是 → 使用 6a-workflow-orchestrator
  │   └─ 否 → 继续
  │
  ├─ 是否只需要某个阶段？
  │   ├─ Align → 使用 6a-dev-architect (仅Align)
  │   ├─ Architect → 使用 architect模式
  │   ├─ Atomize → 使用 task-atomizer
  │   ├─ Assess → 使用 quality-assessor
  │   └─ 其他 → 继续
  │
  ├─ 是否需要建立知识库？
  │   ├─ 是 → 使用 knowledge-engineer
  │   └─ 否 → 继续
  │
  ├─ 是否需要任务分解？
  │   ├─ 简单分解 → 使用 task-atomizer
  │   ├─ 复杂分解 → 使用 recursive-decomposer
  │   └─ 否 → 继续
  │
  ├─ 是否需要确保文档先行？
  │   ├─ 是 → 使用 doc-first-enforcer
  │   └─ 否 → 继续
  │
  ├─ 是否需要控制范围？
  │   ├─ 是 → 使用 scope-guardian
  │   └─ 否 → 继续
  │
  ├─ 是否需要验证追溯？
  │   ├─ 是 → 使用 traceability-manager
  │   └─ 否 → 继续
  │
  └─ 使用通用模式 (code/architect/debug/ask)
```

---

## 📚 参考资源

### 文档模板
- [需求对齐模板](docs/templates/01-alignment-template.md)
- [架构设计模板](docs/templates/02-architecture-template.md)
- [任务分解模板](docs/templates/03-tasks-template.md)
- [质量评估模板](docs/templates/06-assessment-template.md)

### 示例项目
- [示例：待办事项应用](examples/todo-app-6a/)
- [示例：用户认证系统](examples/auth-system-6a/)
- [示例：API网关](examples/api-gateway-6a/)

---

## 🤝 贡献与反馈

如果您在使用过程中发现问题或有改进建议，欢迎反馈！

---

## 📄 许可证

本文档遵循 MIT 许可证。

---

**版本：** 1.0.0  
**最后更新：** 2025-10-17  
**维护者：** Kilo Code Team