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

## Environment Scoping Rules

此 wiki 通过 git 在多平台同步。内容必须区分**公共知识**与**环境专有知识**，避免跨平台冲突。

### 环境标签体系

每个涉及环境依赖的页面**必须**在 frontmatter 中标注 `env` 字段：

| `env` 值 | 含义 | 示例 |
|-----------|------|------|
| `shared` | 跨平台通用知识，无环境依赖 | 范式理论、通用经验、工具概念 |
| `termux` | Termux/Android 专有 | `pkg install`、`$PREFIX`、手机特有路径 |
| `macos` | macOS 专有 | Homebrew、`brew install`、darwin 特有 |
| `linux` | 桌面 Linux 专有 | apt/dnf、systemd、X11 |
| `windows` | Windows 专有 | PowerShell、WSL 路径 |

### 拆分原则

1. **默认 `shared`**：不涉及具体命令、路径、包管理器的知识，不需要标注 `env`。
2. **必须拆分**：当同一主题在不同平台有不同操作时，拆为：
   - 一个 `shared` 概念页（讲「是什么」「为什么」）
   - 若干环境专有页（讲「怎么做」），用 `> [!info] 环境` callout 链接回概念页
3. **环境专有页命名**：`{主题}（{环境}）`，如 `Pi-Agent安装配置（Termux）.md`
4. **环境专有页模板**：
   ```yaml
   ---
   title: {主题}（{环境}）
   type: concept | entity
   env: {termux|macos|linux|windows}
   relates: "[[{共享概念页}]]"
   ---
   ```
5. **内联环境标注**：当内容混合了公共和专有信息，用 callout 隔离：
   ```markdown
   > [!info] Termux 专有
   > 在 Termux 中路径为 `$PREFIX/tmp` 而非 `/tmp`
   ```

当扩展或模型生成/更新 wiki 页面时，**必须**自动遵循以上规则，无需后处理即可在 Obsidian 中正常显示。

## Ownership Rules

| Path | Owner | Rule |
|------|-------|------|
| raw/** | extension | immutable after capture |
| wiki/** | model + user | editable knowledge pages |
| meta/* | extension | auto-generated |
| . | human + explicit request | operating rules |