---
type: source
title: "Wiki 环境标注规范：多平台同步的知识拆分"
slug: wiki-env-scoping
status: insight
created: 2026-05-24
updated: 2026-05-24
category: architecture
---
# Wiki 环境标注规范：多平台同步的知识拆分
在 wiki 中引入了环境标注体系（Environment Scoping Rules），解决多平台同步时公共知识与平台专有知识的冲突问题。规则写入 WIKI_SCHEMA.md：1) frontmatter `env` 字段标注环境（shared/termux/macos/linux/windows）；2) 同一主题跨平台有差异时拆为 shared 概念页 + 若干环境专有页；3) 混合内容用 callout 隔离。实践：Pi-Agent 使用习惯为 shared，安装配置拆出 Termux 专有页。
*Category: architecture*
---
*Captured: 2026-05-24*
## Related
_Add links to related pages._