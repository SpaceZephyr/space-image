---
name: space-xerox-editorial
description: 用黑底、粉蓝专色、荧光粉强调、影印拼贴字体与半色调物件制作中文编辑型封面。适用于用户点名“黑蓝粉影印”“杂志剪贴字”“会议机器人那版”“字体融入背景”或要求简约但能识别真实场景的科技、办公、Agent 主题海报。是 space-image 的酸性影印风格子 Skill，可独立使用。
---

# 黑蓝粉影印编辑封面

锁定已验证的视觉语言：黑纸背景、纸白影印字、一个粉蓝场景面、少量荧光粉油墨，以及可识别的物件或角色。用具体场景承载一个简单关系，保持成熟的杂志编辑感。

## 默认画幅与输入

- 默认 `2.35:1` 横版，约 `1920 × 817`；用户指定尺寸时遵从其要求。
- 接收文章或主题、准确标题、可选品牌资产。缺少非必要信息时自主补足，不强制询问。
- 先查看 [生成效果图](assets/meeting-agent-example.png)，学习材质、字效与空间比例。样图中的会议、机器人、豆包工作 Logo 和标题是示例内容，不是每次必备元素。

## 视觉规则

### 背景与油墨

- 黑纸 `#070707`，保留细微复印机噪点；不要用渐变雾、霓虹光或全屏花纹。
- 主文字和摄影剪贴用纸白 `#EEEAE2`。
- 粉蓝 `#A9CBFF` 用在一个明确场景面，例如桌面、设备屏幕、纸面或底板。
- 荧光粉 `#FF1F7A` 是实体印刷专色，仅强调一个关键词及一个关键动作；不做发光效果。
- 人物、机器和家具用黑白半色调、网点、影印侵蚀和剪贴边缘。即使有体积，也要像杂志图片经复印后贴在黑纸上，不能像光滑 3D 玩具。

### 排版与字效

- 标题通常两行，较长时三行；行间距紧凑但不粘连。默认用厚重、略窄的中文黑体，保持整句可读。
- 在字形内部加入适量油墨脱落、纸纤维和颗粒；在少数外缘加入极细的粉色错版痕迹。字仍须完整，不能变成破碎噪点或难读的涂鸦。
- 从标题中选一个真正承载变化或冲突的 2–4 字短语，印在一条粗糙粉色墨带上，短语改用黑字。只强调一处。
- 墨带边缘可不齐，标题整体对齐、字距与行距必须有秩序。不要每个字单独旋转，也不要每行套卡片框。
- 标题应有与画面一致的印刷质感；避免直接贴一层毫无纹理的 UI 字。不得为了做旧牺牲中文准确性。

### 场景与复杂度

- 一个能被认出的主场景，加一个由输入走向产出的动作关系。会议可用桌椅、录音设备、纪要与待办；其他主题应换成相应的物件，不能硬套会议桌。
- 留白约占 30%–45%。主场景约占 40%–55%，标题占其余主要视觉面积，Logo 占宽约 3%–5%。比例是起点而非固定模板。
- 信息关系可以由纸张前后、一个短箭头、工具动作或对象重叠表达；避免复杂流程图和多卡片墙。
- 在具体与抽象之间取中间值：读者无需解释就能识别场景；删去不服务主题的细节。不要只画一个空洞符号，也不要塞满整间办公室。

### Agent 与品牌

- 当主题需要 Agent 参会、协作或执行时，可加入一个机器人。用户明确要求时必须加入；其他主题不自动放机器人。
- 机器人使用黑白影印金属质感、少量蓝色细节、克制的眼睛与机械结构。体型适中，姿势须与环境吻合；坐在椅子上时要看得出椅子承托和手臂接触桌面。
- 默认最多一个机器人，避免大头萌宠、悬浮半身像和抢占标题空间。
- 仅使用用户要求的品牌，优先接收原始 Logo 并作为输入参考。保持原形与留白；不要从示例图自动继承豆包工作品牌。

## 制作与迭代

1. 把文章压缩成一句关系句，选择一个能体现它的具体场景。
2. 确定标题断行、唯一强调词、主场景、关键动作与所需品牌。
3. 使用环境已有的图片生成能力，传入适用的参考资产。无法生图时说明能力缺口并交付提示词，不把设计规则当成图片服务。
4. 检查标题、纸面短标签、Logo、角色姿势、文字可读性，以及缩略图能否看懂主场景。
5. 用户认可布局后，只编辑指定元素。例如“字效更融合、加一个机器人”时，保留其余桌椅、文件、Logo 和场景关系。

使用如下提示词骨架，替换方括号内容：

```text
Create an original 2.35:1 Chinese editorial cover. Matte black paper field,
warm-ivory heavy condensed Chinese headline with restrained xerox grain,
ink erosion inside intact glyphs and very subtle spot-ink misregistration.
Exact headline: [verbatim title and line breaks]. Highlight only [keyword]
with black letters on one rough hot-pink printed strip.
One immediately recognizable scene: [scene and relevant objects].
Show [input -> action -> output] with one compact visual relation.
Use powder-blue for [one scene surface], black-and-white halftone photographic
cutouts for objects, and tiny hot-pink marks for [key action].
[Optional requested Agent: one small retro-industrial robot physically
seated/working in the scene, newspaper halftone, natural contact and posture.]
[Optional requested brand: use supplied logo, small and accurate.]
Generous black negative space, balanced title and scene, mature magazine
collage, no glow, no gradients, no glossy plastic, no unreadable distressed
characters, no icon grid, no irrelevant stickers or fine-print paragraphs.
```

## 用户反馈的处理

- “太抽象”：补回最少量、可识别的场景物件，仍保持单一关系。
- “太复杂”：先删除重复道具、说明字和装饰，不改变已认可的配色和材质。
- “字不融合”：调整字内颗粒、边缘侵蚀和油墨强调，不擅自重写标题。
- “加 Agent”：将机器人放进已有空间，避免另加漂浮徽章。
- “换颜色”：保留布局，只调整专色；“换风格”才重新选择材质与构图。
