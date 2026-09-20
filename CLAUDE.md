# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

这是 **Spotlight Workflow（探照灯式工作流引擎）** 的开发项目。包含一个主技能和五个子命令技能，共同构成一套完整的个人工作流操作系统。

**当前状态：v3.0，SKILL.md 拆分为核心指令（~9 KB 常驻加载）和 REFERENCE.md（按需读取），初始化流程简化（默认当前目录）。写作铁律已从三项扩至六项。**

## 项目结构

```
spotlight-workflow/
├── README.md              ← 功能说明（中文）
├── README_EN.md           ← 功能说明（英文）
├── SKILL.md               ← 核心指令（~9 KB，每次加载）
├── REFERENCE.md           ← 参考手册（~14 KB，按需读取）
├── CLAUDE.md              ← 本文件
├── version.md             ← 版本迭代记录
├── spotlight-init/
│   └── SKILL.md           ← /spotlight-init
├── spotlight-work/
│   └── SKILL.md           ← /spotlight-work
├── spotlight-check/
│   └── SKILL.md           ← /spotlight-check
├── spotlight-learn/
│   └── SKILL.md           ← /spotlight-learn
└── spotlight-style/
    └── SKILL.md           ← /spotlight-style
```

## 命令体系

| 命令 | 用途 | 检查安装 | 创建文件夹 | 写复盘 |
|------|------|---------|-----------|--------|
| `/spotlight` | 自动模式 — 先执行任务，再检查/询问安装 | 延迟检查 | 按需 | 按模式 |
| `/spotlight-init` | 强制初始化 — 设置 learn 和 claudework 路径 | 直接初始化 | ✅ | - |
| `/spotlight-work` | 完整工作流 — 项目管理 + 复盘 + 全部功能 | 必须已安装 | ✅ | ✅ |
| `/spotlight-check` | 诊断报告 — 仅输出安装状态，不执行任务 | 仅检查 | - | - |
| `/spotlight-learn` | 仅思考 — 写作铁律 + 避坑 + 思维模式 | 跳过 | ❌ | ❌ |
| `/spotlight-style` | 风格切换 — 混合模式 ↔ 纯学习模式 | 无需安装 | - | - |

## 部署路径

开发完成后，将各目录部署到 `C:\Users\admin\.claude\skills\`：

```
skills/
├── spotlight/SKILL.md
├── spotlight-init/SKILL.md
├── spotlight-work/SKILL.md
├── spotlight-check/SKILL.md
├── spotlight-learn/SKILL.md
└── spotlight-style/SKILL.md
```

## 开发工作流

**边工作边完善**：

1. 在日常项目中与用户协作时，发现新的写作偏好、思维模式、错误教训
2. 将新发现更新到 `SKILL.md`（主技能）对应章节
3. 如果新内容涉及子命令的行为变更，同步更新对应的子命令 SKILL.md
4. 更新版本号和"最后更新"日期
5. 同时将经验教训写入 learn 复盘文件（双轨同步）
6. 当技能组足够成熟后，部署到 skills 目录

## 数据来源

- `{learn_path}` — 项目复盘文件，SKILL.md 的经验教训来源
- `~/.claude/CLAUDE.md` — 全局用户规则
- `{claudework_path}/CLAUDE.md` — 工作区规则
- 用户在各项目中的交互记录 — 新发现的直接来源

## 命名历史

- 原名：GCH
- 现名：Spotlight（探照灯 — 注意力导向的工作流隐喻）
- 改名原因：用户不希望实名信息出现在公开发布的技能文件中
