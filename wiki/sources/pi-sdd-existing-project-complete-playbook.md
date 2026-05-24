---
title: Pi SDD 接手现有项目操作方案
type: source
slug: pi-sdd-existing-project-complete-playbook
status: insight
tags: [agent-dev, SDD, Pi, 操作指南]
created: 2026-05-24
updated: 2026-05-24
---

# Pi SDD 接手现有项目完整操作方案

## 四阶段路线图

1. **阶段 0 安装验证**（30 分钟）：确认 Pi + Gentle AI + subagents 可用
2. **阶段 1 知识提取**（2-4 小时）：context-builder 扫描 + 手写隐性知识 + wiki 记录
3. **阶段 2 SDD 基础设施**（1-2 小时）：openspec/config.yaml + 项目 AGENTS.md + 补测试
4. **阶段 3 试运行**（2-4 小时）：sdd-onboard 小变更试水 → 验证全流程
5. **阶段 4 日常循环**：描述需求 → sdd-plan → 审查 → sdd-verify → 归档

## 关键 SDD 命令

- `sdd-onboard`：引导式走完整个 SDD 流程（推荐新手）

## 相关页面

- [[concepts/agent-dev-playbook-existing-project|已有项目操作手册]]
- [[concepts/agent-driven-development-paradigms|三大范式详解]]
- [[concepts/agent-dev-key-lessons|核心经验总结]]