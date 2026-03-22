# Usage Guide

## 1. Install the skill

Copy `skills/pptx-codex` into your `$CODEX_HOME/skills` directory.

## 2. Install helpers

```powershell
python -m pip install -r requirements.txt
```

## 3. Common tasks

### Extract text

```powershell
python .\skills\pptx-codex\scripts\extract_text.py .\deck.pptx
```

### Check for leftover placeholders

```powershell
python .\skills\pptx-codex\scripts\check_placeholders.py .\deck.pptx
```

### Create slide thumbnails

```powershell
python .\skills\pptx-codex\scripts\thumbnail.py .\deck.pptx
```

### Unpack a deck for XML editing

```powershell
python .\skills\pptx-codex\scripts\office\unpack.py .\deck.pptx .\unpacked
```

### Repack the edited deck

```powershell
python .\skills\pptx-codex\scripts\office\pack.py .\unpacked .\output.pptx
```

## 4. Workflow choice

- If the user gives you an existing branded deck, use the template-editing workflow.
- If the user gives only notes or Markdown, use the from-scratch workflow.
- If the user wants review only, extract text, render thumbnails, and inspect.

## 5. Render backends

The render helper tries these options in order:

1. Microsoft PowerPoint automation on Windows
2. LibreOffice to PDF, then PDF-to-image rasterization with PyMuPDF

If neither is available, the script exits with a clear message telling you what is missing.

