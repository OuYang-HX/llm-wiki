---
title: Termux 配置备份
type: concept
env: termux
tags: [termux, backup, config, github]
created: 2026-05-24
updated: 2026-05-24
relates: "[[Pi-Agent安装配置（Termux）]]"
---

# Termux 配置备份

> [!info] 仓库地址
> `git@github.com:OuYang-HX/termux-backup.git`（Private）
> 本地路径: `~/termux-backup/`

## 备份内容

仅 Termux 相关配置文件，不含包列表和安装脚本。

| 文件 | 放置位置 | 说明 |
|------|----------|------|
| `dotfiles/bashrc` | `~/.bashrc` | 环境变量、PATH、字体、编辑器 |
| `dotfiles/termux.properties` | `~/.termux/termux.properties` | 额外键盘布局（3 行，含中文标注） |
| `dotfiles/ssh-config` | `~/.ssh/config` | SSH 主机别名 |
| `dotfiles/pi-settings.json` | `~/.pi/agent/settings.json` | Pi Agent 默认 provider/model/packages |
| `dotfiles/herdr-config.toml` | `~/.config/herdr/config.toml` | herdr 终端复用器快捷键和 UI |

## 字体

JetBrainsMono Nerd Font Mono ExtraBold Italic — 下载命令见仓库 README。

## 新手机恢复

```bash
# 1. 安装 Termux (F-Droid)
# 2. pkg install git openssh
# 3. ssh-keygen -t ed25519 → 加到 GitHub
# 4. git clone git@github.com:OuYang-HX/termux-backup.git ~/termux-backup
# 5. 复制 dotfiles/ 到对应位置（见仓库 README）
# 6. 安装字体
# 7. termux-reload-settings && source ~/.bashrc
```

## ⚠️ 不在仓库中

| 项目 | 原因 |
|------|------|
| SSH 私钥 (`id_ed25519`) | 安全风险，手动传输 |
| Pi Agent API Keys | `models.json` / `auth.json` 手动填 |
| Pi Agent agents/chains/extensions | `pi install` 自动生成 |
| 其他项目仓库 | 单独 clone |

## 更新备份

修改配置后运行：

```bash
cd ~/termux-backup
cp ~/.bashrc dotfiles/bashrc
cp ~/.termux/termux.properties dotfiles/termux.properties
cp ~/.ssh/config dotfiles/ssh-config
cp ~/.pi/agent/settings.json dotfiles/pi-settings.json
cp ~/.config/herdr/config.toml dotfiles/herdr-config.toml
git add -A && git commit -m "backup: $(date +%Y-%m-%d)" && git push
```

## 相关页面

- [[Pi-Agent安装配置（Termux）]]
- [[SRC-2026-05-24-001]]
