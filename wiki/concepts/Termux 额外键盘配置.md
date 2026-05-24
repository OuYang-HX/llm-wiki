---
title: Termux 额外键盘配置
type: concept
env: termux
tags: [termux, keyboard, 配置]
created: 2026-05-24
updated: 2026-05-24
relates: "[[Pi-Agent安装配置（Termux）]]"
---

# Termux 额外键盘配置

放置位置: `~/.termux/termux.properties`

修改后运行 `termux-reload-settings` 生效。

## 配置

```
extra-keys = [[ \
  {key: '/', popup: '|'}, \
  {key: '-', popup: '_'}, \
  QUOTE, \
  {key: HOME, display: 首}, \
  UP, \
  {key: END, display: 尾}, \
  {key: '{', popup: '}'}, \
  {key: '(', popup: ')'}, \
  KEYBOARD \
], [ \
  {key: TAB, popup: {macro: ":wq\n", display: wq}}, \
  {key: CTRL, popup: {macro: ":w\n", display: w}}, \
  ALT, \
  LEFT, \
  DOWN, \
  RIGHT, \
  ESC, \
  {key: '~', popup: '$'}, \
  {key: ':', popup: ';'} \
], [ \
  {macro: "CTRL g", display: 编辑}, \
  {macro: "CTRL b T", display: 命名, popup: {macro: "CTRL b W", display: rn-ws}}, \
  {macro: "CTRL b v", display: 分屏}, \
  {macro: "CTRL b c", display: 新建, popup: {macro: "CTRL b N", display: +ws}}, \
  {macro: "CTRL b K", display: 关闭, popup: {macro: "CTRL b D", display: 关工作区}}, \
  {key: SPACE, display: 空格}, \
  ENTER \
]]
```

## 布局说明

### 第一行 — 符号 + 导航

| 按键 | popup | 说明 |
|------|-------|------|
| `/` | `\|` | 斜杠 / 管道 |
| `-` | `_` | 短横 / 下划线 |
| `"` | — | 引号 |
| `首` | — | HOME |
| ↑ | — | 上 |
| `尾` | — | END |
| `{` | `}` | 花括号 |
| `(` | `)` | 圆括号 |
| 🎹 | — | 切换系统键盘 |

### 第二行 — 修饰键 + 方向 + vim

| 按键 | popup | 说明 |
|------|-------|------|
| TAB | `:wq` | Tab / vim 保存退出 |
| CTRL | `:w` | Ctrl / vim 保存 |
| ALT | — | Alt |
| ← ↓ → | — | 方向键 |
| ESC | — | Esc |
| `~` | `$` | 家目录 / 变量符号 |
| `:` | `;` | 冒号 / 分号 |

### 第三行 — herdr 快捷键

| 按键 | 实际按键 | popup | 说明 |
|------|----------|-------|------|
| 编辑 | Ctrl+G | — | Pi Agent 编辑器 |
| 命名 | Ctrl+B T | rn-ws (Ctrl+B W) | 重命名 tab / 重命名 workspace |
| 分屏 | Ctrl+B V | — | 垂直分屏 |
| 新建 | Ctrl+B C | +ws (Ctrl+B N) | 新建 tab / 新建 workspace |
| 关闭 | Ctrl+B K | 关工作区 (Ctrl+B D) | 关闭 pane / 关闭 workspace |
| 空格 | — | — | Space |
| 回车 | — | — | Enter |
