---
title: Pi-Agent 安装配置（Termux）
type: concept
env: termux
tags: [pi-agent, termux, android, 环境专有, 安装配置]
created: 2026-05-24
updated: 2026-05-24
relates: "[[Pi-Agent使用习惯]]"
---

# Pi-Agent 安装配置（Termux）

> [!warning] 环境专有
> 本页仅适用于 Termux/Android 环境。跨平台通用内容见 [[Pi-Agent使用习惯]]。

## 环境概览

| 项 | 值 |
|-----|-----|
| 操作系统 | Android 15 (aarch64) |
| 终端 | Termux (F-Droid) |
| Shell | bash |
| 内核 | Linux 6.6.77-android15 |
| 包管理器 | `pkg` / `apt`（Termux 仓库） |
| 前缀路径 | `$PREFIX` = `/data/data/com.termux/files/usr` |
| Home | `/data/data/com.termux/files/home` |

## Pi Agent 安装

### 依赖安装

```bash
pkg install nodejs git openssh vim
```

### Pi 安装

```bash
npm install -g @mariozechner/pi-coding-agent
```

### 扩展安装

```bash
pi install npm:gentle-pi          # SDD/OpenSpec harness
pi install npm:@zosmaai/pi-llm-wiki  # 知识库
pi install npm:pi-autoresearch     # 自主实验循环
```

## 关键配置

### WIKI_HOME

```bash
# ~/.bashrc
export WIKI_HOME="$HOME"
```

> [!info] 为什么这样设
> pi-llm-wiki 默认在 `~/.llm-wiki/.llm-wiki/` 创建内容（双层嵌套）。设置 `WIKI_HOME=$HOME` 后，wiki root 变为 `$HOME`，内容直接存在 `~/.llm-wiki/` 下，与 git 仓库扁平对齐。

### SSH 密钥

```bash
ls ~/.ssh/
# id_ed25519  id_ed25519.pub  config  authorized_keys  known_hosts
```

- 使用 ed25519 密钥连接 GitHub
- 连接验证：`ssh -T git@github.com`

### Git 配置

> [!warning] Termux 没有 .gitconfig
> Termux 默认无全局 git 配置。需要在每个仓库内 `git config --local` 设置 user.name 和 user.email。

```bash
cd <repo>
git config user.name "OuYang-HX"
git config user.email "OuYang-HX@users.noreply.github.com"
```

### 模型网关

```json
{
  "providers": {
    "gateway": {
      "baseUrl": "http://<server>:49127/v1",
      "api": "openai-completions",
      "apiKey": "<key>",
      "models": [
        { "id": "astron-code-latest", "contextWindow": 204800, "maxTokens": 65536 },
        { "id": "MiniMax-M2.7-highspeed", "contextWindow": 204800, "maxTokens": 65536 }
      ]
    }
  }
}
```

> [!danger] 密钥安全
> 网关地址和 API Key 存储在 `~/.pi/agent/models.json`，属于敏感信息，不应写入 wiki。此处仅记录结构。

## LLM Wiki 同步

| 项 | 值 |
|-----|-----|
| 本地路径 | `~/.llm-wiki/` |
| 远程仓库 | `git@github.com:OuYang-HX/llm-wiki.git` |
| 分支 | `main` |
| 同步方式 | `git pull` / `git push` |

```bash
cd ~/.llm-wiki
git pull origin main   # 拉取其他平台的更新
git add -A && git commit -m "xxx" && git push origin main  # 推送本地更新
```

## Termux 特有注意事项

### 路径差异

| 通用路径 | Termux 实际路径 |
|----------|----------------|
| `/tmp` | `$PREFIX/tmp`（已设置 `TMPDIR`） |
| `/usr/bin` | `$PREFIX/bin` |
| `/usr/lib` | `$PREFIX/lib` |
| `~` | `/data/data/com.termux/files/home` |

### 常用 .bashrc 配置

```bash
# 临时目录
export TMPDIR="$PREFIX/tmp"
export TMP="$TMPDIR"
export TEMP="$TMPDIR"

# 字体（Nerd Font 用于 TUI 图标）
export TERMUX_FONT_FAMILY="JetBrainsMonoNerdFontMono-ExtraBoldItalic"

# 编辑器
export EDITOR=vim
export VISUAL=vim

# Pi LLM Wiki
export WIKI_HOME="$HOME"
```

