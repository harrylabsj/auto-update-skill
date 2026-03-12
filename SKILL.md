# Auto Update Skill

智能 Skill 更新工具 - 安全地管理 skill 更新。

## 概述

Auto Update Skill 是一个帮助用户管理 OpenClaw skill 更新的工具。它提供版本检查、备份管理和回滚功能，确保更新过程安全可靠。

## 核心理念

**安全第一**：
- 只读取本地文件，不执行危险操作
- 更新前自动备份
- 支持版本回滚
- 分级更新策略

## 功能

- **版本检查** - 查看已安装 skills 的当前版本
- **备份管理** - 更新前自动备份，支持手动备份
- **版本回滚** - 升级失败可回滚到之前版本
- **配置管理** - 黑名单、自动升级策略等
- **缓存管理** - 智能缓存避免重复检查

## 安装

```bash
clawhub install auto-update-skill
```

## 使用方法

### 检查版本

```bash
# 检查所有已安装 skills
auto-update-skill check

# 检查指定 skill
auto-update-skill check my-skill
```

### 更新 skill

```bash
# 获取更新提示（实际更新使用 clawhub）
auto-update-skill update my-skill

# 然后按提示运行
clawhub update my-skill
```

### 配置管理

```bash
# 查看配置
auto-update-skill config

# 添加黑名单（不自动检查更新）
auto-update-skill config blacklist add my-skill

# 移除黑名单
auto-update-skill config blacklist remove my-skill

# 设置自动升级策略
auto-update-skill config auto patch true
auto-update-skill config auto minor false
auto-update-skill config auto major false
```

### 备份与回滚

```bash
# 列出备份
auto-update-skill backup list

# 回滚到指定版本
auto-update-skill rollback my-skill --version 1.0.0

# 清除缓存
auto-update-skill refresh
```

## 配置说明

配置文件位置：`~/.openclaw/auto-update-skill.json`

```json
{
  "mode": "interactive",
  "cacheDuration": 86400000,
  "autoUpgrade": {
    "patch": true,
    "minor": false,
    "major": false
  },
  "remindInterval": 604800000,
  "blacklist": [],
  "quietHours": {
    "start": "22:00",
    "end": "08:00"
  }
}
```

## 更新原则

| 版本变化 | 策略 | 说明 |
|---------|------|------|
| **Patch** (1.0.1→1.0.2) | 建议升级 | Bug 修复，安全更新 |
| **Minor** (1.1→1.2) | 建议升级 | 新功能，向后兼容 |
| **Major** (1→2) | 需确认 | 重大变更，可能影响功能 |

## 安全说明

- 本工具**只读取本地文件**，不执行网络请求
- 实际更新操作通过 `clawhub` CLI 执行
- 所有备份存储在本地 `~/.openclaw/skill-backups/`
- 无敏感信息收集或传输

## 依赖

- Node.js
- OpenClaw 已安装
- clawhub CLI 已配置

## 许可证

MIT
