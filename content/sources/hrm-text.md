---
type: source
arxiv_id: "2605.20613"
title: "HRM-Text: Efficient Pretraining Beyond Scaling"
authors: ["Guan Wang", "Changling Liu", "Chenyu Wang", "Cai Zhou", "Yuhao Sun", "Yifei Wu", "Shuai Zhen", "Luca Scimeca", "Yasin Abbasi Yadkori"]
date: 2026-05-21
org: "Sapient Inc"
tags: [architecture, recurrent, pretraining, efficiency, non-transformer, 2026]
upvotes: 90
---

# HRM-Text: Efficient Pretraining Beyond Scaling

> Hierarchical Recurrent Model replacing standard Transformers with deep multi-timescale recurrence inspired by the frontoparietal loop, achieving competitive language modeling with significantly reduced compute via MagicNorm and warmup deep credit assignment.

## Key Contributions
- **Hierarchical Recurrent Model (HRM)**: decouples computation into multi-timescale processing levels inspired by biological frontoparietal loop organization
- **MagicNorm**: novel normalization technique enabling stable deep recurrence training
- **Warmup deep credit assignment**: solves vanishing gradient problem in deep recurrent architectures
- **Task-completion objective**: specialized training on instruction-response pairs with PrefixLM masking
- **987 GitHub stars** indicating strong community interest in non-Transformer alternatives
- Achieves competitive performance with significantly reduced computational requirements

## Method
HRM-Text replaces standard Transformer self-attention with a Hierarchical Recurrent Model that processes information at multiple timescales — fast local processing at lower levels and slower global integration at higher levels, inspired by the functional organization of biological neural circuits. MagicNorm stabilizes training of deep recurrent layers. Warmup deep credit assignment gradually increases the effective depth during training to solve vanishing gradients. The model is trained with a task-completion objective on instruction-response pairs using PrefixLM masking.

## Results
- Competitive language modeling performance with significantly reduced compute-to-performance ratio
- Demonstrates that non-Transformer architectures remain viable for language modeling
- Sample-efficient learning through multi-timescale processing

## Connections
- Builds on: [[sources/mamba]], [[sources/mamba-2]], [[concepts/state-space-models]]
- Related: [[sources/nemotron-3-super]], [[sources/darwin-family]], [[concepts/transformer-architecture]]
- Challenges: Transformer dominance assumption in LLM pretraining

## Citation
> Wang et al., "HRM-Text: Efficient Pretraining Beyond Scaling," arXiv:2605.20613, 2026.
