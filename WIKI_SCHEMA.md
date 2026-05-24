# LLM Wiki Schema

## Format Rules

### Obsidian Compatibility

All wiki pages under `wiki/` **MUST** follow Obsidian-flavored Markdown conventions so the vault opens cleanly in Obsidian:

| Rule | Detail |
|------|--------|
| **Wikilinks** | Use `[[page-name]]` for internal links (not `[text](./page-name.md)`). Obsidian resolves these automatically. |
| **Frontmatter** | Each page starts with a YAML frontmatter block (`---` fenced) containing at minimum: `title`, `type`, `created`, `updated`. Extension-generated metadata goes here, not in a separate section. |
| **Tags** | Use `#tag` syntax in frontmatter or inline. Avoid nested tag paths (`#a/b/c`) unless a taxonomy is explicitly agreed upon. |
| **Callouts** | Use Obsidian callout syntax: `> [!note] Title` / `> [!warning]` / `> [!tip]` etc. Do **not** use raw HTML `<details>` or custom block syntax. |
| **Embeds** | Embed images with `![[image.png]]` and other pages with `![[page-name]]`. Avoid Markdown image syntax `![alt](path)`. |
| **文件命名** | 中文命名，用连字符分隔：`核心经验总结.md`。Obsidian 原生支持中文文件名，wikilink 直接写 `[[核心经验总结]]` 即可解析。frontmatter 的 `slug` 字段保留英文/拼音用于程序索引。 |
| **Folder structure** | Keep the existing `wiki/{sources,entities,concepts,syntheses,requirements,analyses}/` layer. Obsidian picks this up as folder-based navigation. |
| **语言** | 页面内容、标题、正文、callout、文件名均使用中文描述，仅保留行业通用专业词汇的英文原文（如 SDD、Vibe Coding、CLAUDE.md、CI 等）。frontmatter 的 `slug` 字段仍用英文/拼音用于程序索引。 |
| **No HTML** | Avoid inline HTML. Use Markdown tables, callouts, and wikilinks instead. |
| **Line width** | Soft wrap — no hard line breaks at 80 chars. Obsidian handles wrapping natively. |

当扩展或模型生成/更新 wiki 页面时，**必须**自动遵循以上规则，无需后处理即可在 Obsidian 中正常显示。

## Ownership Rules

| Path | Owner | Rule |
|------|-------|------|
| raw/** | extension | immutable after capture |
| wiki/** | model + user | editable knowledge pages |
| meta/* | extension | auto-generated |
| . | human + explicit request | operating rules |