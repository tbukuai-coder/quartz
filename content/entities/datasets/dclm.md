---
type: entity
category: dataset
tags: [pre-training, open-science, data-curation, allenai, benchmark]
---

# DCLM (DataComp for Language Models)

> A **benchmark and framework for data curation** that evaluates how different data filtering strategies affect LLM quality — built on [[entities/models/olmo|OLMo]] and [[entities/datasets/dolma|Dolma]], enabling systematic study of pretraining data quality.

## Overview
DCLM applies the DataComp methodology to language model pretraining. It fixes the model architecture and training recipe (using OLMo) and varies only the data — enabling controlled experiments that isolate the effect of data curation decisions.

## How It Works
1. **Fixed model**: OLMo architecture (1B or 7B) with fixed hyperparameters
2. **Fixed compute**: Same training budget across all experiments
3. **Variable data**: Researchers submit different filtering strategies
4. **Evaluation**: Standardized evaluation suite

## Dataset Scale
- **DCLM-Pool**: 240T tokens of raw Common Crawl data
- **DCLM-Baseline**: 4T curated tokens (best filtering strategy)
- Components from: [[entities/datasets/dolma|Dolma]], Common Crawl, StarCoder, peS2o

## Key Findings
- Data curation shows 10+ point differences on downstream benchmarks
- Perplexity-based filtering is highly effective
- Deduplication provides consistent gains
- Combining multiple filtering strategies is best

## Related Papers
- [[sources/olmo]] — OLMo (model used for experiments)
- [[sources/olmoe]] — OLMoE (uses DCLM data)
- [[sources/fineweb]] — FineWeb (complementary approach)

## See Also
- [[entities/orgs/allenai]] — AllenAI (creator)
- [[entities/datasets/dolma]] — Dolma (data source)
- [[comparisons/pretraining-data]] — Pretraining data strategies