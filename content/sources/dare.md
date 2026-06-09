---
type: source
arxiv_id: "2311.03099"
title: "Language Models are Super Mario: Absorbing Abilities from Homologous Models as a Free Lunch"
authors: ["Le Yu", "Bowen Yu", "Haiyang Yu", "Fei Huang", "Yongbin Li"]
date: 2023-11-06
org: "Alibaba DAMO"
tags: [model-merging, delta-parameters, efficiency, 2023]
upvotes: 32
---

# DARE — Drop And REscale

> 90–99% of fine-tuned delta parameters can be randomly dropped and rescaled without losing abilities — enabling interference-free merging of multiple specialist models into one generalist.

## Key Contributions
- **Extreme sparsity of delta parameters**: Discovered that dropping 90–99% of fine-tuning deltas randomly preserves model abilities — fine-tuning creates massively redundant parameter changes
- **DARE operation**: Drop random delta parameters + rescale survivors to maintain expected magnitude — a simple preprocessing step before merging
- **Multi-model merging**: With DARE preprocessing, multiple specialist models (code, math, instruction-following) can be merged without interference
- **Free lunch**: Merged model inherits capabilities of all constituent models at zero additional training cost

## Method
1. **Compute delta**: For each fine-tuned model, compute δ = θ_fine - θ_base
2. **Drop**: Randomly set (1-p) fraction of delta parameters to zero (p = 0.01 to 0.1 — keep only 1–10%)
3. **Rescale**: Multiply surviving parameters by 1/p to preserve expected magnitude
4. **Merge**: Average the DARE-processed deltas across models + add to base model

Why it works: Fine-tuning creates highly redundant parameter changes. The "knowledge" is concentrated in a tiny fraction of high-magnitude deltas — the rest are noise that causes interference during merging.

## Results
- **Llama 2** merges: WizardLM + WizardMath + Code Alpaca → single model with all three capabilities
- Zero-shot accuracy preserved even at 99% drop rate on BERT/RoBERTa
- GSM8K maintained after merging math-specialized and instruction-following models
- Combined with [[sources/ties-merging|TIES]] (`dare_ties` strategy) is the industry standard merge recipe
- Works for both encoder (BERT) and decoder (Llama) models

## Impact on the Ecosystem
DARE + TIES is the **standard merging pipeline** on HF Hub:
- `mergekit` implements `dare_ties` and `dare_linear` strategies
- Thousands of merged models on HF Hub use DARE preprocessing
- Democratizes multi-capability models without training

## Connections
- Paired with: [[sources/ties-merging|TIES-Merging]] (DARE preprocesses, TIES resolves conflicts)
- Related: [[sources/lora|LoRA]] (both exploit low-rank/sparse structure of fine-tuning)
- Concepts: [[concepts/model-merging|Model Merging]]
- Org: [[entities/orgs/alibaba|Alibaba / Qwen]]

## Citation
> Yu et al., "Language Models are Super Mario: Absorbing Abilities from Homologous Models as a Free Lunch," arXiv:2311.03099, 2023.
