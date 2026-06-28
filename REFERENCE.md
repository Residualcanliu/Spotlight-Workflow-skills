# Spotlight — 参考手册

> 本文件是 Spotlight 的详细参考手册。**按需加载，不要一次读完。** 核心指令见 `SKILL.md`。

---

## §1 新项目启动

```
用户提出需求 → 创建项目目录 → cd 进入 → 搭建脚手架 → 运行 Init → 开始开发
```

1. **创建目录**：`{claudework_path}\YYYY年-MM月-DD日-项目名称`
   - 日期格式：`YYYY年-MM月-DD日`（如 `2026年-06月-26日-my-project`）
   - 未指定项目名称则先询问
2. **切换工作目录**到新项目文件夹
3. **搭建项目脚手架**（按项目类型）
4. **运行 `/init`**：在脚手架就位后生成 CLAUDE.md
5. **开始开发**

---

## §2 工作流模式

### 2.1 迭代精炼

用户不会一次说完所有需求——这是正常的：

```
用户给核心要求 → AI执行初版 → 呈现给用户 → 用户补充/修正 → AI调整 → 循环至完成
```

- 做完初版后**主动呈现**，不要等用户来问
- 用户的补充约束（如"XX不动"）**立刻确认并执行**

### 2.2 两阶段审批

适用于风格模仿、大段改写等容易有理解偏差的任务：

```
Phase 1: 总结规律/方案 → 用户判断方向 → Phase 2: 执行 → 用户确认结果
```

核心原则：向用户展示中间检查点，大幅降低返工风险。

### 2.3 文档编辑（officecli）

**三步法：**
```
Step 1: get --json 读结构 → Step 2: set/remove/add 做修改 → Step 3: get --depth 1 快速验证
```

**修改前检查清单：**
- [ ] 跑了 `officecli query image` 确认图片位置了吗？
- [ ] 目标段落是否包含图片？（含图片的段落绝对不能碰）
- [ ] 是否用了 stable paraId 寻址（而非位置索引）？

### 2.4 Signal Counter 模式（跨组件联动）

**场景：** 组件 A 执行完动画后需要触发组件 B 重新显示 UI。

**解决：** context 中加计数器字段（如 `signalGeneration: 0`）：
- A 调用 `resetXxx()` → `signalGeneration++`
- B 用 `useEffect` 监听 `signalGeneration` → 变化时 `setShowXxx(true)` + 导航

要点：计数器只增不减；B 用 `if (counter > lastCounter)` 判断；适用于动画后 UI 重显、多步骤阶段切换、跨路由状态同步。

---

## §3 写作风格（完整）

### 3.1 双模式设计

| 模式 | 来源 | 说明 |
|------|------|------|
| `blend`（默认） | 50% Spotlight 内置 + 50% 用户个人风格 | 日常使用 |
| `learn_only` | 100% 用户个人风格 | learn 积累足够后切换 |

`/spotlight-style` 一键切换。配置字段：`writing_style_mode`: `"blend"` | `"learn_only"`

### 3.2 五维风格框架

分析参考文本时从五个维度入手：

| 维度 | 内容 | 默认偏好 |
|------|------|---------|
| **整体结构** | 章节如何组织？粒度如何？ | 粗粒度模块：按功能归并，不穷尽罗列 |
| **段落内部模式** | 段落内信息如何流动？ | "思路→截图→验证"三段节奏：设计意图 → 代码/截图 → 观察结论 |
| **语言特征** | 用词、句式、语气 | 第一人称叙事："我定义了……"，实验报告像开发日志 |
| **核心区别** | 和目标文体的典型写法有何不同？ | 叙事感 > 教科书感：技术细节带着理由出现 |
| **一句话概括** | 整篇风格的本质 | 粗粒度模块 + 第一人称 + 三段节奏 + 口语化过渡 + 设计决策带理由 |

### 3.3 图片与桥接规范

