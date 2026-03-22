# pptx-codex

```bash
npx skills add https://github.com/lin521045/codex-pptx-skill --skill pptx-codex
```

## 摘要

创建、编辑、读取和处理 PowerPoint 演示文稿，并提供设计指导与质量保证流程。

- 支持三条主要工作流：读取/提取现有 `.pptx` 文本、通过模板解包与重打包编辑演示文稿、使用 PptxGenJS 从零创建 deck
- 提供设计指导、颜色方案、字体搭配、版式模式、间距规则和视觉 QA 流程
- 包含文本提取、缩略图生成、XML 解包、复制 slide、清理、重打包、PDF/图片导出等辅助脚本
- 这是面向 Codex 的中文版本，保留与参考 `pptx` skill 接近的内容结构与能力边界

## SKILL.md

- [`skills/pptx-codex/SKILL.md`](../skills/pptx-codex/SKILL.md)

## 快速参考

| 任务 | 指南 |
| --- | --- |
| 阅读/分析内容 | `python skills/pptx-codex/scripts/extract_text.py presentation.pptx` |
| 编辑或基于模板创建 | [`skills/pptx-codex/editing.md`](../skills/pptx-codex/editing.md) |
| 从零创建 | [`skills/pptx-codex/pptxgenjs.md`](../skills/pptx-codex/pptxgenjs.md) |

---

## 读取内容

```bash
python skills/pptx-codex/scripts/extract_text.py presentation.pptx
python skills/pptx-codex/scripts/thumbnail.py presentation.pptx
python skills/pptx-codex/scripts/office/unpack.py presentation.pptx unpacked/
```

---

## 编辑工作流

1. 用 `thumbnail.py` 分析模板布局
2. 解包 PPTX
3. 先完成 slide 结构操作
4. 再编辑内容
5. 清理无用关系
6. 重打包
7. QA

完整说明见 [`editing.md`](../skills/pptx-codex/editing.md)。

---

## 从零创建

当没有模板或参考 deck 时，使用 PptxGenJS 从零生成。完整说明见 [`pptxgenjs.md`](../skills/pptx-codex/pptxgenjs.md)。

---

## 设计思路

不要做无聊的 PPT。白底 bullet 页不适合正式答辩或汇报。

### 开始前

- 选定主配色
- 选定标题/正文字体配对
- 选定贯穿全套 deck 的视觉母题
- 决定两到三种轮换使用的布局模式

### 推荐配色

- 午夜行政风：`1E2761 / CADCFC / FFFFFF`
- 森林与苔藓：`2C5F2D / 97BC62 / F5F5F5`
- 珊瑚能量：`F96167 / F9E795 / 2F3C7E`
- 暖陶土：`B85042 / E7E8D1 / A7BEAE`
- 海洋渐层：`065A82 / 1C7293 / 21295C`

### 推荐版式

- 双栏图文
- 卡片网格
- 大数字指标
- 对比页
- 流程页
- 半出血图片页

---

## QA（必须）

### 内容 QA

```bash
python skills/pptx-codex/scripts/extract_text.py output.pptx
python skills/pptx-codex/scripts/check_placeholders.py output.pptx
```

### 视觉 QA

将幻灯片渲染为图片后检查：

- 重叠
- 溢出
- 边距不足
- 间距失衡
- 对比不足
- 占位符残留

### 验证循环

1. 生成
2. 转图片
3. 检查
4. 修复
5. 复查

---

## 转换为图片

```bash
python skills/pptx-codex/scripts/office/soffice.py --headless --convert-to pdf output.pptx
python skills/pptx-codex/scripts/office/render.py output.pptx rendered/
```

---

## 依赖

- `markitdown[pptx]`
- `Pillow`
- `PyMuPDF`
- `pptxgenjs`
- `soffice` 或 PowerPoint

---

## 仓库

- GitHub：[lin521045/codex-pptx-skill](https://github.com/lin521045/codex-pptx-skill)
- 技能目录：[`skills/pptx-codex`](../skills/pptx-codex)

