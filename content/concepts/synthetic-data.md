---
type: concept
tags: [synthetic-data, data-curation, pre-training, alignment]
---

# Synthetic Data for LLM Training

> Using LLMs to **generate training data for other LLMs** — from instruction datasets to pretraining textbooks. The dominant trend of 2024–2025, enabling models to surpass their teachers and making data quality accessible without expensive human annotation.

## Overview
Synthetic data has become a critical ingredient at every stage of LLM development. What started as a clever trick for generating instruction-tuning data ([[sources/self-instruct|Self-Instruct]], 2022) has evolved into a comprehensive methodology spanning pretraining, alignment, and evaluation — fundamentally changing the relationship between data quantity and data quality.

## How It Works

### Synthetic Data for Pretraining
- **Phi series** approach ([[sources/phi-4|Phi-4]]): Generate 50+ types of synthetic datasets (Q&A pairs, textbooks, reasoning chains, code exercises) using GPT-4 and other teachers
- Seed the generation with organic data (web pages, textbooks, code) to maintain diversity
- Multi-stage prompting: extract key concepts → generate exercises → verify answers
- **Result**: 14B Phi-4 surpasses GPT-4 on STEM despite being trained partly from GPT-4 synthetic data — proving curation goes beyond imitation

### Synthetic Data for Alignment (Post-Training)
- **Magpie** ([[sources/magpie|Magpie]]): Exploit chat templates — feed only the pre-query template, model generates both instruction and response
- **Zephyr dSFT/dDPO** ([[sources/zephyr]]): Use GPT-4 to generate instruction responses, then use AI preference judgments for DPO
- **Rejection Sampling**: Generate many responses, keep only those verified correct (used in [[sources/deepseek-r1|DeepSeek-R1]], [[sources/llama-3|Llama 3]])

### Synthetic Data for Evaluation
- FineWeb-Edu ([[sources/fineweb]]): LLM-based quality classifier trained on synthetic annotations
- Process reward labels: Use LLMs to generate step-level correctness labels

## Key Methods

| Method | Stage | Approach | Paper |
|---|---|---|---|
| Self-Instruct | SFT | Bootstrap instructions from seed tasks | [[sources/self-instruct]] |
| Magpie | SFT + DPO | Auto-generate from chat templates | [[sources/magpie]] |
| dSFT/dDPO | SFT + DPO | Distill from stronger model | [[sources/zephyr]] |
| Phi-style synthesis | Pretraining | Multi-stage prompting, 50+ dataset types | [[sources/phi-4]] |
| Rejection sampling | RL | Generate many, filter by correctness | [[sources/deepseek-r1]] |
| FineWeb-Edu classifier | Data filtering | Train classifier on LLM annotations | [[sources/fineweb]] |

## The Arc of Progress
```
Self-Instruct (2022): Generate instructions from seed tasks
    → Magpie (2024): No seed tasks needed — template prompting
    → Phi-4 (2024): Systematic synthetic pretraining data
    → Result: AI-generated data at every training stage
```

## Key Insight
Synthetic data is **not just cheaper imitation** — it can be **strategically designed** to target specific capabilities (math reasoning, coding, safety), control difficulty distributions, ensure correctness via verification, and cover long-tail topics that organic data misses.

## Key Papers
- [[sources/self-instruct]] — Original synthetic instruction generation
- [[sources/magpie]] — Template-based alignment data synthesis
- [[sources/phi-4]] — Comprehensive synthetic pretraining
- [[sources/fineweb]] — LLM-based data quality classification
- [[sources/zephyr]] — Distilled alignment with AI feedback

## See Also
- [[concepts/instruction-tuning]]
- [[concepts/distillation]]
- [[concepts/pre-training]]
