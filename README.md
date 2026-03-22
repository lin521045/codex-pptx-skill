# Codex PPTX Skill

[![CI](https://github.com/lin521045/codex-pptx-skill/actions/workflows/validate.yml/badge.svg)](https://github.com/lin521045/codex-pptx-skill/actions/workflows/validate.yml)
[![Docs](https://img.shields.io/badge/docs-GitHub%20Pages-0A66C2)](https://lin521045.github.io/codex-pptx-skill/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

`codex-pptx-skill` is a public repository that packages a reusable Codex skill for PowerPoint work. It is designed to feel close to Anthropic's public `pptx` skill in capability, while being an original implementation that can be installed and used in Codex.

This repository contains:

- A Codex-ready skill folder at `skills/pptx-codex/`
- Helper scripts for extracting text, unpacking/repacking decks, rendering slides to images, building thumbnail sheets, and scanning for placeholder content
- Reference guides for template-based editing, from-scratch deck creation, design direction, and QA
- Project-level documentation for installation, structure, and usage

## Why this project exists

The public Anthropic `pptx` skill page shows a strong workflow for presentation work: read the deck, inspect layouts, edit templates safely, create new decks with code, and run a strict QA pass. This repository recreates that *experience and workflow shape* for Codex without copying upstream proprietary skill contents.

## Repository layout

```text
.
|- README.md
|- requirements.txt
|- docs/
|  |- _config.yml
|  |- index.md
|  `- usage.md
|- examples/
|  `- source-brief-template.md
`- skills/
   `- pptx-codex/
      |- SKILL.md
      |- agents/openai.yaml
      |- references/
      `- scripts/
```

## Install in Codex

1. Clone this repository.
2. Copy [skills/pptx-codex](skills/pptx-codex) into your `$CODEX_HOME/skills/` directory.
3. Make sure the folder name stays `pptx-codex`.

On Windows PowerShell:

```powershell
Copy-Item -Recurse .\skills\pptx-codex "$env:CODEX_HOME\skills\pptx-codex"
```

## Python dependencies

The helper scripts use Python packages that are easy to install in a local environment:

```powershell
python -m pip install -r requirements.txt
```

Optional tools:

- Microsoft PowerPoint on Windows for the highest-fidelity slide image export
- LibreOffice for PDF conversion when PowerPoint is unavailable

## What the skill does

- Read and summarize existing `.pptx` files
- Export slide images and create contact sheets for layout review
- Unpack a presentation into editable XML
- Duplicate and clean slide structures during template-based editing
- Repack an edited deck into a valid `.pptx`
- Check for leftover placeholders before delivery
- Guide Codex through from-scratch deck generation with PptxGenJS
- Enforce a stronger design and QA process than a generic "title + bullets" workflow

## Quick commands

```powershell
python .\skills\pptx-codex\scripts\extract_text.py .\deck.pptx
python .\skills\pptx-codex\scripts\thumbnail.py .\deck.pptx
python .\skills\pptx-codex\scripts\check_placeholders.py .\deck.pptx
python .\skills\pptx-codex\scripts\office\unpack.py .\deck.pptx .\unpacked
python .\skills\pptx-codex\scripts\office\pack.py .\unpacked .\output.pptx
```

## Documentation

- Project homepage: [docs/index.md](docs/index.md)
- Usage guide: [docs/usage.md](docs/usage.md)
- Skill entrypoint: [skills/pptx-codex/SKILL.md](skills/pptx-codex/SKILL.md)

## Notes

This repository is an original Codex-oriented implementation inspired by the public capability outline of Anthropic's `pptx` skill page at [skills.sh](https://skills.sh/anthropics/skills/pptx). The upstream skill materials are marked proprietary, so this repository does not redistribute or copy those assets.
