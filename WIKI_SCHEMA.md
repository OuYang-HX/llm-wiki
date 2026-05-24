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
| **File naming** | Kebab-case: `my-page-name.md`. No spaces, no Chinese characters in filenames. Display titles (in frontmatter `title`) may use any language. |
| **Folder structure** | Keep the existing `wiki/{sources,entities,concepts,syntheses,requirements,analyses}/` layer. Obsidian picks this up as folder-based navigation. |
| **No HTML** | Avoid inline HTML. Use Markdown tables, callouts, and wikilinks instead. |
| **Line width** | Soft wrap — no hard line breaks at 80 chars. Obsidian handles wrapping natively. |

When the extension or model generates/updates wiki pages, it **MUST** apply these rules automatically. No post-processing step should be needed to make the vault Obsidian-compatible.

## Ownership Rules

| Path | Owner | Rule |
|------|-------|------|
| raw/** | extension | immutable after capture |
| wiki/** | model + user | editable knowledge pages |
| meta/* | extension | auto-generated |
| . | human + explicit request | operating rules |