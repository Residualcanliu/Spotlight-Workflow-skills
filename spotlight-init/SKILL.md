---
name: spotlight-init
description: >
  Spotlight 工作流引擎 — 初始化安装。强制进入初始化流程，设置 learn（复盘库）和
  claudework（项目工作区）的存放位置。无论之前是否已配置，都会重新执行安装。
---

# Spotlight Init — 初始化安装

你已被 `/spotlight-init` 命令调用。用户想要**强制初始化/重新初始化** Spotlight 工作流引擎。

## 执行流程

1. **加载主技能文件**：读取 spotlight 主技能文件，完整理解 Spotlight 工作流体系。
   > `{项目目录}` 解析规则：优先检查 `~/.claude/skills/spotlight/SKILL.md`（已部署）；如果不存在，则查找当前工作目录或其父目录中的 `SKILL.md`（开发模式）。

2. **检查是否已有配置**：
   - 读取 `~/.spotlight_config.json`
   - 如果已存在 → 提示用户："检测到已有配置（{路径信息}）。是否覆盖？"
     - 覆盖 → 继续
     - 不覆盖 → 告知用户配置保持不变，退出
   - 如果不存在 → 直接继续

3. **执行安装流程**：
   - 跳至主技能 §0.2 欢迎界面
   - 执行 §0.3 询问 learn 位置
   - 执行 §0.4 询问 claudework 位置
   - 保存配置到 `~/.spotlight_config.json`，其中 `mode` 设为 `"full"`，`initialized` 设为 `true`，`writing_style_mode` 默认设为 `"blend"`

4. **安装完成后**：
   - 运行一次 `/spotlight-check` 逻辑确认安装状态
   - 告知用户所有功能已就绪

> 详细避坑清单、工具速查、思维模式见同目录下的 `REFERENCE.md`。按需读取，无需一次加载。
