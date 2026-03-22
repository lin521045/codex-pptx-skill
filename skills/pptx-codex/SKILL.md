---
name: pptx-codex
description: Create, inspect, edit, and quality-check PowerPoint presentations. Use when a task mentions slides, decks, presentations, pitch decks, speaker notes, templates, or any .pptx file as input or output. Trigger this skill for reading text from existing decks, revising branded templates, exporting slides to images for review, scanning for leftover placeholders, or creating a new presentation from notes with code.
---

# PPTX for Codex

## Overview

Use this skill to turn Codex into a practical presentation agent. It supports three main modes: reading an existing deck, editing a template safely, and creating a deck from scratch with a stronger design and QA process than a generic outline-to-bullets workflow.

## Quick Start

| Task | Command or guide |
| --- | --- |
| Extract text from a deck | `python scripts/extract_text.py path/to/deck.pptx` |
| Build a visual contact sheet | `python scripts/thumbnail.py path/to/deck.pptx` |
| Check for placeholder text | `python scripts/check_placeholders.py path/to/deck.pptx` |
| Unpack a deck to editable XML | `python scripts/office/unpack.py deck.pptx unpacked/` |
| Repack an edited deck | `python scripts/office/pack.py unpacked/ output.pptx` |
| Edit an existing template | Read [references/editing-workflow.md](references/editing-workflow.md) |
| Create a deck from scratch | Read [references/build-from-scratch.md](references/build-from-scratch.md) |
| Pick a visual direction | Read [references/design-playbook.md](references/design-playbook.md) |

## Workflow Decision

Use this decision path:

1. If the user provides an existing `.pptx`, inspect it first with `extract_text.py` and `thumbnail.py`.
2. If the existing deck already has the right visual language, use the template-editing workflow.
3. If there is no usable template, use the from-scratch workflow and write code to generate the deck.
4. In every case, run a QA pass before declaring success.

## Reading and Inspection

When a `.pptx` is input-only:

```bash
python scripts/extract_text.py presentation.pptx
python scripts/thumbnail.py presentation.pptx
```

Use the text extract to understand structure, titles, bullets, tables, and notes. Use rendered images or the contact sheet to understand layout variety, spacing, contrast, and density.

## Template Editing

For branded or reference decks, unpack the `.pptx`, make structural edits, edit slide XML, clean the unpacked folder, then repack it. Read [references/editing-workflow.md](references/editing-workflow.md) before touching XML.

## Creating from Scratch

When there is no suitable starting deck, generate the presentation from code. Prefer PptxGenJS for from-scratch deck generation because it is expressive enough for cards, shapes, charts, and repeatable visual systems. Read [references/build-from-scratch.md](references/build-from-scratch.md) before implementing.

## Design Standard

Avoid flat "title + five bullets" decks. Every slide should have a clear purpose, a deliberate layout, and at least one visual anchor such as an image, chart, metric card, icon row, timeline, or contrast block.

Before building, choose:

- One dominant color and one or two support colors
- A typography pairing with clear title/body contrast
- A repeated visual motif across the deck
- Two or three layout patterns to alternate across slides

Read [references/design-playbook.md](references/design-playbook.md) for concrete palettes, layout patterns, and spacing rules.

## QA Is Required

Never stop at the first working export. Treat QA as a bug hunt.

Content QA:

```bash
python scripts/extract_text.py output.pptx
python scripts/check_placeholders.py output.pptx
```

Visual QA:

1. Render the deck to slide images.
2. Inspect for overlap, cut-off text, weak contrast, cramped spacing, inconsistent alignment, and leftover template content.
3. Fix issues.
4. Re-render and check again.

If your environment supports a second reviewer, use a fresh review pass after the first fix cycle. Otherwise do a second manual pass after a short break.

## References

- [references/editing-workflow.md](references/editing-workflow.md)
- [references/build-from-scratch.md](references/build-from-scratch.md)
- [references/design-playbook.md](references/design-playbook.md)
