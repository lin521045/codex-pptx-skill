# Codex PPTX Skill

Build, inspect, edit, and quality-check PowerPoint decks with Codex.

- Repository: [github.com/lin521045/codex-pptx-skill](https://github.com/lin521045/codex-pptx-skill)
- Installable skill path: `skills/pptx-codex/`

## What you get

- A drop-in Codex skill at `skills/pptx-codex/`
- Practical scripts for `.pptx` text extraction, rendering, unpacking, repacking, and placeholder checks
- A stronger presentation workflow: plan, build, inspect, fix, re-check
- Guidance for both template editing and from-scratch deck creation

## Intended use

Use this skill whenever a task involves:

- Creating a presentation from notes, Markdown, or a source brief
- Revising an existing `.pptx`
- Mining text or structure from a slide deck
- Using a branded template while preserving layouts
- Exporting slides to images for review

## Skill path

The installable skill lives here:

- `skills/pptx-codex/`

## Workflow overview

1. Read the input deck or source brief.
2. Decide whether to edit a template or generate a new deck.
3. Build slides with strong visual structure instead of plain bullet pages.
4. Render slides to images.
5. Run content and visual QA.
6. Fix issues and verify again.

## Key files

- `skills/pptx-codex/SKILL.md`
- `skills/pptx-codex/references/editing-workflow.md`
- `skills/pptx-codex/references/build-from-scratch.md`
- `skills/pptx-codex/references/design-playbook.md`

## Install

```powershell
Copy-Item -Recurse .\skills\pptx-codex "$env:CODEX_HOME\skills\pptx-codex"
python -m pip install -r requirements.txt
```

## More

- Full repository guide: [README.md](../README.md)
- Usage guide: [usage.md](usage.md)
