---
type: comparison
tags: [pre-training, data-curation, synthetic-data, synthesis]
---

# Comparison: Pretraining Data Strategies — Web Curation vs Synthetic Data

> Two competing approaches to building high-quality pretraining datasets: **curating web data** (FineWeb, RefinedWeb) vs **generating synthetic data** (Phi series). The frontier increasingly combines both, and [[sources/davinci-llm|daVinci-LLM]] provides the first systematic scientific framework for understanding the full spectrum.

## Overview

The question "where does pretraining data come from?" has diverged into two distinct philosophies:
1. **Web curation**: Start with massive web crawls, apply increasingly sophisticated filtering and deduplication to extract quality
2. **Synthetic generation**: Use existing LLMs to generate training data that targets specific skills and knowledge

In practice, the best models now combine both approaches.

## Approach Comparison

| Aspect | Web Curation | Synthetic Generation | Hybrid |
|---|---|---|---|
| **Representative** | [[sources/fineweb\|FineWeb]], [[sources/refinedweb\|RefinedWeb]] | [[sources/phi-4\|Phi-4]] | [[sources/smollm2\|SmolLM2]], [[sources/llama-3\|Llama 3]] |
| **Scale** | 5–15T tokens | 0.1–0.5T tokens | 10–30T+ tokens |
| **Cost** | Low (crawling + compute) | Medium (LLM inference) | Medium-High |
| **Diversity** | Very high (billions of domains) | Moderate (controlled by prompts) | High |
| **Quality** | Variable (depends on filtering) | High (by design) | High |
| **Skill targeting** | Weak (filter for quality, not skill) | Strong (generate math, code, reasoning) | Strong |
| **Contamination risk** | High (benchmark data on web) | Low (can decontaminate) | Medium |
| **Reproducibility** | Medium (CC snapshots change) | High (fixed prompts + seeds) | Medium |

## The Methods

### Web Curation Pipeline ([[sources/fineweb|FineWeb]])
```
Common Crawl (petabytes of HTML)
  → Text extraction (trafilatura on WARC)
    → Base filtering (URL blocklist, language ID, quality heuristics)
      → Deduplication (MinHash)
        → Custom heuristic filters (50+ statistics)
          → Educational quality classifier (LLM-based)
            → FineWeb-Edu (1.3T tokens)
```
**Key innovation**: Using an LLM-trained classifier to score educational value — the single largest quality improvement in the pipeline.

### Synthetic Generation Pipeline ([[sources/phi-4|Phi-4]])
```
Organic seeds (web pages, textbooks, code)
  → Multi-stage prompting with GPT-4
    → 50+ dataset types (Q&A, exercises, textbooks, reasoning chains)
      → Quality filtering + decontamination
        → ~400B synthetic tokens
          → Combine with curated web + acquired data
```
**Key innovation**: 50+ distinct generation strategies, each targeting different skills. Not a single prompt template, but a diverse ecosystem of synthetic data.

### Data Darwinism Framework ([[sources/davinci-llm|daVinci-LLM]])
```
Raw web data (L0)
  → Basic filtering (L1–L2)
    → Quality classification (L3–L4)
      → Domain-specific processing (L5–L6)
        → Curriculum optimization (L7–L8)
          → Full synthetic generation (L9)
```
**Key innovation**: A principled **L0–L9 taxonomy** that classifies all data operations by processing depth — establishing *processing depth* as a critical scaling dimension alongside volume. Through 200+ controlled ablations, reveals that different domains saturate at different rates and require adaptive strategies.

## Results Comparison

### FineWeb-Edu (Pure Web Curation)
- 1.71B model trained on 350B tokens from FineWeb-Edu outperforms models trained on:
  - C4, Dolma, RedPajama, RefinedWeb
  - Any other open web dataset on knowledge benchmarks

### Phi-4 (Synthetic-Heavy)
- 14B model with ~40% synthetic pretraining data achieves:
  - 80.4% MATH (vs 64.2% for Llama-3.1-70B)
  - 56.1% GPQA (vs 53.6% for GPT-4o)
  - Surpasses its GPT-4 teacher on STEM

### SmolLM2 (Hybrid)
- 1.7B model using FineWeb-Edu + Cosmopedia (synthetic textbooks) + curated code:
  - Outperforms all sub-2B models
  - Competitive with 7B models on many tasks

### daVinci-LLM (Systematic Science)
- 3B model trained on 8T tokens with adaptive curriculum:
  - Processing depth (L0→L9) systematically enhances all capabilities
  - Code/math domains saturate faster than general language
  - Compositional balance prevents "performance collapse"
  - 200+ ablations documenting domain-specific dynamics

## Key Insights

### 1. They're Complementary, Not Competing
- Web data provides **breadth and diversity** — billions of topics, styles, and perspectives
- Synthetic data provides **depth and targeting** — focused practice on specific skills
- Best results come from combining both

### 2. Quality Filtering Is the Key Lever
- **FineWeb**: Educational quality classifier is the single largest improvement over raw web data
- **Phi-4**: Careful prompt engineering and multi-stage generation produces higher quality than single-template approaches
- In both cases, the innovation is in *selection*, not just *generation*

### 3. Data Quality > Data Quantity
Both approaches converge on the same insight: **a small amount of high-quality data beats a large amount of low-quality data**.
- FineWeb-Edu (1.3T) > FineWeb (15T) on knowledge benchmarks
- Phi-4 (14B, quality-focused) > Llama-3.1-70B (5× larger, more data)

### 4. Processing Depth Is a New Scaling Dimension
[[sources/davinci-llm|daVinci-LLM]] establishes that *how* data is processed (depth) matters as much as *how much* data is used (volume). This is a previously underappreciated dimension — the Data Darwinism framework provides a principled way to think about it.

### 5. Domain Saturation Requires Adaptive Strategies
Different data domains saturate at different rates. Code and math saturate faster than general language, requiring earlier format shifts to synthetic data. Naive scaling of any single strong domain can degrade other capabilities — compositional balance is essential.

## See Also
- [[sources/fineweb]] — FineWeb dataset and curation methodology
- [[sources/phi-4]] — Phi-4 synthetic data approach
- [[sources/refinedweb]] — RefinedWeb web curation
- [[sources/scaling-data-constrained]] — Scaling laws for data
- [[sources/davinci-llm]] — daVinci-LLM: Data Darwinism framework for pretraining science
- [[concepts/synthetic-data]]
- [[concepts/pre-training]]
- [[concepts/data-mixing]]
