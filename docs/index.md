# Codex PPTX Skill

用 Codex 构建、检查、编辑和质检 PowerPoint 演示文稿。

- 仓库地址：[github.com/lin521045/codex-pptx-skill](https://github.com/lin521045/codex-pptx-skill)
- 可安装 skill 路径：`skills/pptx-codex/`

## 你会得到什么

- 一个可以直接放进 Codex 的 skill：`skills/pptx-codex/`
- 一组实用脚本：文本提取、slide 渲染、解包、重打包、占位符扫描
- 一套更完整的 PPT 工作流：规划、构建、审阅、修复、复核
- 两种主要模式的说明：模板编辑、从零创建

## 适用场景

当任务涉及以下内容时，都建议使用这个 skill：

- 根据 Markdown、会议纪要、brief 或研究内容生成演示文稿
- 修改或续写已有 `.pptx`
- 从 PPT 中抽取结构、文本、标题或表格信息
- 在品牌模板或历史 deck 的基础上更新内容
- 将 slide 导出为图片做视觉检查

## 工作流概览

1. 读取输入 deck 或 source brief。
2. 判断是基于模板编辑，还是从零创建。
3. 按视觉结构而不是纯 bullet 文本去设计每一页。
4. 渲染为图片进行检查。
5. 执行内容 QA 和视觉 QA。
6. 修复后再次验证。

## 关键文件

- `skills/pptx-codex/SKILL.md`
- `skills/pptx-codex/references/editing-workflow.md`
- `skills/pptx-codex/references/build-from-scratch.md`
- `skills/pptx-codex/references/design-playbook.md`
- `examples/first-ppt-workflow-template.zh.md`

## 快速安装

```powershell
Copy-Item -Recurse .\skills\pptx-codex "$env:CODEX_HOME\skills\pptx-codex"
python -m pip install -r requirements.txt
```

## 快速查看

- 总说明：[README.md](../README.md)
- 使用文档：[usage.md](usage.md)
