# Termux 环境迁移指南

> 导出时间: 2026-05-24
> 源设备: Android 15, aarch64, kernel 6.6.77
> Termux: F-Droid 版, API 0.53.0

---

## 一、新手机初始安装

### 1. 安装 Termux (必须从 F-Droid 安装)

**不要用 Play Store 版本**，Play Store 版已过时且不维护。

- 安装 [F-Droid](https://f-droid.org/)
- 在 F-Droid 中搜索安装 **Termux**
- 同时安装 **Termux:API** (如果需要 termux-api 命令)

### 2. 首次启动 Termux

启动后等待初始化完成，然后更新系统：

```bash
pkg update && pkg upgrade -y
```

---

## 二、恢复包列表

备份中有 `pkg_installed.txt`，包含 224 个已安装包。

### 方法 A: 批量安装（推荐）

```bash
cp /storage/emulated/0/Download/termux-backup/pkg_installed.txt ~/
pkg install $(cat ~/pkg_installed.txt) -y
```

> ⚠️ 部分包可能已更名或移除，报错时记下失败的包名，跳过继续。

### 方法 B: 分组安装（更稳妥）

```bash
# 核心工具
pkg install bash coreutils curl git gh findutils fd vim openssh termux-api -y
# 开发工具链
pkg install build-essential clang cmake autoconf automake bison flex gdbm -y
# 语言运行时
pkg install openjdk-17 python nodejs-lts rust -y
# Android 工具
pkg install android-tools aapt aapt2 apksigner d8 -y
# 其他工具
pkg install dialog diffutils dos2unix ed file gawk -y
```

---

## 三、恢复配置文件

### 1. Termux 应用配置

```bash
cp /storage/emulated/0/Download/termux-backup/termux.properties ~/.termux/
cp /storage/emulated/0/Download/termux-backup/font.ttf ~/.termux/
termux-reload-settings
```

### 2. Shell 配置

```bash
cp /storage/emulated/0/Download/termux-backup/bashrc ~/.bashrc
source ~/.bashrc
```

### 3. SSH 配置

```bash
mkdir -p ~/.ssh && chmod 700 ~/.ssh
cp /storage/emulated/0/Download/termux-backup/ssh_config ~/.ssh/config
cp /storage/emulated/0/Download/termux-backup/ssh_authorized_keys ~/.ssh/authorized_keys
# ⚠️ SSH 私钥未导出（安全原因），需要手动复制或重新生成：
# 选项1: 从旧手机手动复制 id_ed25519
# 选项2: 生成新密钥: ssh-keygen -t ed25519
chmod 600 ~/.ssh/*
```

### 4. Git 配置

```bash
git config --global user.name "你的名字"
git config --global user.email "你的邮箱"
git config --global core.editor vim
```

---

## 四、恢复 Pi Agent 环境

### 1. 安装 Node.js 全局包

```bash
npm install -g @earendil-works/pi-coding-agent
npm install -g pi-autoresearch
npm install -g @zosmaai/pi-llm-wiki
npm install -g gentle-pi
npm install -g @anthropic-ai/claude-code
```

### 2. 恢复 Pi 配置

```bash
mkdir -p ~/.pi/agent/agents ~/.pi/agent/chains ~/.pi/agent/extensions ~/.pi/agent/gentle-ai/support
cp /storage/emulated/0/Download/termux-backup/pi_models.json ~/.pi/agent/models.json
cp /storage/emulated/0/Download/termux-backup/pi_auth.json ~/.pi/agent/auth.json
cp /storage/emulated/0/Download/termux-backup/pi_agent_settings.json ~/.pi/agent/settings.json
cp /storage/emulated/0/Download/termux-backup/pi_settings.json ~/.pi/settings.json
cp /storage/emulated/0/Download/termux-backup/pi-agents/*.md ~/.pi/agent/agents/
cp /storage/emulated/0/Download/termux-backup/pi-chains/*.md ~/.pi/agent/chains/
cp -r /storage/emulated/0/Download/termux-backup/pi-extensions/* ~/.pi/agent/extensions/
cp -r /storage/emulated/0/Download/termux-backup/pi-gentle-ai/* ~/.pi/agent/gentle-ai/
```

> ⚠️ `pi_auth.json` 包含 API 密钥，请确认安全后再复制。

---

## 五、恢复 Herdr (终端复用器)

```bash
mkdir -p ~/.config/herdr
cp /storage/emulated/0/Download/termux-backup/herdr_config.toml ~/.config/herdr/config.toml
# Herdr 二进制需重新安装 (pkg search herdr 或从官方获取)
```

---

## 六、恢复其他工具

```bash
# Python 包
pip install markdown-it-py rich Pygments

# ATL Skill Registry
mkdir -p ~/.atl
cp /storage/emulated/0/Download/termux-backup/skill-registry.md ~/.atl/

# LLM Wiki (可选，从旧手机复制 ~/.llm-wiki/ 目录)
```

---

## 七、Termux 存储权限

```bash
termux-setup-storage
```

---

## 八、验证清单

- [ ] `pkg list-installed | wc -l` — 包数量接近 224
- [ ] `node -v` — Node.js 可用
- [ ] `python -V` — Python 可用
- [ ] `cargo --version` — Rust 可用
- [ ] `java -version` — Java 可用
- [ ] `gh auth status` — GitHub CLI 需要重新认证
- [ ] `ssh a` — SSH 到服务器测试
- [ ] `pi` — Pi agent 可启动
- [ ] `herdr` — 终端复用器可用
- [ ] Termux 额外键盘行显示正确
- [ ] 字体显示为 JetBrains Mono Nerd Font

---

## 九、未导出项（需手动处理）

| 项目 | 原因 | 处理方式 |
|------|------|----------|
| SSH 私钥 (`id_ed25519`) | 安全风险 | 手动安全传输或重新生成 |
| GitHub token (`gh auth`) | 令牌绑定设备 | 在新手机运行 `gh auth login` |
| `~/.local/bin/herdr` | 编译二进制 | 重新安装 |
| `~/.local/bin/herdr-close-*.sh` | 脚本未导出 | 手动复制或重建 |
| `~/.opencode/` | 需检查安装方式 | 重新安装 |
| `~/AndroidGit/` | 项目代码 | git clone 重新拉取 |
| `~/CodingPlanBoard/` | 项目代码 | git clone 重新拉取 |
| `~/my-pi-extentions/` | 项目代码 | git clone 重新拉取 |
| `~/.llm-wiki/` | Wiki 数据 | 可选复制或重建 |
| `~/.tetm` | 未知大文件(2.4MB) | 检查是否需要 |
| `~/.termux_authinfo` | 认证信息 | Termux 自动生成 |

---

## 十、备份文件清单

```
termux-backup/
├── RESTORE_GUIDE.md          ← 本文件
├── pkg_installed.txt          ← 224个已安装包列表
├── bashrc                     ← Shell 配置
├── termux.properties          ← Termux 键盘/快捷键配置
├── termux.properties.bak      ← 配置备份
├── font.ttf                   ← JetBrains Mono Nerd Font
├── gitignore                  ← 全局 .gitignore
├── ssh_config                 ← SSH 主机配置
├── ssh_id_ed25519.pub         ← SSH 公钥
├── ssh_authorized_keys        ← SSH 授权密钥
├── pi_models.json             ← Pi Agent 模型配置
├── pi_auth.json               ← Pi Agent 认证密钥
├── pi_agent_settings.json     ← Pi Agent 设置
├── pi_settings.json           ← Pi 全局设置
├── herdr_config.toml          ← Herdr 终端复用器配置
├── skill-registry.md          ← ATL 技能注册表
├── claude.json                ← Claude Code 配置
├── pi-agents/                 ← SDD agent 定义 (11个)
├── pi-chains/                 ← SDD chain 定义 (3个)
├── pi-extensions/             ← Pi 扩展 (llm-stats)
└── pi-gentle-ai/              ← Gentle AI 支持 (strict-tdd)
```
