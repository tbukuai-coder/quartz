---
type: entity
category: dataset
tags: [pre-training, open-source, web-data, multi-source]
---

# RedPajama

> A community-driven **open reproduction of LLaMA's training data** — one of the largest openly available pretraining datasets, enabling truly open model training.

## Versions

### v1 (2023) — 1.2T tokens
Direct LLaMA data recipe reproduction from open sources:

| Source | Tokens | % |
|---|---|---|
| Common Crawl | 878B | 67% |
| C4 | 175B | 15% |
| GitHub | 59B | 4.5% |
| Wikipedia | 24B | 2.5% |
| Books | 26B | 2% |
| ArXiv | 28B | 2.5% |
| StackExchange | 20B | 2% |

### v2 (2023) — 30T tokens
Massive raw web dataset with quality signals (perplexity, dedup, language ID). Users apply their own filters.

## Models Trained
- **RedPajama-INCITE** (3B, 7B) — Together AI
- **OpenLLaMA** (3B, 7B, 13B) — Berkeley AI

## Significance
Showed LLaMA's data recipe could be reproduced from public sources at trillion-token scale.

## See Also
- [[entities/orgs/together-ai]] — Together AI (creator)
- [[entities/datasets/dolma]] — AllenAI's multi-source alternative
- [[entities/datasets/fineweb]] — HF's web-only dataset
- [[comparisons/pretraining-data]] — Data strategies