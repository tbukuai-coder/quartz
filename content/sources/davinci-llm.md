---
type: source
arxiv_id: "2603.27164"
title: "daVinci-LLM: Towards the Science of Pretraining"
authors: ["Yiwei Qin", "Yixiu Liu", "Tiantian Mi", "Muhang Xie", "Various (GAIR-NLP)"]
date: 2026-03-26
org: "GAIR-NLP / SII"
tags: [pre-training, data-curation, open-science, scaling-laws, curriculum-learning, 2026]
upvotes: 32
---

# daVinci-LLM: Towards the Science of Pretraining

> A fully-open pretraining study that treats **pretraining as a scientific discipline** rather than engineering art — introducing the **Data Darwinism** framework (a principled L0–L9 taxonomy for data processing) and training a 3B model on 8T tokens with **200+ controlled ablations** documenting domain saturation dynamics, compositional balance, and evaluation protocol effects. 134 GitHub ⭐.

## Key Contributions
- **Data Darwinism framework**: A principled **L0–L9 taxonomy** classifying all data operations from raw filtering (L0) to fully synthetic generation (L9) — establishes *processing depth* as a critical scaling dimension alongside data volume
- **200+ controlled ablations**: Systematic experiments documenting how domain-specific saturation dynamics, compositional balance, and evaluation protocols shape pretraining outcomes
- **Two-stage adaptive curriculum**: Stage 1 builds foundational capabilities across diverse corpora; Stage 2 shifts to reasoning-intensive data — adapting to domain saturation signals
- **Domain saturation dynamics**: Different data domains saturate at different rates — code and math saturate faster than general language, requiring earlier format shifts to synthetic data
- **Fully open paradigm**: Complete data processing pipelines, training logs, checkpoints, and ablation results — breaking the commercial secrecy norm in pretraining research
- **Compositional balance principle**: Naive scaling of a strong domain can degrade other capabilities; targeted intensification requires maintaining compositional balance

## Method
1. **Data pipeline**: Apply Data Darwinism taxonomy to classify and process data across domains with varying pipeline depths (L0–L9)
2. **Adaptive curriculum**: Two stages — breadth-first foundational training followed by reasoning-intensive enhancement, with adaptive proportions based on domain saturation signals
3. **Systematic ablations**: Over 200 controlled experiments varying data mixing ratios, processing depth per domain, curriculum schedule, and evaluation protocol
4. **Model**: 3B parameters trained from random initialization on 8T tokens

Key insight: *How* data is processed (depth) matters as much as *how much* data is used (volume). Processing depth is a previously underappreciated scaling dimension.

## Results
- Processing depth (L0→L9) systematically enhances capabilities across benchmarks
- Code and math domains saturate faster than general language, requiring earlier shifts to synthetic formats
- Compositional balance prevents "performance collapse" — naive scaling of any single strong domain degrades others
- Evaluation protocol design materially affects interpretation of pretraining progress (benchmark contamination, evaluation window effects documented)

## Connections
- **Builds on**: [[sources/chinchilla|Chinchilla scaling laws]], [[sources/fineweb|FineWeb]], [[sources/dolma|Dolma]]
- **Related**: [[sources/data-mixing-laws|Data Mixing Laws]], [[sources/regmix|RegMix]], [[sources/scaling-data-constrained|Scaling Data-Constrained]]
- **Concepts**: [[concepts/data-mixing|Data Mixing]], [[concepts/pre-training|Pre-Training]], [[concepts/scaling-laws|Scaling Laws]]
- **Comparison**: [[comparisons/pretraining-data|Pretraining Data Comparison]]
- **GitHub**: https://github.com/GAIR-NLP/daVinci-LLM

## Citation
> Qin et al., "daVinci-LLM: Towards the Science of Pretraining," arXiv:2603.27164, 2026.