- 图片前：简短引导语（"关键代码如下："、"效果如下："）
- 图片后：用"可以看到……"做观察结论
- 图片保护：模板中图片位置/编号/尺寸已审核，不重新排版
- 占位符格式：`[结果参数]`、`[图片N]`，用方括号与正文括号区分

### 3.4 先搭框架后填数据

1. 先写好报告骨架（所有段落、图片位置）
2. 用占位符标记待填充内容（`[结果参数]`、`[图片x]`）
3. 跑完实验拿到实际数据后一次性替换

---

## §4 用户思维模式（完整）

### 4.1 核心特征

**迭代精炼型思维者。** 用户先给核心框架，在执行中逐层补充——在看见初版之后才能更好地判断下一步。

**"即时应用"要求者。** 新规则立完立刻在当前场景践行一次。"定规则→立刻用→写复盘"的闭环。

**自己做模板的主人。** 保留自己手写的作品作为风格参照——"我写过的就是我认可的标准"。

**"可追溯性优先"者。** 要求版本记录（version.md）、项目记忆（memory/）、复盘文件（learn/）三层体系。"改了什么、为什么改、学到了什么"三者缺一不可。

**"元工作流"观察者。** 不只复盘项目内容，也复盘 AI 的执行过程——AI 的 error 不是"默默修好就行"，而是值得写入复盘的重要内容。

**设计敏感型决策者。** 对视觉设计高度敏感。偏好系统性全局调整。修改方向：① 更大（字号、间距、容器宽度）② 更亮（颜色、对比度）③ 更满（利用左右空白区域）。

**`[xxN]` 占位符系统使用者。** 用 `[xx1]`、`[xx2]` … `[xxN]` 标记待填写的个人数据。AI 不填写虚假数据，使用此占位符系统。

**"慢即是快"偏好。** "慢慢优化下" = 小步迭代，每次只做一小步。AI 应主动控制改动范围。除非用户说"一起改完"或"批量处理"。

### 4.2 决策节奏

- 简短指令 → 期望 AI 自己判断实现方式（不讲"为什么"，只讲"做什么"）
- 修改完成后不主动要求验证：AI 应主动验证，但不需长篇报告
- 所有修改在同一文档上累积：不做备份/另存，直接改原文件
- 微调时一次改 2-3 维：位置+大小+透明度一起调，缩短迭代轮次
- "慢慢"是节奏信号：每次只做一步，等反馈

### 4.3 验收标准

1. 结构清晰：一眼能看到层次
2. 不过度：不会做多余的事
3. 一致性：和用户自己写的风格一致
4. 闭环：规则立了就用，任务完了就复盘

---

## §5 完整避坑清单

### 5.1 officecli

| 错误 | 症状 | 正确做法 |
|------|------|---------|
| batch JSON 中 ASCII 双引号未转义 | 解析失败：`'C' is invalid after a value` | 中文引用全部用方括号 `[xxx]` 替代。设置 `OFFICECLI_BATCH_ALLOW_STDIN_REDIRECT=1` |
| set 替换段落文本丢失格式 | 多 run 结构被替换为单个 run | 格式统一的段落用 set；混合格式用 `--find`/`--replace` |
| 位置索引寻址不稳定 | 增删段落后索引偏移 | 用 stable paraId：`p[@paraId=00100054]`，不用 `p[3]` |
| 逐段 set 效率低 | 中间出错难定位 | 用 batch JSON 一次性提交 |
| get 输出过大 | stdout 截断 | 用 `--depth 1` 看概要，完整内容自动持久化 |
| 未确认图片位置就编辑 | 误删含图片段落 | 编辑前必跑 `officecli query image` |

### 5.2 文件操作

| 错误 | 症状 | 正确做法 |
|------|------|---------|
| Edit 精确匹配失败（中英混合） | old_string 匹配不到 | 用 Write 全量覆写。也适用于 SKILL.md、CLAUDE.md 等配置文件的修改 |
| Glob 返回相对路径直接拼绝对路径 | File not found | 用 `find` 或 Bash 确认实际路径 |

