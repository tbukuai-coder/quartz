---
type: source
arxiv_id: "2406.11794"
title: "DataComp-LM: In search of the next generation of training sets for language models"
authors: ["Jeffrey Li", "Alex Fang", "et al."]
date: 2024-06-17
org: "Multi-institutional (DataComp)"
tags: [data-curation, pre-training, benchmark, 2024]
upvotes: 55
---

# DCLM: DataComp for Language Models

> A **benchmark for data curation** — providing a standardized 240T token Common Crawl corpus, evaluation suite, and recipes for systematically comparing data curation strategies. DCLM-Baseline (model-based filtering) produces a 7B model matching Mistral-7B quality. 1.4K GitHub stars.

## Key Contributions
- **Standardized data curation benchmark**: Fixed corpus + recipes + evaluations for controlled experiments
- **240T token corpus**: Extracted from Common Crawl with standardized processing
- **DCLM-Baseline**: Model-based filtering produces highest quality open pretraining data (at release)
- **53 downstream evaluations**: Comprehensive eval suite for data curation experiments
- **Scaling validation**: Results validated at 400M, 1B, and 7B model scales

## Method
### The DCLM Benchmark
```
Raw Common Crawl (240T tokens)
  → Participant applies curation strategy
    → Train model with standardized recipe (OpenLM)
      → Evaluate on 53 benchmarks
        → Compare with other curation strategies
```

### DCLM-Baseline: Model-Based Filtering
Key finding: Using a fastText classifier trained on high-quality reference data to score and filter web pages dramatically improves downstream model quality.

1. Train fastText classifier on OpenHermes 2.5 (positive) vs. random web (negative)
2. Score all Common Crawl pages
3. Keep top ~20% by quality score
4. Result: 3.8T high-quality tokens

## Results
| Training Data | 7B Model MMLU (5-shot) | vs. Peers |
|---|---|---|
| **DCLM-Baseline** | **63.7%** | Matches Mistral-7B |
| FineWeb-Edu | ~62% | Similar |
| RefinedWeb | ~55% | Below |
| C4 | ~50% | Well below |

DCLM-Baseline is used as a key component in [[sources/smollm2|SmolLM2]] and [[sources/olmo-2|OLMo 2]] training.

## Impact
- Used by: [[sources/smollm2|SmolLM2]] (60% FineWeb-Edu + 40% DCLM mix), [[sources/olmo-2|OLMo 2]] (filtered DCLM in Dolmino Mix)
- Established that **model-based filtering** is the most effective data curation strategy
- Dataset entity: [[entities/datasets/dclm]]
- 1.4K GitHub stars, active research community

## Connections
- Data: [[entities/datasets/dclm]]
- Used by: [[sources/smollm2]], [[sources/olmo-2]]
- Related: [[sources/fineweb]], [[sources/refinedweb]], [[entities/datasets/dolma]]
- Concepts: [[concepts/pre-training]]
- Comparisons: [[comparisons/pretraining-data]]

## Citation
> Li et al., "DataComp-LM: In search of the next generation of training sets for language models," NeurIPS 2024, arXiv:2406.11794.
