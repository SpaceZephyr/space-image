---
name: article-cover-and-batch-illustration
description: 分析文章结构并生成公众号视觉素材，默认使用 Codex 内置 image_gen/image2。当用户说"制作封面图"、"生成封面"时输出一张 2.35:1 白底工程风封面图；当用户说"批量配图"、"给文章配图"、"生成文章插图"、"为这篇文章配图"时为段落批量生成多张专业逻辑图/概念图。自动保存到Obsidian图片目录并按需插入文档。
---

# 文章封面与批量配图

分析 Markdown 文章结构，默认调用 Codex 内置 `image_gen` 工具（image2）生成公众号视觉素材。用户说“制作封面图/生成封面”时只生成一张封面；用户说“制作配图/批量配图/给文章配图”时为每个段落/小节生成多张配图并插入文档。旧的 API 脚本只作为用户明确要求 CLI/API fallback 时使用。

## 路由规则

| 用户意图 | 输出 | 风格参考 | 默认比例 |
|---------|------|----------|----------|
| 制作封面图 / 生成封面 / 封面图 | 1 张封面图 | `references/cover-style.md` | 2.35:1 |
| 制作配图 / 批量配图 / 给文章配图 / 文章插图 | 多张段落配图 | `references/style-guide.md` | 16:9 |

如果用户同时要求“封面图和配图”，先生成封面图，再进入批量配图流程。

## 封面图工作流程

### Cover Phase 1: 提取封面信息

1. **读取文章** - 获取用户提供的文章内容（当前打开文件、指定路径或粘贴文本）
2. **确定标题** - 使用用户明确给出的标题；如果没有标题，从文章 H1 或核心主题中提炼一个
3. **提取顶部小字** - 使用用户指定的小字；如果用户没有指定，默认空置，不要臆造篇数
4. **梳理全文逻辑** - 提炼 5-7 个流程节点，用于封面右侧/底部的系统图
5. **读取封面风格** - 使用 `references/cover-style.md`

### Cover Phase 2: 生成 1 张封面图

调用 Codex 内置 `image_gen` 工具生成单张封面。封面必须遵循：

- **比例**: 2.35:1 横版宽封面
- **背景**: 白底或暖白底
- **版式**: 左侧大标题，右侧/底部展示全文逻辑系统图
- **标题**: 用户给定标题必须完整、醒目、黑色、粗体、可读
- **顶部小字**: 用户指定时必须逐字呈现，例如 `空格的第 205 篇原创文章`
- **视觉语言**: ASCII/工程蓝图风、蓝色虚线连接、点阵网格、UI 卡片、文件夹、终端、流程节点
- **输出数量**: 只生成 1 张

工具调用前，把封面提示词整理成完整规格：

```text
Use case: ads-marketing
Asset type: WeChat article cover
Primary request: [标题 + 文章核心逻辑 + 顶部小字]
Aspect ratio: 2.35:1 wide cover
Style reference: white background, bold Chinese editorial typography, ASCII/technical blueprint details, blue dashed connector lines, dotted guide grids, small UI cards, clean creator-tool aesthetic
Layout: title on the left half, workflow/system diagram on the right and lower area
Text policy: Chinese text must be accurate and readable. The title and top small text must appear exactly as requested.
Avoid: dark background, photorealistic people, brand logos, clutter, watermark, illegible tiny text
```

### Cover 保存规范

封面图保存到当前 Obsidian vault：

```text
/path/to/current/obsidian-vault/09 image/MMDD-主题简称/
└── 00-cover-主题简称.png
```

如果 `image_gen` 输出比例不是严格 2.35:1，允许在不裁切画面主体的前提下补白边到 2.35:1，并另存为 `00-cover-主题简称-2.35.png`。

## 配图工作流程

### Phase 1: 分析文章 → 生成提示词

