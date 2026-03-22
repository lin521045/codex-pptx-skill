# Codex PPTX Skill

[![CI](https://github.com/lin521045/codex-pptx-skill/actions/workflows/validate.yml/badge.svg)](https://github.com/lin521045/codex-pptx-skill/actions/workflows/validate.yml)
[![Docs](https://img.shields.io/badge/docs-GitHub%20Pages-0A66C2)](https://lin521045.github.io/codex-pptx-skill/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

面向 Codex 的 PowerPoint/PPTX 技能仓库。它的目标不是只提供一个“生成 PPT”的提示词，而是提供一整套可复用的工作流：读取现有 `.pptx`、基于模板安全编辑、从零生成新 deck、导出图片做视觉检查、扫描占位符、以及执行完整 QA。

这个项目参考了 Anthropic 公共 `pptx` skill 展示出来的能力边界与工作流形态，但仓库内容为面向 Codex 的原创实现，不直接复制上游专有材料。

## 快速入口

- GitHub 仓库：[lin521045/codex-pptx-skill](https://github.com/lin521045/codex-pptx-skill)
- 项目首页：[lin521045.github.io/codex-pptx-skill](https://lin521045.github.io/codex-pptx-skill/)
- 可安装 skill：[`skills/pptx-codex`](skills/pptx-codex)
- Skill 入口说明：[`skills/pptx-codex/SKILL.md`](skills/pptx-codex/SKILL.md)
- 第一份示例工作流模板：[`examples/first-ppt-workflow-template.zh.md`](examples/first-ppt-workflow-template.zh.md)

## 这个仓库解决什么问题

很多“AI 生成 PPT”方案只会产出一份普通大纲，最后仍然需要人工返工样式、结构和细节。这个仓库把 PPT 任务拆成了可执行的工程流程：

- 先读 deck，再决定是“模板编辑”还是“从零创建”
- 用脚本处理 `.pptx` 的提取、解包、重打包和渲染
- 明确要求视觉检查，而不是只看文字是否齐全
- 保留设计 playbook，避免做出千篇一律的 AI 幻灯片

## 主要能力

- 读取和抽取现有 `.pptx` 内容
- 导出单页图片和缩略图拼板，便于快速审阅版式
- 解包 `.pptx` 为可编辑 XML，并重新打包回有效文件
- 在模板改版场景下复制 slide、清理孤儿文件、检查残留占位符
- 指导 Codex 用 PptxGenJS 从零创建 deck
- 用设计规范和 QA 流程约束输出质量

## 仓库结构

```text
.
|- README.md
|- requirements.txt
|- docs/
|  |- _config.yml
|  |- index.md
|  `- usage.md
|- examples/
|  |- first-ppt-workflow-template.zh.md
|  |- sample-codex-prompt.zh.md
|  |- source-brief-template.md
|  |- source-brief-template.zh.md
|  `- starter-pptxgenjs.js
|- tools/
|  `- validate_skill.py
`- skills/
   `- pptx-codex/
      |- SKILL.md
      |- agents/openai.yaml
      |- references/
      `- scripts/
```

## 安装到 Codex

1. 克隆本仓库。
2. 将 [`skills/pptx-codex`](skills/pptx-codex) 复制到 `$CODEX_HOME/skills/`。
3. 保持目录名为 `pptx-codex`。

Windows PowerShell:

```powershell
Copy-Item -Recurse .\skills\pptx-codex "$env:CODEX_HOME\skills\pptx-codex"
```

## 安装依赖

```powershell
python -m pip install -r requirements.txt
```

可选工具：

- Windows 上的 Microsoft PowerPoint：用于高保真导出 slide 图片
- LibreOffice：在没有 PowerPoint 时可作为 PDF 渲染后备方案

## 常用命令

```powershell
python .\skills\pptx-codex\scripts\extract_text.py .\deck.pptx
python .\skills\pptx-codex\scripts\thumbnail.py .\deck.pptx
python .\skills\pptx-codex\scripts\check_placeholders.py .\deck.pptx
python .\skills\pptx-codex\scripts\office\unpack.py .\deck.pptx .\unpacked
python .\skills\pptx-codex\scripts\office\pack.py .\unpacked .\output.pptx
```

## 推荐工作流

1. 用 `extract_text.py` 和 `thumbnail.py` 看清输入 deck。
2. 判断是沿用模板，还是从零创建。
3. 先做结构，再填内容，再跑视觉 QA。
4. 输出前必须执行占位符检查和二次复核。

## 示例文件

仓库已经放入一套“首份示例 PPT 工作流模板”：

- [`examples/first-ppt-workflow-template.zh.md`](examples/first-ppt-workflow-template.zh.md)
- [`examples/sample-codex-prompt.zh.md`](examples/sample-codex-prompt.zh.md)
- [`examples/source-brief-template.zh.md`](examples/source-brief-template.zh.md)
- [`examples/starter-pptxgenjs.js`](examples/starter-pptxgenjs.js)

如果你想直接运行 starter 脚本：

```powershell
npm install pptxgenjs
node .\examples\starter-pptxgenjs.js
```

它们可以直接作为：

- 给 Codex 的首轮任务模板
- 项目立项时的 PPT brief 模板
- 从零生成 deck 的 starter 文件

## 文档

- 项目首页：[`docs/index.md`](docs/index.md)
- 使用说明：[`docs/usage.md`](docs/usage.md)
- Skill 入口：[`skills/pptx-codex/SKILL.md`](skills/pptx-codex/SKILL.md)

## 验证状态

本仓库已经完成以下验证：

- skill frontmatter 校验通过
- helper scripts 语法校验通过
- 本地链路验证通过：文本提取、占位符检查、解包、复制 slide、清理、重打包、渲染、缩略图生成
- GitHub Actions 工作流已通过
- GitHub Pages 已启用

## English Summary

`codex-pptx-skill` is a Codex-ready public skill for PowerPoint work. It supports reading `.pptx` files, editing template decks safely, generating decks from scratch, exporting slide images, checking placeholders, and enforcing a stronger design/QA workflow. The repository is inspired by the public capability outline of Anthropic's `pptx` skill, but the contents here are original and openly published under MIT.
