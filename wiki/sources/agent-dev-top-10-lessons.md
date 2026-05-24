---
type: source
title: "Agent驱动开发十大核心经验"
slug: agent-dev-top-10-lessons
status: insight
created: 2026-05-24
updated: 2026-05-24
---
# Agent驱动开发十大核心经验
## 十大核心经验

1. **CLAUDE.md/AGENTS.md 最值得投入** — 减少 50-70% 错误和返工
2. **Spec 优先于 Prompt** — SDD 吞吐量高 5-7x
3. **测试是 Agent 的工作语言** — 有测试成功率 40%→80%
4. **任务拆小** — 1-2h 原子任务成功率 > 80%，> 4h < 50%
5. **沙盒和护栏不可妥协** — 无护栏 20% 情况产生意外变更
6. **渐进式接手** — 直接接手失败率 > 60%，渐进 < 20%
7. **人类角色转变** — 从写代码到写规格和审查结果
8. **多 Agent 并行** — 10任务 30h→4h
9. **显式代码优于优雅代码** — Go 风格优于模板化 C++
10. **逆向文档工程是前提** — 没有文档 = agent 盲飞

## 工具选择决策树
- 新项目快速原型 → Bolt.new/GPT-Engineer
- 新项目生产质量 → Claude Code + SDD / Kiro
- 已有项目接手 → Reversa + ABC + Claude Code
- 全自主运行 → Agent-OS/Factory/karl
- 多agent协作 → MetaGPT/CrewAI/LangGraph
- 日常加速 → Cursor/Windsurf/Aider

## 七个常见失败模式
1. 没规格就让agent开干 2. 没测试就改代码 3. 任务太大 4. 没护栏 5. 逐行审查agent代码 6. 隐性知识没传达 7. 一次全交

详细内容见 [[Agent-Dev-Key-Lessons]]
---
*Captured: 2026-05-24*
## Related
_Add links to related pages._