# pptx-codex

[![CI](https://github.com/lin521045/codex-pptx-skill/actions/workflows/validate.yml/badge.svg)](https://github.com/lin521045/codex-pptx-skill/actions/workflows/validate.yml)
[![Docs](https://img.shields.io/badge/docs-GitHub%20Pages-0A66C2)](https://lin521045.github.io/codex-pptx-skill/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

```bash
npx skills add https://github.com/lin521045/codex-pptx-skill --skill pptx-codex
```

## 摘要

创建、编辑、读取和处理 PowerPoint 演示文稿，并提供设计指导与质量保证流程。

- 支持三条主要工作流：读取/提取现有 `.pptx` 文本、通过模板解包与重打包编辑演示文稿、使用 PptxGenJS 从零创建 deck
- 提供 10 组配色和字体搭配建议，避免做出通用 AI 幻灯片风格，并给出版式模式、间距和对比度规则
- 提供强制 QA 流程：占位符检查、缩略图/单页渲染、视觉复核，以及适配 Codex 的二轮检查流程
- 提供文本提取、缩略图生成、XML 解包、复制 slide、清理关系、PDF/图片导出等工具

## SKILL.md

入口文件：[`skills/pptx-codex/SKILL.md`](skills/pptx-codex/SKILL.md)

## 快速参考

| 任务 | 指南 |
| --- | --- |
| 阅读/分析内容 | `python skills/pptx-codex/scripts/extract_text.py presentation.pptx` |
| 编辑或基于模板创建 | 阅读 [`skills/pptx-codex/editing.md`](skills/pptx-codex/editing.md) |
| 从零创建 | 阅读 [`skills/pptx-codex/pptxgenjs.md`](skills/pptx-codex/pptxgenjs.md) |

---

## 读取内容

```bash
# 文本提取
python skills/pptx-codex/scripts/extract_text.py presentation.pptx

# 可视化缩略总览
python skills/pptx-codex/scripts/thumbnail.py presentation.pptx

# 原始 XML
python skills/pptx-codex/scripts/office/unpack.py presentation.pptx unpacked/
```

如需和参考 skill 保持接近的使用方式，并且本地已安装 `markitdown[pptx]`：

```bash
python -m markitdown presentation.pptx
```

---

## 编辑工作流

完整说明见 [`skills/pptx-codex/editing.md`](skills/pptx-codex/editing.md)。

1. 用 `thumbnail.py` 分析模板
2. 解包
3. 操作 slide 结构
4. 编辑内容
5. 清理
6. 重新打包
7. 执行 QA

---

## 从零创建

完整说明见 [`skills/pptx-codex/pptxgenjs.md`](skills/pptx-codex/pptxgenjs.md)。

当没有模板或参考 deck 时，使用 PptxGenJS 从零创建。

---

## 设计思路

不要做无聊的 PPT。白底 bullet 页不适合答辩、汇报或路演。

### 开始前

- 选择与内容高度相关的主配色，而不是默认蓝色
- 一个颜色占主导，其他颜色只做辅助
- 决定深浅结构：深色封面/结尾 + 浅色正文，或整套深色
- 选择一个能贯穿整套 deck 的视觉母题

### 配色方案

| 主题 | 主色 | 辅色 | 强调色 |
| --- | --- | --- | --- |
| 午夜行政风 | `1E2761` | `CADCFC` | `FFFFFF` |
| 森林与苔藓 | `2C5F2D` | `97BC62` | `F5F5F5` |
| 珊瑚能量 | `F96167` | `F9E795` | `2F3C7E` |
| 暖陶土 | `B85042` | `E7E8D1` | `A7BEAE` |
| 海洋渐层 | `065A82` | `1C7293` | `21295C` |
| 木炭极简 | `36454F` | `F2F2F2` | `212121` |
| 青柠信任感 | `028090` | `00A896` | `02C39A` |
| 莓果奶油 | `6D2E46` | `A26769` | `ECE2D0` |
| 鼠尾草宁静 | `84B59F` | `69A297` | `50808E` |
| 樱桃强对比 | `990011` | `FCF6F5` | `2F3C7E` |

### 每页建议

- 双栏布局
- 图标 + 文本行
- 2x2 / 2x3 卡片网格
- 半出血图片
- 大数字指标
- 对比页
- 时间线 / 流程页

### 字体

| 标题字体 | 正文字体 |
| --- | --- |
| Georgia | Calibri |
| Arial Black | Arial |
| Calibri | Calibri Light |
| Cambria | Calibri |
| Trebuchet MS | Calibri |
| Impact | Arial |
| Palatino | Garamond |
| Consolas | Calibri |

| 元素 | 尺寸 |
| --- | --- |
| 幻灯片标题 | 36-44pt 粗体 |
| 分区标题 | 20-24pt 粗体 |
| 正文 | 14-16pt |
| 注释 | 10-12pt |

### 间距

- 最小边距 `0.5"`
- 内容块之间 `0.3-0.5"`
- 保留呼吸感，不要塞满

### 避免

- 整套使用同一种布局
- 大段正文居中
- 标题和正文没有明显字号对比
- 默认蓝白配色
- 标题下加装饰线
- 纯文字页
- 忽略文本框 padding
- 低对比文字和图标

---

## QA（必须）

默认第一页导出一定有问题，QA 要按“找 bug”思路进行。

### 内容 QA

```bash
python skills/pptx-codex/scripts/extract_text.py output.pptx
python skills/pptx-codex/scripts/check_placeholders.py output.pptx
```

可选：

```bash
python -m markitdown output.pptx
```

### 视觉 QA

将 slide 导出成图片后逐页检查：

- 元素重叠
- 文本裁切或溢出
- 页边距不足
- 卡片间距过近
- 左右未对齐
- 文本/图标对比不足
- 仍有占位内容

Codex 版说明：

- 只有在用户明确允许多代理时，才用子代理做第二轮视觉审查
- 否则执行双轮人工复核

### 验证循环

1. 生成 slides
2. 转图片
3. 列问题
4. 修复
5. 复查
6. 直到不再出现新问题

---

## 转换为图片

```bash
python skills/pptx-codex/scripts/office/soffice.py --headless --convert-to pdf output.pptx
python skills/pptx-codex/scripts/office/render.py output.pptx rendered/
```

或直接：

```bash
python skills/pptx-codex/scripts/thumbnail.py output.pptx
```

---

## 依赖

- `pip install "markitdown[pptx]"`：可选文本抽取
- `pip install Pillow`：缩略图拼板
- `pip install PyMuPDF`：PDF 栅格化
- `npm install pptxgenjs`：从零创建
- LibreOffice `soffice`：PDF 转换
- Microsoft PowerPoint（Windows，可选）：PDF 导出和高保真渲染

---

## 仓库入口

- 仓库：[github.com/lin521045/codex-pptx-skill](https://github.com/lin521045/codex-pptx-skill)
- 文档页：[lin521045.github.io/codex-pptx-skill](https://lin521045.github.io/codex-pptx-skill/)
- 技能目录：[`skills/pptx-codex`](skills/pptx-codex)

