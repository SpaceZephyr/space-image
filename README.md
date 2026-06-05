<div align="center">

# space-GPT-image2-design

> *「打字。回车。一张能直接发的图。」*

[![License](https://img.shields.io/badge/License-Personal%20Use%20Only-orange.svg)](#license)
[![Skills](https://img.shields.io/badge/Claude%20Code-Skill-blueviolet)](https://docs.claude.com/en/docs/claude-code/skills)
[![Model](https://img.shields.io/badge/Model-GPT--image--2-black)](#配置-api-key)
[![Author](https://img.shields.io/badge/by-%40zephyrwang6-FF4D4F)](https://github.com/zephyrwang6)

<br>

**在 Claude Code 里说一句中文，拿回一张能直接发的图。**

<br>

不是「AI 画的还行」那种水平——是看起来像找设计师做的。

小红书爆款封面、Keynote 级 PPT 配图、热力图 / 流程图 / SWOT、公众号文章逻辑图——一个 Skill 全搞定。
12 种内置视觉风格，从 Apple Keynote 极简到中式宋体留白，从赛博霓虹到杂志撞色，每种都按真实设计师的方法论拆细到 hex / 字体 / Do & Don't。

```bash
# 直接克隆到本地
git clone https://github.com/zephyrwang6/space-GPT-image2-design.git ~/.claude/skills/space-GPT-image2-design
```

[看效果](#样图--9-张全部用-skill-自己跑出来) · [装上就能用](#装上就能用) · [5 个 Skill](#5-个-skill) · [核心机制](#核心机制) · [License](#license)

</div>

---

## 装上就能用

把任意一个 Skill 文件夹复制到 `~/.claude/skills/`，配上你自己的 GPT-image-2 API key，就能在 Claude Code 里直接说话：

```
「画张小红书封面：标题"我用AI每天读100篇文章"，xhs-vibrant 风格」
「做张PPT配图：核心观点 Context, not Prompts，minimal 风格」
「画个产品路线图，dark-atmospheric 风格」
「为我这篇文章批量配 6 张图，sketch-notes 风格」
「整套幻灯片：把这份 markdown 转成 12 页 deck」
```

没有 Figma，没有 Canva，没有模板库。说话就行。

---

## 5 个 Skill

每个 Skill 文件夹独立，可以按需挑选 / 全装上。底层都通过 OpenAI Codex / 官方 GPT-image-2 API 出图。

| Skill | 一句话 | 输出 | 典型耗时 |
|-------|--------|------|----------|
| **[space-image-studio](./space-image-studio)** | 全能图片工作室：4 类型 × 12 风格的总控 | 单张高质量 PNG | 2–8 min |
| **[space-article-batch-illustration](./space-article-batch-illustration)** | 文章自动配图：分析段落 → 批量生图 → 自动插入 | 多张 PNG + 修改后的 md | 5–15 min |
| **[space-article-cover-and-batch-illustration](./space-article-cover-and-batch-illustration)** | 公众号封面 + 文章配图：封面单张，配图多张，默认走 Codex 内置 image2 | 1 张封面或多张配图 | 3–15 min |
| **[space-chart-image](./space-chart-image)** | 10 类结构化图表（流程 / 架构 / SWOT / 路线图…） | 单张 PNG | 2–5 min |
| **[space-baoyu-slide-deck](./space-baoyu-slide-deck)** | 内容到整套幻灯（含大纲）+ PPTX/PDF 导出 | 多张 PNG + PPTX + PDF | 15–30 min |

---

## 样图 · 9 张全部用 skill 自己跑出来

下面这 9 张图，没有打开任何设计软件，全是 `space-image-studio` 一句话生成的。

### 小红书封面（3:4 · 3 风格对比）

| xhs-vibrant | chinese-elegance | bold-editorial |
|---|---|---|
| 「我用AI每天读100篇文章」 | 「AI时代 如何活得像个人」 | 「30天 副业月入3万」 |
| 暖色 + 真实物品 + 红色重点笔触 | 宣纸底 + 竖排宋体 + 朱砂方印 | 黄黑分屏 + 撞色超大字 |

### PPT 配图（16:9 · 3 风格对比）

| minimal | dark-atmospheric | bold-editorial |
|---|---|---|
| Context, not Prompts | AI Agent 的三种形态 | 一个人 就是一支团队 |
| 白底 + 金线分隔 + 三卡编号 | 深色 + 紫青粉霓虹卡 + ★ 评分 | 红奶油分屏 + 4 角色编号 |

### 图表（3 种 · blueprint / corporate / scientific）

| 流程图 | SWOT | 热力图 |
|---|---|---|
| AI 内容生产 6 步工作流 | 做付费专栏的 SWOT 分析 | 一周时间精力分布热力图 |
| 深蓝工程图纸感 + 青色高亮关键节点 | 投资级深蓝 + 金线 + 4 象限色彩区分 | 学术级 IBM Plex Mono + 连续色带图例 |

---

## 核心机制

### 风格不是滤镜，是设计方法论

每个风格文件（`references/styles/*.md`）都包含完整 4 维定义：

| 维度 | 内容 |
|------|------|
| **Background** | 底色 hex / 是否有纹理 / 渐变方向 |
| **Typography** | 标题字体 / 正文字体 / 字重 / 字距偏好 |
| **Color Palette** | 5–8 个 hex 色，按角色分配（背景 / 主文 / 次文 / 强调 / 装饰） |
| **Visual Elements + Do/Don't** | 视觉元素清单 + 做什么 + 绝对不做什么 |

举例 · `xhs-vibrant.md` 不是说「小红书风」三个字，而是：

```
- 高饱和暖色背景 #FFF4D6
- 主标题占画面高 1/4–1/3
- 标题带描边或 highlight 块
- 数字/数据用加粗大号
- 真实物品做视觉锚点
- ❌ 冷色阴沉调（深蓝/灰）
- ❌ emoji 列表（≤ 2 个）
- ❌ 假数据或夸张话术
```

风格越具体，AI 越不会跑偏。

### 5 步标准化流程（image-studio）

```
输入内容 → 选类型 → 补全信息 → 选风格 → 提示词模式（自动/审核）→ 出图
```

每步都用 `AskUserQuestion` 强制确认，避免「AI 自己脑补，跑出来不是你要的」。

「内容完整性检查」这一步是最关键的——每种类型有强制必填字段：
- 小红书封面：主标题 / 副标题 / 视觉描述 / 主色倾向
- PPT 配图：核心观点 / 关键数据 / 3–5 要点 / 视觉锚点
- 图表：类型 / 节点 / 关系 / 强调项
- 文章逻辑图：核心论点 / 逻辑结构 / 关键概念

缺一个就追问一个。这一步省 20 秒，后面省半小时返工。

### 提示词组装的 4 块结构

```
[1] 类型规范 — 比例 / 信息密度 / 必填字段
[2] 风格指令 — 完整 hex / 字体 / Do & Don't
[3] 用户内容 — 标题 / 节点 / 数据
[4] 通用约束 — 中文字符精确 / 无 logo 水印 / 留白足够
```

提示词控制在 ~1000 字符内（实测过长会被 API 拒绝），既包含完整设计规范，又不超 budget。

---

## Limitations

- **真人照片质量受 GPT-image-2 限制**。涉及具体人物用风格化替代。
- **节点 > 12 个的图表会拥挤**。Skill 会自动建议拆图。
- **生成耗时 100–500 秒/张**（4:3 大尺寸更慢，已设置 600s timeout）。
- **不支持图层级编辑**。输出 PNG，要改文字得重生。
- **依赖 GPT-image-2 API**（OpenAI Codex / 兼容服务商），需要自己充值（每张约 $0.05–0.1）。

这是一个 80 分的 skill，不是 100 分的产品。
对不愿意打开 Photoshop / Figma 的人，80 分的 skill 比 100 分的产品好用。

---

## 仓库结构

```
space-GPT-image2-design/
├── README.md                              # 本文件
├── .gitignore                             # 排除你的 API key 配置
├── space-image-studio/                    # 全能图片工作室
│   ├── SKILL.md                           # 主入口（5 步流程）
│   ├── .labnana.env.example               # API key 配置模板
│   ├── scripts/generate_image.py          # GPT-image-2 API 调用
│   └── references/
│       ├── types/        (4 类型规范)
│       ├── styles/       (12 风格定义)
│       └── prompt-templates/base.md       # 提示词组装模板
├── space-article-batch-illustration/      # 文章批量配图
├── space-article-cover-and-batch-illustration/ # 公众号封面 + 批量配图（Codex 内置 image2）
├── space-chart-image/                     # 10 类结构化图表
└── space-baoyu-slide-deck/                # 整套幻灯片生成
```

---

## 配置 API key

每个 Skill 都依赖 GPT-image-2 模型（通过 OpenAI Codex 或第三方兼容 API 提供）：

1. 准备一个支持 `gpt-image-2` 的 API endpoint + key
2. 在每个 Skill 文件夹复制 `.labnana.env.example` 为 `.labnana.env`
3. 填入你自己的 endpoint + key

```bash
cd ~/.claude/skills/space-GPT-image2-design/space-image-studio
cp .labnana.env.example .labnana.env
# 编辑 .labnana.env 填入你的 API_KEY 和 API_URL
```

⚠️ `.labnana.env` 已写入 `.gitignore`，不会被推到 GitHub。

---

## 起源

我每天写文章、做 PPT、发小红书，需要的图远多于设计师能交付的速度。
试过一堆 AI 画图工具，问题都一样：
- **MidJourney** 美但不可控、不能精准放中文
- **Canva AI** 套模板有上限
- **chart.js / Mermaid** 是图表，不是「设计」
- **GPT-image-2** 原生能力强，但缺一层「设计师方法论」的封装

于是把每种场景拆成「类型规范 + 风格库 + 标准化流程」，做成 Skill，让 AI 按设计师的方式工作。

参考了 Anthropic 的 [skill-creator](https://docs.claude.com/en/docs/claude-code/skills) 设计哲学，以及 [@alchaincyf](https://github.com/alchaincyf) 在 huashu-design 仓库里展示的「品牌资产协议 + Junior Designer 工作流」思想。

---

## License

**个人使用免费、自由**——学习、研究、写文章、做副业、发自己的内容，随便用，不用打招呼。
**企业商用请联系**——任何公司、团队或盈利组织想集成进自己的产品 / 对外服务，请先和我打招呼。

---

<div align="center">

由 **[@zephyrwang6（空格）](https://github.com/zephyrwang6)** 制作 · 持续分享 AI 产品的思考与实践

如果有用，点个 ⭐ 支持一下

</div>
