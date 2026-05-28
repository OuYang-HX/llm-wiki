---
type: source
title: "herdr confirm_close 仅覆盖 workspace"
slug: herdr-confirm-close-scope
status: insight
created: 2026-05-28
updated: 2026-05-28
category: devops
---
# herdr confirm_close 仅覆盖 workspace
herdr 的 `confirm_close = true`（`[ui]` 段）**只作用于关闭 workspace**，不作用于关闭 pane。关闭 pane 需要确认时，必须用 `[[keys.command]]` 绑定自定义脚本实现。

配置示例：
```toml
[keys]
close_workspace = "prefix+shift+d"  # 原生 confirm_close 覆盖

[[keys.command]]
key = "prefix+shift+k"
type = "pane"
command = "~/.local/bin/herdr-close-pane.sh"

[ui]
confirm_close = true  # 仅 workspace 关闭时弹窗
```

相关页面：[[Termux 额外键盘配置]]
*Category: devops*
---
*Captured: 2026-05-28*
## Related
_Add links to related pages._