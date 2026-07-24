# AI 辅助开发指南

本文档为 AI 编程助手提供项目上下文与编码规范。

## 项目概述

> 由开发者自行填写项目的一句话描述。

---

## Agent 角色定义

Agent 承担以下角色：

- 实现助手 — 按 Issue 规范编写代码
- 设计评审 — 提出候选方案供用户决定
- 技术解释 — 按 LEARNING_MODE.md 要求逐层讲解

Agent **不替代**以下决策：

- 产品决策（做什么功能、不做功能）
- 架构决策（模块如何划分、依赖方向）
- 范围决策（当前 Issue 做多少、不做多少）

不确定时，先问再实现。

---

## Agent 权限分级

### Level 1 — 自动允许

以下操作 Agent 可直接执行，无需确认：

- 在所属模块内新增实现类
- 新增测试文件
- 修复明显的局部 Bug（如空指针判断反了）
- 补充文档（README 运行说明、API 文档等）
- 遵循现有模式的代码重构（提取方法、重命名局部变量等）

### Level 2 — 需先说明方案

以下操作 Agent 必须在执行前输出方案并等待确认：

- 添加第三方依赖（NuGet / npm / Cargo 等）
- 修改已有公共接口（interface / abstract class / public API）
- 修改或创建配置结构（settings.json / metadata.db 等）
- 移动文件或改变目录结构
- 修改模块职责
- 改变依赖方向
- 修改数据格式 / 数据模型

### Level 3 — 必须询问

以下操作 Agent 不得自主决定：

- 改变架构（例如删除中间层、合并模块）
- 替换技术栈（例如 React → Vue）
- 大规模重构（超过 5 个文件、超过 300 行）
- 删除大量代码（超过 50 行连续删除）
- 修改项目文档中的项目目标

---

## Git 权限

### Level 1 — 自动允许

- `git status`
- `git diff`
- `git add`
- 生成 Commit Message

### Level 2 — 确认后执行

- `git commit`（Agent 生成 Message → 用户确认 → Agent 执行）

### Level 3 — 禁止自动执行

- `git push`
- `git merge`
- `git rebase`
- `git reset --hard`
- `git tag`
- 删除 Branch

---

## 任务工作流

### 上下文同步协议

每个新 Session 的第一条消息建议固定为：

```
请先阅读：

README.md
ARCHITECTURE.md
AGENTS.md
docs/issues/ 目录下当前正在进行的 Issue

阅读完成后，请总结：
1. 当前项目目标
2. 当前架构
3. 当前完成进度（已完成的 Issue 及关键产出）
4. 当前正在处理的 Issue
5. 你的开发约束

确认无误后等待我的任务。
```

### 任务范围

每项任务必须明确范围：

```
允许修改：
  src/xxx/

禁止修改：
  src/yyy/
  ARCHITECTURE.md
```

### 提案模式

对于复杂任务（涉及架构决策、多个模块、新增依赖），优先使用提案模式：

1. Agent 输出设计方案（修改哪些模块、新增哪些类、数据流变化、风险）
2. 用户确认方案
3. Agent 实现

### 停机条件

任务完成后必须停止，不得：

- "顺便优化"其他模块
- 实现当前 Issue 范围外的功能
- 重构无关代码

完成后输出摘要：修改文件列表、设计决策说明、验证方式。

---

## 编码约定

### 命名规范

- 文件名: PascalCase（组件）、kebab-case（普通文件）
- 类名: PascalCase
- 函数/方法: camelCase
- 常量: UPPER_SNAKE_CASE
- 私有变量: 按语言惯例

### 代码风格

- **不添加注释**，除非代码本身无法表达意图
- 优先使用有意义的变量名和函数名代替注释
- 遵循各语言社区主流代码风格
- 一个类一个职责
- 避免 static 全局状态
- 避免提前抽象（仅有单个实现时不需要 interface）
- 避免过度设计

### 抽象引入原则

仅在以下情况引入抽象（interface / abstract class）：

- 存在至少两个实现
- 或未来版本已明确规划需要多态

### 架构约束

1. **UI 层不得包含业务逻辑**
2. **核心逻辑不得依赖 UI 实现**
3. **底层引擎通过接口暴露，不暴露实现细节**
4. **模块间通信优先事件驱动**

---

## Definition of Done

每个 Issue 完成必须满足：

- [ ] 能正常编译运行
- [ ] 无重要 Warning
- [ ] 已完成测试（如有测试框架）
- [ ] 更新 CHANGELOG.md
- [ ] 更新 TODO.md（将对应项标记完成）
- [ ] Agent 生成 Commit Message，用户确认后执行 `git commit`
- [ ] 不遗留 TODO / FIXME 注释
- [ ] 未超出 Issue 定义的范围

---

## Git 提交规范

- 一个功能完成 → 一次 Commit
- 格式: `type: description`
- Type: `feat` `fix` `refactor` `docs` `style` `test` `chore`
- 示例:
  - `feat: add local music loading`
  - `fix: playback not triggered on manual skip`
  - `refactor: extract engine interface`

---

## 项目文件结构（建议）

```
<project>/
  src/
    ui/              ← UI 组件
    core/            ← 共享类型、工具
    <domain>/        ← 领域模块（按项目调整）
  docs/
    issues/          ← Issue 文档
    adr/             ← 架构决策记录
    devlog/          ← 开发日志
    agent/           ← Agent 协作规范
    research/        ← 技术调研记录
  tests/
```

---

## 禁止事项

- 不要在 UI 中编写业务逻辑
- 不要提交编译产物和依赖包
- 不要提交包含密钥或敏感信息的文件
- 不要为了当前需求提前实现未来功能
- 不要一次修改整个项目
- 先读全文再编辑，不要猜测文件内容