### 5.3 理解偏差

| 错误 | 症状 | 正确做法 |
|------|------|---------|
| 凭印象改写，不先读全貌 | 改写结果和原文脱节 | 文档改写前先用 `get --depth 3` 读全貌 |
| 风格模仿跳过中间检查 | 改完方向不对，大面积返工 | 先总结风格特征 → 用户确认 → 再批量执行 |
| 做了用户没要求的多余工作 | 多写心得、多分场景分析 | 严格遵守三项铁律 |

### 5.4 Python/Windows 环境

| 错误 | 症状 | 正确做法 |
|------|------|----------|
| Windows 下使用 python3 | exit code 49 | 永远用 `python` |
| print 含 Unicode 特殊字符 | UnicodeEncodeError | ① 脚本开头加 `sys.stdout.reconfigure(encoding='utf-8')` ② 用 ASCII 标记（OK/FAIL）代替 Unicode 符号 |
| 多个脚本顺序修改同一文件 | 后执行脚本模式匹配失效 | ① 后跑脚本基于最新文件状态 ② 全部跑完统一验证 ③ pattern not found 可能是前面的脚本已完成该修改 |

### 5.5 React/Three.js + WebGL

| 错误 | 症状 | 正确做法 |
|------|------|---------|
| `useMemo` 内做副作用更新 shader uniform | resize 后 shader 分辨率不更新 | `useMemo` 只创建一次 uniforms 对象（空 deps）；值变更全部通过 `useEffect` 写入 |
| 3D 对象不可见 | 用户说"没效果" | 定量验证：`可见半高 = (相机z - 物体z) × tan(FOV/2)`，对比物体 scale |
| 深色主题下 opacity 叠加导致文字不可见 | "太暗了" | 两步排查：① 检查基础色值本身是否够亮 ② 检查叠加的 opacity 是否过低 |
| GLSL 着色器多参数同步调优 | 改单参数效果不明显 | 同步调整 7+ 参数：星空密度/亮度、光子环、爱因斯坦环、吸积盘、星云、暗角 |
| Canvas 内 plane 被遮挡或裁剪 | 3D 内容时有时无 | shaderMaterial 加 `depthTest={false}` `depthWrite={false}` |

---

## §6 工具速查

### 6.1 officecli 核心命令

| 操作 | 命令模板 |
|------|---------|
| 读取段落结构 | `officecli get file.docx /body/.../scope --depth 3 --json` |
| 修改段落文本 | `officecli set file.docx '/body/.../p[@paraId=XXX]' --prop text="..."` |
| 删除段落 | `officecli remove file.docx '/body/.../p[@paraId=XXX]'` |
| 文本查找替换 | `officecli set file.docx /scope --find "旧文本" --replace "新文本"` |
| 新增段落（锚点后） | `officecli add file.docx /parent --type paragraph --after '/body/.../p[@paraId=XXX]' --prop text="..."` |
| 查询图片位置 | `officecli query image file.docx` |
| 批量修改 | 构造 JSON 数组，`officecli batch file.docx batch.json` |
| 设置中文字体 | `--prop font.ea="宋体"` |
| 设置西文字体 | `--prop font.latin="Times New Roman"` |
| 设置行距 | `--prop lineSpacing="1.5x"` |
| 设置首行缩进 | `--prop firstLineIndent="24pt"` |

### 6.2 工具选择原则

| 场景 | 工具 | 原因 |
|------|------|------|
| 新建文件 | Write | 比 Edit 可靠，尤其是中英混合 |
| 精确修改片段 | Edit | 只改一处时用 |
| 中英混合/特殊字符修改 | Write（全量覆写） | Edit 的 old_string 匹配容易失败 |
| 搜索文件 | Glob | 比 `find` 快，结果带路径 |
| 搜索文件内容 | Grep | 比 `grep` 精准，支持正则 |
| 确认实际路径 | Bash `find` | Glob 的相对路径可能不准确 |

