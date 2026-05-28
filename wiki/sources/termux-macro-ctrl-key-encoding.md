---
type: source
title: "Termux macro CTRL 修饰键的编码行为"
slug: termux-macro-ctrl-key-encoding
status: insight
created: 2026-05-28
updated: 2026-05-28
category: devops
---
# Termux macro CTRL 修饰键的编码行为
Termux extra-keys 的 macro 中空格分隔按键序列，`CTRL` 是修饰键前缀（toggle 行为）：

- `"CTRL b K"` = Ctrl+b（prefix），然后 K（大写 = Shift+k）→ herdr 中为 `prefix+shift+k`
- `"CTRL b D"` = Ctrl+b（prefix），然后 D（大写 = Shift+d）→ herdr 中为 `prefix+shift+d`
- `"CTRL b v"` = Ctrl+b（prefix），然后 v（小写）→ herdr 中为 `prefix+v`

**常见误解**：`"CTRL b D"` 中的 D 不是 Ctrl+D，而是 Shift+D。`CTRL` 修饰键在按完 b 后就已释放。

herdr keybinding 名称对照：
| Termux macro | 发送序列 | herdr keybinding |
|---|---|---|
| CTRL b K | Ctrl+b, Shift+k | prefix+shift+k |
| CTRL b D | Ctrl+b, Shift+d | prefix+shift+d |
| CTRL b v | Ctrl+b, v | prefix+v |

相关页面：[[Termux 额外键盘配置]]
*Category: devops*
---
*Captured: 2026-05-28*
## Related
_Add links to related pages._