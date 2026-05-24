---
title: 已有项目操作手册
type: concept
tags: [agent-dev, 操作手册, 已有项目, 迁移]
created: 2026-05-24
updated: 2026-05-24
sources:
  - "[[sources/agent-driven-development-paradigms-and-playbooks]]"
---

# 已有项目操作手册

让 Agent 接手已有代码库的关键步骤。

> [!danger] 核心警告
> 禁止一次性全移交，失败率 > 60%。必须渐进式接手。

## 步骤

### 1. 逆向文档工程

用 Reversa 等工具提取代码库中的隐性知识。没有文档 = Agent 盲飞。

### 2. 补关键测试 + Seam Model

添加测试保护现有代码，用 Seam Model 隔离变更区域。

### 3. 写 CLAUDE.md 传达隐性知识

记录禁区、临时方案、团队约定。这是 Agent 理解代码库的关键入口。

### 4. 渐进式接手（4 周过渡）

| 周次 | 重点 | 人工参与度 |
|------|------|-----------|
| 第 1 周 | 补测试 | 高 |
| 第 2 周 | 小功能 | 中高 |
| 第 3 周 | 中功能 | 中 |
| 第 4 周起 | 独立开发 | 低 |

### 5. 禁止一次性全移交

直接接手失败率 > 60%，渐进式接手失败率 < 20%。

## 推荐工具

- Reversa + ABC（逆向文档工程）
- Claude Code（渐进式接手）
- SAM / TDD-Skills（测试驱动）

## 相关页面

- [[concepts/agent-driven-development-paradigms|三大范式详解]]
- [[concepts/agent-dev-playbook-new-project|新项目操作手册]]
- [[concepts/agent-dev-key-lessons|核心经验总结]]
- [[entities/agent-dev-tool-landscape|工具全景]]