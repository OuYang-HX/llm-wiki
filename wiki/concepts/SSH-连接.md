---
title: SSH 连接
type: concept
tags: [ssh, 远程连接]
created: 2026-05-25
updated: 2026-05-25
---

# SSH 连接

## 连接命令

```bash
ssh -p <port> <user>@<host>
ssh <alias>  # 使用 ~/.ssh/config
```

## SSH Config

```
Host <alias>
    HostName <ip-or-domain>
    User <username>
    Port <port>
    IdentityFile ~/.ssh/<key>
```

## 专有配置

### Termux 远程设备

| 项 | 值 |
|-----|-----|
| 地址 | 192.168.50.244 |
| 端口 | 8022 |
| 用户 | u0_a455 |
| 别名 | `remote-termux`（需手动添加到 config） |

```bash
ssh -p 8022 u0_a455@192.168.50.244
```

### 服务器 A

| 项 | 值 |
|-----|-----|
| 地址 | 47.117.247.155 |
| 端口 | 27182 |
| 用户 | oyhx |
| 密钥 | `~/.ssh/id_ed25519_server_a` |
| 系统 | Debian |

```bash
ssh a
```

config 配置：
```
Host a
    HostName 47.117.247.155
    User oyhx
    Port 27182
    IdentityFile ~/.ssh/id_ed25519_server_a
```
