# 公众号封面图风格指南

用于用户说“制作封面图”“生成封面”“封面图”时。默认只生成 1 张封面图，使用 Codex 内置 `image_gen` / image2。

## 固定风格

- **画幅**: 2.35:1 横版宽封面
- **背景**: 纯白或暖白底，允许极轻微纸张纹理
- **标题**: 左侧大标题，黑色，粗体，高辨识度，现代中文无衬线风格
- **顶部小字**: 用户指定时必须逐字呈现，放在顶部小号文字区域，可用 ASCII 虚线框承载
- **逻辑展示**: 右侧和底部用系统图展示全文逻辑，不做随机素材拼贴
- **视觉语言**: ASCII 技术封面、工程蓝图、点阵网格、虚线连接、UI 卡片、文件夹、终端、文档、节点图
- **主色**: 黑白为主，蓝色 `#1267FF` 做工程线和节点强调
- **辅助色**: 少量橙色 `#C56A32` 做重点高亮
- **文字量**: 标题和顶部小字必须准确；流程节点只保留 5-7 个短中文词

## 默认布局

```text
+---------------------------------------------------------------+
| 顶部小字 ASCII 虚线框                                          |
|                                                               |
|  大标题（左侧，2-3 行）          中央/右侧工具窗口或系统主节点 |
|                                                               |
|  副标题或空白（可选）            蓝色虚线连接到流程节点        |
|                                                               |
|  底部横向流程：灵感 -> 写作 -> 配图 -> 排版 -> 发布 -> 分发    |
+---------------------------------------------------------------+
```

## 封面提示词模板

```text
Create a 2.35:1 wide cover image on a clean white / warm off-white background,
in a bold Chinese editorial technology style. Use ASCII/technical blueprint
details, dotted guide lines, thin blue dashed connector lines, small UI cards,
folder/document cards, terminal windows, and clean workflow icons.

Main title text must be large, black, bold, and highly legible:
"[用户指定标题]"

Top small text, exactly:
"[用户指定顶部小字]"

Show the full article logic as a connected system diagram, not a random collage:
[5-7 个流程节点，每个节点是短中文词]

Use only short Chinese labels inside workflow nodes. Make all labels readable.
Use blue (#1267FF) as the main accent, with small orange highlights (#C56A32).
Keep lots of white space. No dark background, no photorealistic people, no brand
logos, no clutter, no watermark, no illegible tiny body text.
```

## 文章逻辑提炼规则

1. 从全文中提炼 5-7 个关键节点，优先使用动词或名词短语。
2. 节点要能串成完整逻辑链，而不是只罗列工具名。
3. 标题表达主题，流程图表达文章结构。
4. 如果文章是工具/工作流类，默认使用“输入 -> 处理 -> 产出 -> 发布/复用”的系统图。
5. 如果文章是观点类，默认使用“问题 -> 原因 -> 方法 -> 案例 -> 结论”的论证图。

## 本用户偏好的公众号创作封面风格

当文章主题是 AI 工具、Skill、Codex、公众号创作、工作流、效率工具时，优先使用以下元素：

- 左侧超大黑体中文标题
- 顶部小字格式，例如 `空格的第 205 篇原创文章`
- 右侧一个 Codex/Claude/工具窗口风格的抽象工作台
- 底部 5-7 个蓝色线框流程卡片
- 流程词示例：`灵感`、`写作`、`配图`、`排版`、`发布`、`分发`、`选题`
- 用虚线和小圆点把工作台、文件、Skill、图片、HTML、视频平台节点连接起来
