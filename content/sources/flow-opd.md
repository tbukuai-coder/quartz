---
type: source
arxiv_id: "2605.08063"
title: "Flow-OPD: On-Policy Distillation for Flow Matching Models"
authors: ["Zhen Fang", "Wenxuan Huang", "Yu Zeng", "Yiming Zhao", "Shuang Chen", "Kaituo Feng", "Yunlong Lin", "Lin Chen", "Zehui Chen", "Shaosheng Cao"]
date: 2026-05-11
org: "Multi-institution"
tags: [diffusion, flow-matching, rl, distillation, image-generation, 2026]
upvotes: 98
---

# Flow-OPD: On-Policy Distillation for Flow Matching Models

> First unified post-training framework for Flow Matching T2I models combining GRPO-style on-policy distillation with Manifold Anchor Regularization to overcome reward sparsity and gradient interference in multi-task alignment, achieving teacher-surpassing generation quality.

## Key Contributions
- **On-policy distillation for Flow Matching**: adapts the RL community's OPD paradigm to continuous-flow generative models
- **GRPO + task-routing labeling**: applies group-relative policy optimization with task-specific reward routing
- **Dense trajectory-level supervision**: provides richer signal than scalar rewards via full trajectory scoring
- **Manifold Anchor Regularization (MAR)**: prevents reward hacking and mode collapse during RL alignment
- **Teacher-surpassing effect**: aligned student exceeds teacher quality on GenEval and OCR accuracy
- **213 GitHub stars**

## Method
Flow-OPD addresses two bottlenecks in aligning Flow Matching (FM) T2I models: (1) reward sparsity from scalar-valued rewards; (2) gradient interference from jointly optimizing heterogeneous objectives (the "seesaw effect"). Stage 1: On-policy distillation with GRPO and task-routing labeling provides dense trajectory-level supervision. Stage 2: Manifold Anchor Regularization constrains updates to stay near the data manifold, preventing reward hacking. Applied to Stable Diffusion 3.5 Medium.

## Results
- Surpasses teacher model on GenEval (compositional generation) and OCR accuracy
- Eliminates seesaw effect between competing quality metrics
- Significant improvement over baseline SD3.5 Medium on multiple benchmarks

## Connections
- Builds on: [[sources/sd3]], [[concepts/grpo]], [[concepts/rectified-flow]], [[concepts/diffusion-models]]
- Related: [[sources/marble]], [[sources/edit-r1]], [[sources/anyflow]]
- Bridges: RL reasoning methods (GRPO) applied to image generation alignment

## Citation
> Fang et al., "Flow-OPD: On-Policy Distillation for Flow Matching Models," arXiv:2605.08063, 2026.