### 6.3 sed 批量替换规则

**核心：从高数值往低数值替换，避免连锁覆盖。**

```bash
for file in $(grep -rl "old-class-prefix" --include="*.tsx" dir/); do
  sed -i 's/old\/70/old\/90/g' "$file"   # 最高值先
  sed -i 's/old\/60/old\/80/g' "$file"
  sed -i 's/old\/20/old\/40/g' "$file"   # 最低值最后
done
```

### 6.4 3D/WebGL 速查

| 场景 | 方法 |
|------|------|
| 验证 3D 对象是否在视野内 | `可见半高 = (相机z - 物体z) × tan(FOV/2)` |
| shader 亮度不足 | 同步调整 7+ 参数 |
| Canvas resize 后 shader 比例错 | `useEffect` 监听 `size`，更新 `uResolution` uniform |
| 防止 3D 物体被裁剪 | `depthTest={false}` `depthWrite={false}` |
| Canvas 纹理被 DOM 遮挡 | 算纹理 UV→屏幕像素映射，加 DOM 高度偏移（导航栏 ~54-64px） |
| 动态纹理更新 | `drawTexture()` + `setInterval` + `te.needsUpdate = true` + `clearInterval` |

---

## §7 技能联动

### 7.1 已安装技能的自动调用

| 场景 | 联动技能 |
|------|---------|
| Word 文档（.docx） | `officecli` |
| PPT/演示文稿 | `ppt-master` |
| 论文写作/润色 | `nature-writing`、`nature-polishing` |
| 论文图表 | `nature-figure` |
| 论文引用 | `nature-citation` |
| 论文审稿 | `nature-reviewer`、`nature-response` |
| 项目初始化 | `init` |
| 代码审查 | `code-review` |
| 安全审查 | `security-review` |
| 品牌/视觉设计 | `brand`、`design`、`design-system` |

检测逻辑：Glob 检查 `~/.claude/skills/<skill-name>/SKILL.md` 是否存在。

### 7.2 推荐未安装的技能

任务完成后，回顾涉及的工作类型。对未安装但相关的技能，一句话推荐（最多 2 个）。

推荐文案模板：
- `officecli`：本次任务涉及 Word 文档编辑。可在 GitHub 搜索 "claude-code officecli skill"。
- `ppt-master`：本次任务涉及 PPT 制作。可在 GitHub 搜索 "claude-code ppt-master skill"。
- `nature-writing`：本次任务涉及学术写作。可在 GitHub 搜索 "claude-code nature-writing skill"。
- `code-review`：本次任务涉及代码变更。可在 GitHub 搜索 "claude-code code-review skill"。

推荐优先级：① 核心类型优先 ② 安全/正确性优先 ③ 字母序。只在确实相关时推荐，不硬凑。

---

## §8 配置文件参考

### 8.1 位置

`~/.spotlight_config.json`

### 8.2 完整配置

```json
{
  "mode": "full",
  "learn_path": "D:\\learn",
  "claudework_path": "D:\\claudework\\work",
  "writing_style_mode": "blend",
  "initialized": true,
  "version": "2.7",
  "init_date": "2026-06-26"
}
```

| 字段 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `mode` | string | — | `"full"` / `"lightweight"` |
| `learn_path` | string | — | 复盘库根目录绝对路径 |
| `claudework_path` | string | — | 项目工作区根目录绝对路径 |
| `writing_style_mode` | string | `"blend"` | `"blend"` / `"learn_only"` |
| `initialized` | boolean | — | 是否已完成初始化 |
| `version` | string | — | 配置版本号 |
| `init_date` | string | — | 初始化日期 |

### 8.3 重置配置

用户说"重置 Spotlight 配置"或"重新初始化 Spotlight"时，删除 `~/.spotlight_config.json` 并重新执行初始化。

---

> 版本：v2.7 · 最后更新：2026-06-28
