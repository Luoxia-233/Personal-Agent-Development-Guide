# Personal Agent Development Guide

一套独立于具体项目的 AI 辅助开发规范。可复制到任何新项目中直接使用。

## 目标

本项目的目标不是最大化 AI 自动开发能力。

而是在保持开发效率的同时，使开发者始终拥有：

- 项目理解能力
- 架构决策能力
- 长期维护能力

## 目录

| 文件 | 说明 |
|------|------|
| `AGENTS.md` | Agent 权限分级、Git 权限、角色定义、工作流、编码约定、DoD |
| `LEARNING_MODE.md` | 教学原则、输出格式、Learning Check、学习模式优先级、认知负荷控制 |
| `ISSUE_WORKFLOW.md` | Issue 开发步骤 (Step 0–6) |
| `ARCHITECTURE_TEMPLATE.md` | 架构文档模板 |
| `ROADMAP_TEMPLATE.md` | 路线图模板 |
| `TODO_TEMPLATE.md` | 待办事项模板 |
| `CHANGELOG_TEMPLATE.md` | 变更日志模板 |
| `CHANGELOG.md` | 项目自身变更日志 |
| `BUGS_TEMPLATE.md` | Bug 追踪模板 |
| `GITIGNORE_TEMPLATE` | .gitignore 模板 |
| `docs/adr/ADR_TEMPLATE.md` | 架构决策记录模板 |
| `docs/issues/ISSUE_TEMPLATE.md` | Issue 模板 |
| `docs/agent/ISSUE_WORKFLOW.md` | Issue 工作流详细说明 |
| `docs/devlog/TEMPLATE.md` | 开发日志模板 |

## 使用方式

新项目启动时，将本目录下的模板文件复制到项目中：

```bash
cp AGENTS.md <new-project>/
cp LEARNING_MODE.md <new-project>/docs/agent/
cp docs/issues/ISSUE_TEMPLATE.md <new-project>/docs/issues/
# ...
```

然后根据项目实际情况填写模板中的占位内容。

## 设计原则

- 文档服务于开发，不为完善而创建文档
- 模板保留结构，业务内容由项目自行填写
- 所有规范均经过实际项目验证（Horizon Radio v0.1）

## 非目标

本项目不是：

- 自动生成完整软件的框架
- 替代软件工程知识的教程
- 通用 AI Agent 开发框架
- 企业级工程管理模板

它是一套帮助个人开发者在 AI 辅助开发过程中保持项目理解、决策能力和长期维护能力的约束模板。

## 适用范围

适用于：

- 个人开发项目
- 学习型项目
- 小规模应用开发

不适用于：

- 企业级权限管理
- 高安全要求系统
- 团队大型协作流程
