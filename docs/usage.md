# 使用说明

## 1. 安装 skill

将 `skills/pptx-codex` 复制到你的 `$CODEX_HOME/skills` 目录。

## 2. 安装辅助依赖

```powershell
python -m pip install -r requirements.txt
```

## 3. 常见任务

### 抽取文本

```powershell
python .\skills\pptx-codex\scripts\extract_text.py .\deck.pptx
```

### 检查残留占位符

```powershell
python .\skills\pptx-codex\scripts\check_placeholders.py .\deck.pptx
```

### 生成缩略图拼板

```powershell
python .\skills\pptx-codex\scripts\thumbnail.py .\deck.pptx
```

### 解包 deck 以便 XML 编辑

```powershell
python .\skills\pptx-codex\scripts\office\unpack.py .\deck.pptx .\unpacked
```

### 重新打包 deck

```powershell
python .\skills\pptx-codex\scripts\office\pack.py .\unpacked .\output.pptx
```

## 4. 怎么选工作流

- 用户给了现成品牌模板或旧 deck：走模板编辑流程
- 用户只有笔记、提纲、Markdown 或 brief：走从零创建流程
- 用户只要你帮忙审阅：提取文本、生成缩略图、检查版式

## 5. 渲染后端

渲染脚本会按顺序尝试：

1. Windows 上的 Microsoft PowerPoint 自动化
2. LibreOffice 先转 PDF，再由 PyMuPDF 栅格化成图片

如果两者都不可用，脚本会明确告诉你缺了什么。

## 6. 推荐起手文件

首次上手可以直接从这些示例开始：

- `examples/source-brief-template.zh.md`
- `examples/first-ppt-workflow-template.zh.md`
- `examples/sample-codex-prompt.zh.md`
- `examples/starter-pptxgenjs.js`

运行 starter 示例：

```powershell
npm install pptxgenjs
node .\examples\starter-pptxgenjs.js
```

