---
title: Pi-Agent 使用习惯
type: concept
tags: [pi-agent, 使用习惯, 工作流, 跨平台]
created: 2026-05-24
updated: 2026-05-24
---

# Pi-Agent 使用习惯

## 运行环境

Pi Agent 在多平台使用，环境专有配置见各平台专页：

- [[Pi-Agent安装配置（Termux）]]
- > 后续新增平台时在此补充链接

## 核心使用习惯

### 1. 模型与 Provider

| 项 | 值 |
|-----|-----|
| 默认 Provider | `gateway`（自建 OpenAI 兼容网关） |
| 默认模型 | `astron-code-latest`（Astron Code） |
| 备选模型 | `MiniMax-M2.7-highspeed` |
| Thinking Level | `medium` |
| 上下文窗口 | 204800 tokens |
| 最大输出 | 65536 tokens |

> [!info] Provider 架构
> 使用自建网关 `http://<server>:49127/v1` 统一代理多个模型，避免在客户端配置多个 API Key。网关地址和密钥属于环境专有信息，不在此页记录。

### 2. 扩展生态（三大扩展）

| 扩展 | 版本 | 用途 | 触发场景 |
|------|------|------|----------|
| **gentle-pi** | 0.3.9 | SDD/OpenSpec 流程、subagent 编排、TDD 护栏、review 保护 | 复杂功能开发、多文件变更、PR 审查 |
| **pi-llm-wiki** | 0.7.2 | 知识库管理、来源捕获、自动索引、跨平台同步 | 知识沉淀、来源归档、经验回溯 |
| **pi-autoresearch** | 1.4.0 | 自主实验循环、度量优化、keep/discard 决策 | 性能调优、参数搜索、A/B 测试 |

### 3. 工作流选择模式

根据任务复杂度选择不同工作方式：

| 任务规模 | 工作方式 | 说明 |
|----------|----------|------|
| 小改动（typo、单文件） | Inline 直接执行 | 不启动 SDD 仪式 |
| 中等任务（2-3 文件） | Simple Delegation | scout → worker → reviewer |
| 大型功能 | SDD 全流程 | init → explore → proposal → spec → design → tasks → apply → verify |
| 性能优化 | Autoresearch 循环 | 实验 → 度量 → keep/discard |
| 知识沉淀 | Wiki 流程 | capture → ingest → synthesize → retro |

### 4. Git 工作习惯

| 习惯 | 说明 |
|------|------|
| GitHub 用户 | `OuYang-HX` |
| SSH 连接 | ed25519 密钥，`git@github.com:` 协议 |
| 分支策略 | `main` 为主分支 |
| Wiki 同步 | `~/.llm-wiki/` 通过 git 与 `OuYang-HX/llm-wiki` 同步 |

### 5. 知识管理习惯

- **wiki_recall** 在每个任务开始时调用，回溯相关经验
- **wiki_retro** 在任务结束时调用，沉淀非显而易见的发现
- Wiki 内容通过 git 在多平台同步，公共知识与平台专有知识分离存储
- 中文为主要书写语言，技术术语保留英文原文

### 6. 编辑器与终端

| 项 | 值 |
|-----|-----|
| 编辑器 | vim（`EDITOR=vim`） |
| 字体 | JetBrainsMono Nerd Font |
| Shell | bash |

## Gentle-Pi Skill 清单

| Skill | 触发场景 |
|-------|----------|
| `gentle-ai` | 核心身份与 harness 纪律 |
| `branch-pr` | 创建/准备 PR |
| `chained-pr` | 大 PR 拆分、stacked PR |
| `cognitive-doc-design` | 写文档时降低认知负荷 |
| `comment-writer` | PR 评论、issue 回复 |
| `issue-creation` | 创建 GitHub issue |
| `judgment-day` | 对抗性双盲 review |
| `work-unit-commits` | 规划可审查的提交单元 |
| `release` | npm 发布流程 |
| `skill-registry` | 更新 skill 索引 |

## SDD 资产

| 类型 | 路径 | 说明 |
|------|------|------|
| Phase agents | `~/.pi/agent/agents/sdd-*.md` | 11 个阶段 agent |
| Chain 文件 | `~/.pi/agent/chains/sdd-*.chain.md` | 3 条链（full/plan/verify） |
| TDD 支持 | `~/.pi/agent/gentle-ai/support/strict-tdd*.md` | 严格 TDD 模板 |

## 相关页面

- [[Pi-Agent安装配置（Termux）]]
- [[核心经验总结]]
- [[三大范式]]
- [[工具全景]]