1. **读取文章** - 获取用户提供的文章内容（当前打开文件或指定路径）
2. **结构分析** - 按 H2/H3 标题拆分段落，提取每个段落核心思想
3. **生成风格指令** - 根据文章主题生成全局 STYLE INSTRUCTIONS 代码块
4. **生成提示词** - 为每个段落创建图片提示词大纲（参考 references/style-guide.md）
5. **展示并确认** - 以列表形式展示所有提示词，等待用户确认或修改

### Phase 2: 生成图片 → 插入文档

6. **批量生成** - 使用 Codex 内置 `image_gen` 工具逐个生成图片
7. **保存图片** - 将生成结果复制/移动到当前 Obsidian vault 的 `09 image/MMDD-主题名称/` 目录
8. **插入文档** - 在每个段落标题后插入 `![[图片路径]]` 引用

## Phase 1 详细指引

### 1. 文章结构分析

读取文章后，按以下规则拆分：

- 以 `## ` (H2) 或 `### ` (H3) 标题作为段落分隔符
- 忽略 frontmatter（YAML）部分
- 忽略纯引用、脚注等辅助内容
- 提取每个段落的：标题、核心观点（1句话）、关键概念（3-5个词）

输出格式：
```
## 文章结构分析

| # | 段落标题 | 核心观点 | 关键概念 |
|---|---------|---------|---------|
| 1 | xxx     | xxx     | A, B, C |
| 2 | xxx     | xxx     | D, E, F |
```

### 2. 生成全局风格指令

在所有提示词之前，必须先生成 STYLE INSTRUCTIONS 块。读取 references/style-guide.md 获取风格模板。

默认使用**风格 1（简约手绘风）**，用户可选择风格 2（建筑蓝图编辑风）。

```
STYLE INSTRUCTIONS:
- 整体风格: 简约手绘风格 / 建筑蓝图编辑风格
- 色彩方案: 白底为主，黑色线条，[主题点缀色]
- 比例: 16:9 横版
- 分辨率: 2K
- 文字量: 极少，仅保留1-3个核心关键词
- 文字语言: 图片中文字以简体中文为主，专业术语/缩写（如 AI、API、LLM）可保留英文
- 视觉语言: 逻辑图、流程图、概念图
- 一致性: 统一线条粗细、留白比例、排版网格
```

### 3. 为每个段落生成提示词

每个提示词结构：
1. **风格前缀** - 来自 STYLE INSTRUCTIONS 的通用描述
2. **图表类型** - 概念图/流程图/对比图/层次图/关系图
3. **内容描述** - 以段落核心思想为主，用叙述性语言描述图表内容
4. **中文标签** - 直接写中文关键词（如 "数据采集"、"智能处理"），1-3个
5. **中文为主指令**（必须） - 每个提示词末尾追加：`ALL text, labels, and annotations in the image MUST be primarily in Chinese (Simplified Chinese, 中文). Use clean Chinese font for main text. Technical terms and abbreviations (e.g. AI, API, LLM, RAG) may remain in English.`
6. **排除项** - "No photography, no realistic elements, no complex gradients"

展示格式（等待用户确认）：
```
## 提示词大纲

### 图 1: [段落标题]
- 图表类型: 概念图
- 提示词:
  """
  [完整英文提示词]
  """

### 图 2: [段落标题]
...
```

**关键**:
- 提示词主体用英文编写，图片中要出现的文字标签保留中文原文
- 图片中需要出现的文字标签直接写中文原文（如 `The central node labeled "AI生产力系统"`）
- **每个提示词末尾必须包含中文为主指令**，确保图片中文字以中文为主，专业术语可保留英文

### 4. 等待确认

展示完所有提示词后，询问用户：
- "以上提示词是否满意？是否需要修改某个图的描述？"
- "确认后将开始批量生成图片（共 N 张）"
- 用户可指定某个图使用不同风格或修改描述

## Phase 2 详细指引

### 5. 使用 Codex 内置 image2 生成图片

确认后逐个调用 Codex 内置 `image_gen` 工具。每张图单独调用一次，不要把多张不同图合并到同一个提示词中。

工具调用前，把每张图提示词整理成完整规格：

