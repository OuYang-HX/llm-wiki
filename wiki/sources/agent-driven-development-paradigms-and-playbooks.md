---
title: "Agent自主驱动开发范式与操作手册"
type: source
slug: agent-driven-development-paradigms-and-playbooks
status: insight
tags: [agent-dev, paradigms, playbook, sdd]
created: 2026-05-24
updated: 2026-05-24
---

# Agent自主驱动开发范式与操作手册

## 三大范式

- **Vibe Coding**：对话式，人工逐行审查，适合快速原型
- **Spec-Driven Development (SDD)**：规格先行，agent 按规格实现，吞吐量高 5-7x
- **Autonomous Agent Dev**：最少人工干预的独立循环，适合持续迭代

## 新项目关键步骤

1. 写 CLAUDE.md / AGENTS.md（最关键！agent 的入职手册）
2. 写结构化规格（有验收标准，不是模糊 prompt）
3. 拆成原子任务（1-2小时/任务）
4. Agent 在独立 worktree 并行工作（看门狗监控）
5. 对照验收标准审查（不是逐行 code review）

## 已有项目关键步骤

1. 逆向文档工程（Reversa）提取隐性知识
2. 补关键测试 + Seam Model 保护现有代码
3. 写 CLAUDE.md 传达隐性知识（禁区、workaround、约定）
4. 渐进式接手（4周过渡：Week1补测试→Week2小功能→Week3中功能→Week4+独立）
5. 禁止一次性全移交（失败率 > 60%）

> [!tip] 核心公式
> 好规格 + 好指令文件 + 好测试 + 好CI = Agent 自动驾驶

## 关键工具

| 场景 | 推荐工具 |
|------|----------|
| 新项目入门 | Claude Code + SDD |
| 全自主 | Agent-OS, Factory, karl |
| 已有项目 | Reversa + ABC |
| 多agent | MetaGPT, CrewAI, LangGraph |
| 测试驱动 | SAM, TDD-Skills |

## 相关页面

- [[concepts/agent-driven-development-paradigms|三大范式详解]]
- [[concepts/agent-dev-playbook-new-project|新项目操作手册]]
- [[concepts/agent-dev-playbook-existing-project|已有项目操作手册]]
- [[concepts/agent-dev-key-lessons|核心经验总结]]
