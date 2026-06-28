---
name: spotlight-check
description: >
  Spotlight 工作流引擎 — 安装状态检查。诊断当前工作流的安装情况：
  配置文件是否存在、learn 和 claudework 文件夹状态、复盘文件数量、
  当前运行模式。不执行任何实际任务，仅输出诊断报告。
---

# Spotlight Check — 安装状态检查

你已被 `/spotlight-check` 命令调用。用户想要**诊断当前工作流安装状况**。

## 执行流程

1. **加载主技能文件**：读取 spotlight 主技能文件。
   > `{项目目录}` 解析规则：优先检查 `~/.claude/skills/spotlight/SKILL.md`（已部署）；如果不存在，则查找当前工作目录或其父目录中的 `SKILL.md`（开发模式）。

2. **收集诊断信息**：
   - 检查 `~/.spotlight_config.json` 是否存在
   - 如果存在，读取其中的 `learn_path`、`claudework_path`、`mode`、`version`
   - 检查 `learn_path` 文件夹是否存在 → 统计 `.md` 复盘文件数量
   - 检查 `claudework_path` 文件夹是否存在 → 统计子目录数量
   - 检查 `~/.claude/CLAUDE.md`（全局 CLAUDE.md）是否存在

3. **输出诊断报告**：

   ```
   ══════════════════════════════════════
     Spotlight 工作流 — 安装状态检查
   ══════════════════════════════════════

   配置文件：  ~/.spotlight_config.json — 存在 / [N] 不存在
   当前模式：  [full / lightweight / 未安装]
   版本：      [版本号]

   learn（复盘库）：
      路径：     [路径]
      状态：     文件夹存在 / [N] 文件夹不存在 / 路径未配置
      复盘数：   [N] 个 .md 文件

   claudework（项目工作区）：
      路径：     [路径]
      状态：     文件夹存在 / [N] 文件夹不存在 / 路径未配置
      项目数：   [N] 个子目录

   全局 CLAUDE.md：
      位置：     ~/.claude/CLAUDE.md — 存在 / [N] 不存在

   ══════════════════════════════════════
   ```

4. **如果有异常**（路径配置了但文件夹不存在等），给出修复建议：
   - 文件夹丢失 → "建议运行 /spotlight-init 重新配置路径"
   - 完全未安装 → "运行 /spotlight-init 开始初始化"
   - 轻量模式 → "运行 /spotlight-work 升级为完整模式"
   - 全局 CLAUDE.md 不存在 → "全局 CLAUDE.md 不由 Spotlight 管理。如需创建，请运行 /init 或手动创建 `~/.claude/CLAUDE.md`。"

5. **不执行任何实际任务**。输出报告后即结束。