### 包管理差异

| 通用命令 | Termux 命令 |
|----------|------------|
| `sudo apt install X` | `pkg install X` |
| `brew install X` | `pkg install X` |
| `/etc/` 配置文件 | `$PREFIX/etc/` |

## 环境迁移备份

> 详细迁移指南见 [[SRC-2026-05-24-001]]

备份位置: `/storage/emulated/0/Download/termux-backup/`

### 备份内容 (2026-05-24)

| 类别 | 文件 | 说明 |
|------|------|------|
| 包列表 | `pkg_installed.txt` | 224 个已安装包，可批量重装 |
| Termux 配置 | `termux.properties` + `font.ttf` | 键盘布局、快捷键、JetBrains Mono 字体 |
| Shell | `bashrc` | PATH、环境变量、字体设置 |
| SSH | `ssh_config` + `ssh_id_ed25519.pub` + `ssh_authorized_keys` | 主机别名、公钥（私钥未导出） |
| Pi Agent | `pi_models.json` + `pi_auth.json` + `pi_agent_settings.json` | 模型配置、API 密钥、默认 provider |
| SDD | `pi-agents/` (11) + `pi-chains/` (3) | 完整 SDD 流程定义 |
| 扩展 | `pi-extensions/` + `pi-gentle-ai/` | llm-stats、strict-tdd |
| Herdr | `herdr_config.toml` | 终端复用器键位和 UI 配置 |
| 恢复指南 | `RESTORE_GUIDE.md` | 详细步骤 + 验证清单 |

### 快速恢复流程

```bash
# 1. 新手机安装 Termux (F-Droid) + 更新
pkg update && pkg upgrade -y

# 2. 授权存储
termux-setup-storage

# 3. 批量重装包
cp /storage/emulated/0/Download/termux-backup/pkg_installed.txt ~/
pkg install $(cat ~/pkg_installed.txt) -y

# 4. 恢复配置
cp /storage/emulated/0/Download/termux-backup/termux.properties ~/.termux/
cp /storage/emulated/0/Download/termux-backup/font.ttf ~/.termux/
cp /storage/emulated/0/Download/termux-backup/bashrc ~/.bashrc
termux-reload-settings

# 5. 恢复 SSH (私钥需手动)
mkdir -p ~/.ssh && chmod 700 ~/.ssh
cp /storage/emulated/0/Download/termux-backup/ssh_config ~/.ssh/config

# 6. 恢复 Pi Agent 配置
mkdir -p ~/.pi/agent/agents ~/.pi/agent/chains ~/.pi/agent/extensions ~/.pi/agent/gentle-ai/support
cp /storage/emulated/0/Download/termux-backup/pi_models.json ~/.pi/agent/models.json
cp /storage/emulated/0/Download/termux-backup/pi_auth.json ~/.pi/agent/auth.json
cp /storage/emulated/0/Download/termux-backup/pi_agent_settings.json ~/.pi/agent/settings.json
cp /storage/emulated/0/Download/termux-backup/pi-agents/*.md ~/.pi/agent/agents/
cp /storage/emulated/0/Download/termux-backup/pi-chains/*.md ~/.pi/agent/chains/
cp -r /storage/emulated/0/Download/termux-backup/pi-extensions/* ~/.pi/agent/extensions/
cp -r /storage/emulated/0/Download/termux-backup/pi-gentle-ai/* ~/.pi/agent/gentle-ai/

# 7. 重装 Node.js 全局包
npm install -g @earendil-works/pi-coding-agent pi-autoresearch @zosmaai/pi-llm-wiki gentle-pi

# 8. 重新认证 GitHub
gh auth login
```

### 需手动处理项

| 项目 | 原因 | 处理方式 |
|------|------|----------|
| SSH 私钥 | 安全风险 | 手动安全传输或 `ssh-keygen -t ed25519` |
| GitHub token | 令牌绑定设备 | `gh auth login` |
| Herdr 二进制 | 编译文件 | 重新安装 |
| 项目代码 | 仓库克隆 | git clone |

## 相关页面

- [[Pi-Agent使用习惯]]（公共知识）
- [[核心经验总结]]
- [[工具全景]]
- [[SRC-2026-05-24-001]]（迁移指南源文件）