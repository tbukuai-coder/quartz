---
type: entity
category: org
tags: [tii, falcon, pre-training, open-source, uae]
---

# TII (Technology Innovation Institute)

> A UAE-based research institute that created **Falcon**, one of the first high-quality open models to challenge LLaMA — demonstrating that web-only pretraining data ([[entities/datasets/refinedweb|RefinedWeb]]) can match curated corpora.

## Overview
TII entered the LLM space with Falcon in 2023. Their key contribution: properly filtered web-only data can produce models competitive with those trained on diverse curated corpora. Falcon-40B briefly topped the HF Open LLM Leaderboard.

## Models
- **Falcon-7B** (2023) — Competitive with LLaMA-7B
- **Falcon-40B** (2023) — Briefly #1 on HF Leaderboard
- **Falcon-180B** (2023) — Largest open model at release
- **Falcon-2** (2024) — Updated with VLM capabilities

## Data
- [[entities/datasets/refinedweb|RefinedWeb]] — 5T token web-only dataset (600B released)

## Key Insight
**Data quality > data diversity**: well-filtered web-only corpus matches multi-source corpora.

## Papers in This Wiki
- [[sources/refinedweb]] — RefinedWeb dataset

## See Also
- [[entities/models/falcon]] — Falcon model family (detailed)
- [[entities/datasets/refinedweb]] — RefinedWeb dataset
- [[comparisons/pretraining-data]] — Data strategies comparison