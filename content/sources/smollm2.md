---
type: source
arxiv_id: "2502.02737"
title: "SmolLM2: When Smol Goes Big — Data-Centric Training of a Small Language Model"
authors: ["Loubna Ben Allal", "Anton Lozhkov", "Elie Bakouch", "et al."]
date: 2025-02-04
org: "Hugging Face"
tags: [open-models, small-model, data-centric, 2025]
upvotes: 258
---

# SmolLM2: When Smol Goes Big — Data-Centric Training of a Small Language Model

> A **1.7B parameter** model trained on ~11T tokens through multi-stage data-centric training, outperforming other small models and demonstrating that **data quality and mixing matter more than scale**.

## Key Contributions
- Demonstrated that **overtraining** small models on high-quality data (11T tokens for 1.7B params) produces excellent results
- Introduced a **multi-stage training process** with careful dataset mixing
- Created specialized datasets: **FineMath** (math), **Stack-Edu** (code), **SmolTalk** (conversation)
- Extensive **ablation studies** on dataset composition — one of the most transparent training descriptions
- State-of-the-art among small models (≤2B) at release

## Method
### Multi-Stage Pre-training
1. **Stage 1**: Train on web text (FineWeb-Edu) — general knowledge
2. **Stage 2**: Mix in **FineMath** (curated math data) and **Stack-Edu** (educational code) — domain skills
3. **Stage 3**: Increase proportion of high-quality specialized data — skill refinement

### Key Datasets Created
- **FineMath**: High-quality mathematical content filtered from web data
- **Stack-Edu**: Educational programming content from Stack Overflow + GitHub
- **SmolTalk**: Curated conversational data for instruction tuning

### Key Finding
Data mixing ratios are critical. The paper provides detailed ablations showing how different proportions of web/math/code data affect downstream performance. Small models benefit more from data quality than large models do.

## Models Released
| Model | Params | Training Tokens |
|---|---|---|
| SmolLM2-135M | 135M | ~11T |
| SmolLM2-360M | 360M | ~11T |
| SmolLM2-1.7B | 1.7B | ~11T |

## Connections
- **Key concepts**: [[concepts/pre-training]], [[concepts/scaling-laws]], [[concepts/instruction-tuning]]
- **Related**: [[sources/scaling-data-constrained]] (data repetition insights)
- **Models**: [[entities/models/smollm]]
- **Organizations**: [[entities/orgs/huggingface]]
- **GitHub**: [huggingface/smollm](https://github.com/huggingface/smollm)

## Citation
> Ben Allal et al., "SmolLM2: When Smol Goes Big — Data-Centric Training of a Small Language Model," arXiv:2502.02737, 2025.
> https://huggingface.co/papers/2502.02737
