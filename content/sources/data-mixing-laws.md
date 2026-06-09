---
type: source
arxiv_id: "2403.16952"
title: "Data Mixing Laws: Optimizing Data Mixtures by Predicting Language Modeling Performance"
authors: ["Jiasheng Ye", "Peiju Liu", "Tianxiang Sun", "Yunhua Zhou", "Jun Zhan", "Xipeng Qiu"]
date: 2024-03-25
org: "Fudan University"
tags: [pre-training, data-curation, scaling-laws, 2024]
upvotes: 1
---

# Data Mixing Laws

> Discovers quantitative laws that predict LLM performance from training data mixture proportions, enabling optimized data recipes without expensive full-scale runs.

## Key Contributions
- Discovered **data mixing laws**: functional relationships that quantitatively predict model loss from training data mixture proportions
- Proposed **nested scaling laws** combining data mixing laws with model-size and training-step scaling laws — predict large model performance using only small-scale experiments
- Demonstrated a **1B model trained on optimized mixture matches one trained 48% longer** on the default RedPajama mixture
- Extended to **continual pretraining**, accurately predicting the critical mixture proportion to avoid catastrophic forgetting
- Outlooks **dynamic data schedules** — changing mixture proportions during training based on mixing law predictions

## Method
The key insight is that domain losses follow predictable functional forms with respect to mixture proportions. For K training domains with proportions r₁...r_M, the loss on domain i follows:

L_i(r₁...r_M) = c_i + k_i · exp(Σⱼ t_ij · rⱼ)

This exponential form captures both within-domain and cross-domain effects. Parameters are fit on a small number of sample mixtures, then the fitted law predicts performance on any unseen mixture. Combined with standard scaling laws for model size and training steps, this enables a **nested prediction pipeline**:
1. Train tiny models (70M, 160M) on a few mixtures
2. Fit data mixing laws + scaling laws
3. Predict 1B+ model performance on any mixture
4. Select optimal mixture proportions

## Results
- **Prediction accuracy**: Mean absolute error < 0.01 on domain losses for 3-domain and 7-domain mixtures
- **Optimization**: 1B model on optimized RedPajama mixture ≈ performance of 1B model trained 48% longer on default mixture
- **Nested prediction**: Small-scale experiments (70M, 160M) accurately predict 1B model loss rankings
- **Continual pretraining**: Accurately predicts forgetting thresholds when adding new domain data

## Datasets Used
- [[entities/datasets/redpajama|RedPajama]] (7 domains: Common Crawl, C4, GitHub, Wikipedia, Books, ArXiv, StackExchange)
- The Pile (validation)

## Connections
- **Builds on**: [[sources/chinchilla|Chinchilla]] (scaling laws), [[sources/scaling-data-constrained|Scaling Data-Constrained LMs]]
- **Related concepts**: [[concepts/pre-training|Pre-training]], [[concepts/scaling-laws|Scaling Laws]]
- **Related work**: DoReMi, RegMix (alternative data mixing optimization)
- **Influenced**: CLIMB (clustering-based data mixture bootstrapping), DataChef
- **Complements**: [[sources/fineweb|FineWeb]] (data quality), [[sources/dolma|Dolma]] (data composition)

## Citation
> Ye et al., "Data Mixing Laws: Optimizing Data Mixtures by Predicting Language Modeling Performance," arXiv:2403.16952, 2024.
