---
name: spotlight-work
description: >
  Spotlight 工作流引擎 — 完整工作流模式。确保工作流已安装后，以完整模式执行项目管理任务：
  项目创建（日期前缀+Init）、写作铁律、learn 复盘、全部避坑清单。
  如果未初始化则提示先运行 /spotlight-init。
---

# Spotlight Work — 完整工作流模式

你已被 `/spotlight-work` 命令调用。用户想要以**完整工作流模式**运行。

## 执行流程

1. **加载主技能文件**：读取 spotlight 主技能文件，完整理解 Spotlight 工作流体系。
   > `{项目目录}` 解析规则：优先检查 `~/.claude/skills/spotlight/SKILL.md`（已部署）；如果不存在，则查找当前工作目录或其父目录中的 `SKILL.md`（开发模式）。

2. **检查安装状态**：
   - 读取 `~/.spotlight_config.json`
   - 如果**不存在** → 提示用户：
     ```
     Spotlight 工作流尚未初始化。
     请先运行 /spotlight-init 完成设置，或运行 /spotlight 选择轻量模式。
     ```
     停止，不继续执行。
   - 如果存在但 `mode` = `"lightweight"` → 询问用户：
     ```
     当前为轻量模式。是否升级为完整工作流模式？
     升级后将启用：项目创建工作流、learn 复盘写入。
     ```
     - 是 → 重新执行初始化，将 mode 改为 `"full"`
     - 否 → 以当前轻量模式继续（同 `/spotlight-learn`）
   - 如果存在且 `mode` = `"full"` → 加载配置，继续。

3. **以完整模式执行用户任务**：
   - 启用全部功能：
     - §一 项目全生命周期工作流（含 1.1 项目创建）
     - §二 写作风格三项铁律（实际生效比例受 writing_style_mode 控制，见主技能 §二 模式门）
     - §三 用户思维与决策模式
     - §四 错误→正确路径避坑
     - §五 工具使用最佳实践
     - §六 复盘与持续学习
     - §七 核心铁律速查
   - 项目默认创建在 `{claudework_path}` 下
   - 任务完成后自动写入 `{learn_path}` 复盘
