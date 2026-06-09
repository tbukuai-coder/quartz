---
type: entity
category: dataset
tags: [pre-training, open-science, allenai, web-data, code, academic]
---

# Dolma

> AllenAI's **3 trillion token open pretraining corpus** — the first large-scale LLM training dataset released with full documentation, curation methodology, and data lineage, created alongside [[entities/models/olmo|OLMo]].

## Overview
Dolma (Data for OLMo) is a multi-source pretraining dataset created to enable fully reproducible LLM research. Unlike other pretraining datasets that are either proprietary (GPT-4, Gemini training data) or partially documented ([[entities/datasets/refinedweb|RefinedWeb]], [[entities/datasets/fineweb|FineWeb]]), Dolma provides both the data and complete documentation of every curation decision — filtering rules, deduplication methods, quality scoring, and composition rationale.

## Dataset Composition

| Source | Tokens | Description | Processing |
|---|---|---|---|
| **Common Crawl** | ~2.4T | Web text via CCNet pipeline | Language ID, quality filtering, deduplication |
| **Code** (GitHub, The Stack) | ~200B | Open-source code | License filtering, dedup |
| **Academic Papers** (peS2o) | ~57B | Semantic Scholar full-text papers | Parsed from PDF, cleaned |
| **Books** | ~18B | Project Gutenberg + other | Deduplication |
| **Wikipedia** | ~3.7B | English Wikipedia dumps | Cleaned, formatted |
| **Fandom** | ~4B | Fandom wiki dumps | Cleaned |
| **Reddit** (Pushshift) | ~80B | Reddit comments and posts | Filtered by subreddit quality |
| **Total** | **~3T** | | |

## Curation Methodology
Dolma's curation follows a principled pipeline:

1. **Language identification**: fastText-based filtering for English (Common Crawl)
2. **Quality filtering**: Perplexity-based and heuristic filters (document length, repetition, toxicity)
3. **Deduplication**: Both exact (URL-based for web) and fuzzy (MinHash for all sources)
4. **Mixing**: Proportions chosen based on ablation experiments with OLMo-1B
5. **Documentation**: Every filtering decision documented with rationale and impact metrics

## Usage in Models

| Model | Tokens Used | Source |
|---|---|---|
| [[entities/models/olmo\|OLMo-7B]] | 2.46T | Dolma |
| [[entities/models/olmo\|OLMo-1B]] | 3T | Dolma |
| [[sources/olmoe\|OLMoE-1B-7B]] | Part of 5T OLMoE-Mix | Dolma + DCLM + StarCoder |
| DCLM benchmark models | Various | Dolma components |

## Comparison with Other Pretraining Datasets

| Dataset | Tokens | Open | Sources | Curation Documented |
|---|---|---|---|---|
| **Dolma** | 3T | ✅ Fully | Web, code, academic, books, wiki | ✅ Fully |
| [[entities/datasets/refinedweb\|RefinedWeb]] | 5T | Partial (600B) | Web only | Partially |
| [[entities/datasets/fineweb\|FineWeb]] | 15T | ✅ Fully | Web only | ✅ Fully |
| RedPajama v2 | 30T | ✅ | Web, code, wiki, books, arxiv | Partially |
| Llama training data | ~2T | ❌ | Unknown | ❌ |

## Significance
Dolma's primary contribution is not raw scale but **transparency and reproducibility**:
- Enables studying how pretraining data composition affects model behavior
- Serves as the foundation for DCLM (DataComp for Language Models), a data curation benchmark
- peS2o component uniquely includes academic full-text, enabling scientific domain knowledge
- All processing code released alongside the data

## Related Papers
- [[sources/dolma]] — Dolma paper: design principles, curation, and ablations
- [[sources/olmo]] — OLMo (created Dolma as part of the project)
- [[sources/olmoe]] — OLMoE (uses Dolma as part of OLMoE-Mix)
- [[sources/refinedweb]] — RefinedWeb (web-only alternative)
- [[sources/fineweb]] — FineWeb (larger web corpus with educational subset)

## See Also
- [[entities/orgs/allenai]] — AllenAI (creator)
- [[entities/models/olmo]] — OLMo models trained on Dolma
- [[concepts/pre-training]] — Pre-training methodology
- [[comparisons/pretraining-data]] — Comparison of pretraining data strategies