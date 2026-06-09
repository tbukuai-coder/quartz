---
type: concept
tags: [pre-training, data-curation, scaling-laws, 2024]
---

# Data Mixing & Curation

> The science of selecting and combining training data from different domains (web, code, academic, books) to optimize LLM performance — increasingly recognized as more important than model scale.

## Overview
Pre-training data for LLMs is a mixture of domains: web text, code, academic papers, books, conversation data, math, etc. The **proportions** of these domains dramatically affect model capabilities. Data mixing research aims to make this optimization scientific rather than heuristic.

## Why It Matters
- [[sources/fineweb|FineWeb-Edu]] showed 1.3T curated tokens beats 15T unfiltered tokens
- [[sources/phi-4|Phi-4]] (14B) beats Llama-3.1-70B on reasoning with synthetic data
- [[sources/smollm2|SmolLM2]] showed small models thrive on curated data
- The field has shifted from "bigger models" to "better data"

## Key Approaches

### Data Mixing Laws
[[sources/data-mixing-laws|Data Mixing Laws]] (2024) discovered quantitative relationships between domain proportions and model loss. Key formula: L_i(r) = c_i + k_i · exp(Σⱼ t_ij · rⱼ). Enables predicting 1B+ model performance from 70M experiments.

### Quality Filtering
- [[sources/fineweb|FineWeb]]: Used classifier-based quality scoring (trained on educational text) to filter 15T tokens → 1.3T high-quality tokens
- [[sources/refinedweb|RefinedWeb]]: Proved web-only data can match curated mixtures with proper deduplication
- [[sources/dclm|DCLM]]: Created a benchmark for comparing data curation strategies

### Synthetic Data Generation
- [[sources/phi-4|Phi-4]]: Synthetic textbook-style data surpasses teacher model
- [[entities/datasets/cosmopedia|Cosmopedia]]: Synthetic textbooks from Mixtral for SmolLM
- [[sources/magpie|Magpie]]: Generates instruction data from chat templates

### Multi-stage Mixing
Modern recipes use different data mixes at different training stages:
- **Phase 1**: Broad web data for general knowledge
- **Phase 2**: Higher-quality, domain-focused data for specialization (Dolmino Mix for OLMo 2)
- **Annealing**: Final phase with highest-quality data

## Key Papers
- [[sources/data-mixing-laws|Data Mixing Laws]] (2024) — Quantitative prediction of performance from mix proportions
- [[sources/fineweb|FineWeb]] (2024) — 15T→1.3T quality filtering pipeline
- [[sources/chinchilla|Chinchilla]] (2022) — Compute-optimal data:params ratio
- [[sources/scaling-data-constrained|Scaling Data-Constrained LMs]] (2023) — Data repetition scaling
- [[sources/dclm|DCLM]] (2024) — Data curation benchmark
- [[sources/dolma|Dolma]] (2024) — Fully open data composition

## See Also
- [[concepts/pre-training|Pre-training]]
- [[concepts/scaling-laws|Scaling Laws]]
- [[concepts/synthetic-data|Synthetic Data]]
- [[comparisons/pretraining-data|Pretraining Data Comparison]]
