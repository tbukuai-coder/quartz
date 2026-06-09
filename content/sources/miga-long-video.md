---
type: source
arxiv_id: "2605.18233"
title: "Enhancing Train-Free Infinite-Frame Generation for Consistent Long Videos (MIGA)"
authors: ["X. Feng", "J. Zhu", "M. Wu", "C. Chen", "F. Mao", "H. Guo", "J. Wu", "X. Chu", "K. Huang"]
date: 2026-05-21
org: "Multi-institution"
tags: [video-generation, long-video, train-free, temporal-consistency, 2026]
upvotes: 91
---

# MIGA: Enhancing Train-Free Infinite-Frame Generation for Consistent Long Videos

> Train-free long video generation framework addressing FIFO-diffusion's training-inference gap and temporal inconsistency via dual consistency mechanisms (self-reflection + long-range frame guidance), enabling infinite-length generation with constant memory.

## Key Contributions
- **Dual consistency mechanisms**: combines self-reflection approach with long-range frame guidance for temporal coherence
- **Noise span optimization**: reduces the training-inference gap in frame-level autoregressive (FIFO) diffusion
- **Train-free**: works with existing foundation video models without retraining or fine-tuning
- **Infinite-frame generation**: produces arbitrarily long videos with constant memory consumption
- **Self-reflection approach**: enables the model to correct drift by referring back to its own earlier outputs

## Method
Frame-level autoregressive frameworks like FIFO-diffusion generate infinitely long videos with constant memory, but suffer from (1) training-inference mismatch (noise span differs from what the model saw during training) and (2) temporal drift (no mechanism to maintain long-range consistency). MIGA addresses both: noise span optimization reduces the distributional gap, while dual consistency — self-reflection (looking back at own outputs) and long-range frame guidance (conditioning on temporally distant keyframes) — prevents drift.

## Results
- Significantly improved temporal consistency over FIFO-diffusion
- Enables effective infinite-length video generation with foundation models
- No retraining required — plug-and-play with existing video diffusion models
- Constant memory footprint regardless of output length

## Connections
- Builds on: [[sources/self-forcing-pp]], [[sources/stream-t1]], [[concepts/video-generation]]
- Related: [[sources/longlive-2]], [[sources/causal-forcing-pp]], [[sources/anyflow]]
- Complements: training-based approaches (LongLive-2.0) with training-free alternative

## Citation
> Feng et al., "Enhancing Train-Free Infinite-Frame Generation for Consistent Long Videos," arXiv:2605.18233, 2026.
