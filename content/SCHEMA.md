# 📋 Wiki Schema — HF Papers Wiki

> This file defines the conventions, structure, and workflows for the Hugging Face Papers Wiki. It serves as the instruction manual for any LLM agent maintaining this wiki.

---

## Purpose

This wiki is a **persistent, compounding knowledge base** about the Hugging Face open-source ML ecosystem — its foundational papers, models, training techniques, datasets, and organizations. The LLM reads source papers, extracts key information, and integrates it into an evolving, interlinked collection of markdown pages.

## Directory Structure

```
wiki/
├── SCHEMA.md              # This file — conventions and workflows
├── index.md               # Content catalog — all pages with summaries
├── log.md                 # Chronological record of ingests/queries/maintenance
├── overview.md            # High-level synthesis of the entire wiki
│
├── sources/               # One page per ingested paper
│   ├── attention-is-all-you-need.md
│   ├── bert.md
│   └── ...
│
├── entities/              # Pages for specific named things
│   ├── models/            # Model families (LLaMA, Mistral, Qwen, etc.)
│   ├── datasets/          # Key datasets (RefinedWeb, UltraChat, OASST, etc.)
│   └── orgs/              # Organizations (Meta, Mistral AI, DeepSeek, etc.)
│
├── concepts/              # Pages for techniques, ideas, and methods
│   ├── transformer-architecture.md
│   ├── rlhf.md
│   ├── dpo.md
│   └── ...
│
└── comparisons/           # Side-by-side analyses
    └── ...
```

## Page Types

### Source Pages (`sources/`)
One page per ingested paper. Template:

```markdown
---
type: source
arxiv_id: "XXXX.XXXXX"
title: "Full Paper Title"
authors: ["Author1", "Author2"]
date: YYYY-MM-DD
org: "Organization"
tags: [tag1, tag2]
upvotes: N
---

# Paper Title

> One-sentence summary

## Key Contributions
- Bullet list of what this paper introduces

## Method
Brief description of the approach

## Results
Key benchmark results

## Datasets Used
- [[dataset-name]] — description

## Models Released
- [[model-name]] — description

## Connections
- Builds on: [[other-paper]]
- Cited by / Influenced: [[other-paper]]
- Related concepts: [[concept]]

## Citation
> Author et al., "Title," arXiv:XXXX.XXXXX, YYYY.
```

### Entity Pages (`entities/`)
Pages for specific models, datasets, or organizations. Template:

```markdown
---
type: entity
category: model|dataset|org
tags: [tag1, tag2]
---

# Entity Name

> One-sentence description

## Overview
What it is, why it matters

## Key Details
Technical specs, parameters, benchmarks

## Related Papers
- [[source-page]] — relationship

## See Also
- [[related-entity]]
- [[related-concept]]
```

### Concept Pages (`concepts/`)
Pages for techniques, methods, and ideas. Template:

```markdown
---
type: concept
tags: [tag1, tag2]
---

# Concept Name

> One-sentence definition

## Overview
What the concept is and why it matters

## How It Works
Technical explanation

## Key Papers
- [[source-page]] — introduced / advanced this concept

## Variants & Extensions
- Variant A — description
- Variant B — description

## See Also
- [[related-concept]]
```

## Cross-Reference Conventions

- Use `[[page-name]]` wiki-link syntax (Obsidian-compatible)
- Links are relative file paths without extensions: `[[sources/attention-is-all-you-need]]`
- When referencing a paper inline, use: `[[sources/paper-slug|Short Name]]`
- When referencing a concept, use: `[[concepts/concept-slug|Display Name]]`
- When referencing an entity, use: `[[entities/category/slug|Display Name]]`

## Frontmatter

Every page has YAML frontmatter with at minimum:
- `type`: source | entity | concept | comparison
- `tags`: list of relevant tags

Source pages additionally have: `arxiv_id`, `title`, `authors`, `date`, `org`, `upvotes`

## Workflows

### Ingest a New Paper
1. Read the paper (abstract, key sections)
2. Create a source page in `sources/`
3. Update or create relevant entity pages (models, datasets, orgs)
4. Update or create relevant concept pages
5. Add cross-references between all touched pages
6. Update `index.md` with the new page and summary
7. Append an entry to `log.md`

### Answer a Query
1. Read `index.md` to find relevant pages
2. Read those pages
3. Synthesize an answer with `[[citations]]`
4. If the answer is substantial, file it as a new page (comparison, analysis)
5. Update `index.md` and `log.md`

### Lint / Health Check
1. Check for orphan pages (no inbound links)
2. Check for broken links
3. Check for contradictions between pages
4. Check for stale information
5. Suggest new pages that should exist
6. Suggest new sources to ingest

## Tags Vocabulary

### Domains
`nlp`, `vision`, `multimodal`, `code`, `math`, `robotics`, `speech`

### Methods
`pre-training`, `fine-tuning`, `alignment`, `rlhf`, `dpo`, `sft`, `distillation`, `quantization`, `moe`, `peft`

### Scale
`small-model`, `medium-model`, `large-model`, `frontier-model`

### Era
`foundational`, `2023`, `2024`, `2025`