```text
Use case: infographic-diagram
Asset type: Obsidian article illustration
Primary request: [完整提示词]
Aspect ratio: 16:9 landscape
Resolution intent: high resolution, suitable for article header/section illustration
Text policy: ALL text, labels, and annotations in the image MUST be primarily in Chinese (Simplified Chinese, 中文). Technical terms and abbreviations may remain in English.
Avoid: photography, realistic elements, complex gradients, watermark, illegible text
```

**注意事项**:
- MMDD 取当天日期（如 0206）
- 主题名从文章 H1 标题提取，简化为短名称
- 图片编号两位数字（01, 02, 03...）
- 每张图生成后检查结果是否符合：16:9、风格一致、中文标签可读、没有水印
- 若某张图失败，记录并继续下一张，最后汇报失败项
- Codex 内置工具默认会把图片保存到 `$CODEX_HOME/generated_images/...`；项目要使用的最终图必须复制或移动到 Obsidian vault 内，不能只引用默认保存位置

### 6. 保存路径规范

```
/path/to/current/obsidian-vault/09 image/MMDD-主题简称/
├── 01-段落标题简称.png
├── 02-段落标题简称.png
├── 03-段落标题简称.png
└── ...
```

### 7. 插入文档

在文章对应段落标题下方插入图片引用：

```markdown
## 段落标题

![[09 image/MMDD-主题简称/01-段落标题简称.png]]

段落正文内容...
```

使用 Obsidian wikilink 格式 `![[路径]]` 插入。

## 生成配置

### Codex 内置 image2（默认）

| 配置项 | 值 |
|-------|---|
| 工具 | Codex 内置 `image_gen` |
| Model | Codex 内置 image2 |
| API Key | 不需要用户提供 |
| 默认比例 | 16:9 |
| 默认分辨率 | 高质量/项目可用 |

执行要求：
- 用 `image_gen` 工具逐张生成。
- 生成后从 `$CODEX_HOME/generated_images/...` 复制/移动成目标文件名。
- 插入 Obsidian wikilink 时使用 vault 内相对路径，例如 `![[09 image/MMDD-主题简称/01-段落标题简称.png]]`。

### CLI/API fallback（仅当用户明确要求）

`scripts/generate_image.py` 保留为旧 API fallback。不要在默认流程中使用它；只有当用户明确要求 LabNana、Gemini、CLI、API key、指定模型参数，或内置 `image_gen` 不可用且用户确认 fallback 时才调用。

#### LabNana API fallback

| 配置项 | 值 |
|-------|---|
| API URL | `https://api.labnana.com` |
| API Key | 存储在 `.labnana.env` 文件 |
| Model | `gpt-image-2` |
| Provider | `openai` |
| 默认比例 | 16:9 |
| 默认分辨率 | 2K |

调用示例：
```bash
python3 scripts/generate_image.py \
  --prompt "提示词内容" \
  --output "/path/to/output.png" \
  --provider labnana \
  --aspect-ratio "16:9" \
  --resolution "2K"
```

## 风格选择

| 风格 | 特征 | 适用场景 |
|------|-----|---------|
| 风格 1（默认）| 简约手绘，黑色线条，白底 | 通用、概念解释、流程说明 |
| 风格 2 | 建筑蓝图/技术期刊，精致极简 | 系统架构、技术分析、专业内容 |

用户可在确认阶段选择全局风格，也可为单个图指定不同风格。

## 常见用法

| 用户说 | 操作 |
|-------|-----|
| "给这篇文章制作封面图" | 按 `references/cover-style.md` 生成 1 张 2.35:1 白底工程风封面 |
| "制作封面图，标题是xxx" | 使用指定标题和文章逻辑生成 1 张封面 |
| "给这篇文章配图" | 分析当前打开的文章并批量配图 |
| "批量配图" | 同上 |
| "用风格2给文章配图" | 使用建筑蓝图编辑风格 |
| "修改第3张图的提示词" | 重新生成指定图片 |
| "重新生成第2张" | 用修改后的提示词重新调用内置 image2 |
