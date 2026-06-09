---
type: entity
category: dataset
tags: [math, data-curation, huggingface, pre-training]
---

# FineMath

> A **math-focused pretraining dataset** of up to 54B tokens, created by Hugging Face for [[sources/smollm2|SmolLM2]] training. FineMath achieves **2× improvement on GSM8K** and **6× improvement on MATH** compared to prior open math datasets, by targeting step-by-step mathematical reasoning through classifier-based filtering.

## Overview
FineMath was developed to address critical gaps in existing open math pretraining datasets: insufficient size, lack of focus on step-by-step mathematical reasoning, and overrepresentation of advanced academic content. It uses the FineWeb-Edu filtering approach — training a classifier on LLM-generated quality scores — but with prompts specifically targeting mathematical deduction and reasoning at middle-school to undergraduate levels.

## Variants

| Dataset | Size | Description | HF Repo |
|---|---|---|---|
| FineMath-4+ | 10B tokens (6.7M docs) | Highest quality (scores 4–5) | `HuggingFaceTB/finemath` |
| FineMath-3+ | 34B tokens (21.4M docs) | High quality (scores 3–5) | `HuggingFaceTB/finemath` |
| InfiWebMath-4+ | 8.5B tokens (6.3M docs) | InfiMM-WebMath re-filtered at 4+ | `HuggingFaceTB/finemath` |
| InfiWebMath-3+ | 20.5B tokens (13.9M docs) | InfiMM-WebMath re-filtered at 3+ | `HuggingFaceTB/finemath` |

Combined FineMath-3+ with InfiWebMath-3+: **54B tokens** total.

## Pipeline

```
Common Crawl WARC files
  → Text extraction via Resiliparse (5.8B URLs from FineWeb)
    → Stage 1: Llama-3.1-70B-Instruct 3-point classifier
      (1 = some math, 3 = step-by-step solutions)
        → Identify high-math domains (≥10 pages scoring 2+)
          → Expand domain list with OWM & InfiMM-WebMath domains
            → Re-extract 7.7B URLs → 7.1B pages → 6.5T tokens
              → Stage 2: 5-point classifier (reasoning + school-level content)
                → MinHash deduplication + English-only filter
                  → FineMath-3+ (34B tokens) / FineMath-4+ (10B tokens)
```

## Key Design Decisions
- **Two-stage classifier**: First a coarse 3-point filter to identify math-rich domains, then a fine-grained 5-point filter for quality
- **Reasoning focus**: Prompts specifically target step-by-step mathematical deduction, not just math-adjacent content
- **Level targeting**: Middle school to early undergraduate — avoids overrepresentation of advanced research papers
- **OWM text extraction**: Uses the OpenWebMath pipeline for final extraction, preserving LaTeX formatting
- **Decontamination**: 13-gram matching against GSM8K, MATH, and MMLU with overlap ratio ≥ 0.6

## Results (Annealing Ablations)

| Dataset | GSM8K | MATH | MMLU-STEM |
|---|---|---|---|
| OpenWebMath (OWM) | ~10% | Baseline | Baseline |
| InfiMM-WebMath | ~14% | Slightly below OWM | — |
| **FineMath-4+** | **~28%** (2× InfiMM) | **6× InfiMM** | Above both |
| **FineMath-3+** | Strong | Strong | Strong |

FineMath-4+ does not plateau even after extended training, unlike InfiMM-WebMath-4+ which saturates after ~10 epochs — indicating higher effective diversity.

## Used By
- **[[sources/smollm2|SmolLM2]]**: FineMath is a key component of the multi-stage pretraining pipeline, introduced in later stages to boost mathematical reasoning
- SmolLM2's math performance directly benefited from FineMath during stable phase stages 3–4 and the decay phase

## Related Papers
- [[sources/smollm2]] — SmolLM2 (introduced FineMath)
- [[sources/fineweb]] — FineWeb (classifier-based filtering methodology)

## See Also
- [[entities/datasets/fineweb]] — FineWeb / FineWeb-Edu (same filtering philosophy)
- [[entities/datasets/cosmopedia]] — Cosmopedia (synthetic data for SmolLM2)
- [[entities/orgs/huggingface]] — Hugging Face (creator)
- [[concepts/pre-training]] — Pre-training data curation
- [[concepts/synthetic-data]] — Synthetic vs. curated data
- [[comparisons/pretraining-data]] — Data strategy comparison
