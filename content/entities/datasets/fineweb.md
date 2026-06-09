---
type: entity
category: dataset
tags: [pre-training, data-curation, huggingface]
---

# FineWeb / FineWeb-Edu

> The **largest high-quality open pretraining datasets** — FineWeb (15T tokens) and FineWeb-Edu (1.3T tokens of educational content) from Hugging Face. Produced through a rigorously ablated curation pipeline from 96 Common Crawl snapshots.

## Overview
FineWeb represents the state of the art in open pretraining data curation. It combines careful text extraction, deduplication, heuristic filtering, and LLM-based educational quality classification to produce datasets that consistently outperform all other open pretraining corpora.

## Variants

| Dataset | Size | Description | HF Repo |
|---|---|---|---|
| FineWeb | 15T tokens | Full filtered dataset from 96 CC snapshots | `HuggingFaceFW/fineweb` |
| FineWeb-Edu | 1.3T tokens | Educational content filtered (score ≥ 3) | `HuggingFaceFW/fineweb-edu` |
| FineWeb-Edu-score-2 | 5.4T tokens | Broader educational filter (score ≥ 2) | `HuggingFaceFW/fineweb-edu-score-2` |
| FineWeb2 | Multi-lingual | Multilingual extension | `HuggingFaceFW/fineweb-2` |

## Key Properties
- **Text extraction**: trafilatura on WARC (not WET) — 2-3% benchmark improvement
- **Deduplication**: MinHash with 5-grams and 112 hash functions, per-snapshot
- **Educational filtering**: LLM-trained quality classifier scores documents 0–5
- **Fully open**: Data, code, classifier, and all ablation models released
- **License**: ODC-By v1.0

## Used By
- [[sources/smollm2|SmolLM2]] — pretraining data
- Widely used by community for pretraining experiments

## Related Papers
- [[sources/fineweb]] — FineWeb technical report
- [[sources/refinedweb]] — earlier web data curation (FineWeb builds on this)
- [[sources/scaling-data-constrained]] — data quality and scaling

## See Also
- [[entities/datasets/refinedweb]]
- [[entities/orgs/huggingface]]
- [[concepts/pre-training]]
