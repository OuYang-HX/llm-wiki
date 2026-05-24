---
title: 新项目操作手册
type: concept
tags: [agent-dev, 操作手册, 新项目, SDD]
created: 2026-05-24
updated: 2026-05-24
sources:
  - "[[sources/agent-driven-development-paradigms-and-playbooks]]"
---

# 新项目操作手册

从零开始让 Agent 自动开发新项目的关键步骤。

## 步骤

### 1. 写 CLAUDE.md / AGENTS.md

> [!warning] 最关键的一步
> 这是 Agent 的入职手册。投入时间写好指令文件，可减少 50-70% 错误和返工。

### 2. 写结构化规格

规格必须有验收标准，不是模糊的提示词。验收标准是 Agent 和人类的契约。

### 3. 拆成原子任务

每个任务 1-2 小时。原子任务成功率 > 80%，超过 4 小时的任务成功率 < 50%。

### 4. Agent 在独立 worktree 并行工作

多个 Agent 并行，用看门狗监控进度。10 个任务可从 30 小时缩短到 4 小时。

### 5. 对照验收标准审查

审查验收标准是否满足，不是逐行代码审查。人类角色从写代码转变为写规格和审查结果。

## 推荐工具

- Claude Code + SDD（生产质量）
- Bolt.new / GPT-Engineer（快速原型）
- Kiro（IDE 集成 SDD）

## 相关页面

- [[concepts/agent-driven-development-paradigms|三大范式详解]]
- [[concepts/agent-dev-playbook-existing-project|已有项目操作手册]]
- [[concepts/agent-dev-key-lessons|核心经验总结]]
- [[entities/agent-dev-tool-landscape|工具全景]]