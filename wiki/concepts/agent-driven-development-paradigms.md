---
title: Agent自主驱动开发三大范式
type: concept
tags: [agent-dev, paradigms, sdd, vibe-coding]
created: 2026-05-24
updated: 2026-05-24
sources:
  - "[[sources/agent-driven-development-paradigms-and-playbooks]]"
---

# Agent自主驱动开发三大范式

## 范式对比

| 范式 | 核心模式 | 人工参与 | 适用场景 |
|------|----------|----------|----------|
| **Vibe Coding** | 对话式，人工逐行审查 | 高 | 快速原型、探索性开发 |
| **Spec-Driven Development (SDD)** | 规格先行，agent 按规格实现 | 中 | 生产质量项目，吞吐量高 5-7x |
| **Autonomous Agent Dev** | 最少人工干预的独立循环 | 低 | 持续迭代、成熟项目 |

## Vibe Coding

对话驱动的开发方式，人类逐行审查 agent 输出。适合快速原型和探索性工作，但规模化困难。

## Spec-Driven Development (SDD)

规格先行：先写结构化规格（含验收标准），再让 agent 按规格实现。吞吐量比 vibe coding 高 5-7x，是生产级项目的推荐范式。

> [!important] SDD 的关键
> 规格必须有明确的验收标准，不是模糊的 prompt。验收标准是 agent 和人类的契约。

## Autonomous Agent Dev

最少人工干预的独立循环模式。Agent 自主规划、实现、测试，人类只做看门狗监控。适合成熟项目和持续迭代场景。

## 相关页面

- [[concepts/agent-dev-key-lessons|核心经验总结]]
- [[concepts/agent-dev-playbook-new-project|新项目操作手册]]
- [[concepts/agent-dev-playbook-existing-project|已有项目操作手册]]
- [[syntheses/agent-driven-development-complete-guide|完整指南]]
