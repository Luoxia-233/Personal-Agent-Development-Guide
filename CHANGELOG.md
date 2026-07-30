# 变更日志

## v0.3 — 权限模型重构与一致化

### 修改

- 权限分级从"允许/禁止"改为"自动执行/方案确认/高风险授权"三级语义
- `git add` 约束为仅限明确指定文件
- `git push` 禁止默认推送保护分支
- 架构约束"底层引擎通过接口暴露"改为条件性接口暴露（与 YAGNI 一致）
- 架构约束"模块间通信优先事件驱动"改为条件性事件驱动

### 新增

- 安全与环境保护原则（最小权限、Git 安全、文件系统安全、敏感信息、依赖与环境安全、数据恢复原则）
- 本地环境原则补充"优先检查现有环境，避免重复安装"
- CHANGELOG.md

---

## v0.2 — 所有权与决策体系

### 新增

- Human Ownership Principle
- 开发者决策原则
- Decision Boundary（Agent 决定如何实现，开发者决定是否及为何）
- 用户授权原则（自主行为 vs 用户指令）
- 理解边界（必须理解 vs 可以暂时不了解）
- 不要把 AI 当作第二意见
- 本地环境原则
- YAGNI 判断标准（抽象前三个自问）

### 修改

- README 新增目标与非目标章节

---

## v0.1 — 初始版本

### 新增

- AGENTS.md（Agent 角色定义、权限分级、工作流、编码约定、DoD、Git 规范）
- LEARNING_MODE.md（教学原则、输出格式、认知负荷控制）
- Learning Check（每个 Issue 理解验证）
- 学习模式优先级（用户先尝试 → Agent review）
- Git 权限分级（L1/L2/L3）
- Code Review Checklist
- ARCHITECTURE_TEMPLATE.md
- ADR_TEMPLATE.md（含 ADR 使用条件）
- ISSUE_WORKFLOW.md（Step 0–6）
- 各模板文件（CHANGELOG、TODO、ROADMAP、BUGS）
- GITIGNORE_TEMPLATE
