---
type: source
arxiv_id: "2605.18678"
title: "Lance: Unified Multimodal Modeling by Multi-Task Synergy"
authors: ["Fengyi Fu", "Mengqi Huang", "Shaojin Wu", "Yunsheng Jiang", "Yufei Huo", "Hao Li", "Yinghang Song", "Fei Ding", "Jianzhu Guo", "Qian He"]
date: 2026-05-19
org: "ByteDance"
tags: [multimodal, unified-model, moe, generation, editing, video, 2026]
upvotes: 78
---

# Lance: Unified Multimodal Modeling by Multi-Task Synergy

> Lightweight native unified model supporting multimodal understanding, generation, and editing for images and videos via collaborative multi-task training with dual-stream MoE architecture, modality-aware RoPE, and staged adaptive data scheduling.

## Key Contributions
- **Unified understanding + generation + editing**: single model handles image/video comprehension, generation, and editing without separate specialized models
- **Dual-stream MoE architecture**: decoupled capability pathways via mixture-of-experts with unified context modeling
- **Modality-aware rotary positional encoding**: adapts position encoding per modality for better cross-modal alignment
- **Staged multi-task training with adaptive data scheduling**: progressive training that balances competing task objectives
- **1,082 GitHub stars** — trained from scratch, lightweight, practical
- Explores collaborative multi-task training rather than model capacity scaling

## Method
Lance is trained from scratch with two core principles: (1) unified context modeling — all modalities share a common representation space; (2) decoupled capability pathways — dual-stream MoE routes different capabilities (understanding vs generation) through specialized expert paths while sharing the backbone. Modality-aware rotary positional encoding adapts position information per modality. Staged training with adaptive data scheduling progressively introduces tasks and adjusts data ratios.

## Results
- Competitive with specialized models on understanding, generation, and editing benchmarks
- Lightweight architecture — demonstrates that multi-task synergy can replace model scaling
- Handles both images and videos in a unified framework

## Connections
- Builds on: [[sources/minicpm-o-4-5]], [[sources/qwen-image-2]], [[concepts/mixture-of-experts]]
- Related: [[sources/joyai-image]], [[sources/edit-r1]], [[concepts/multimodal-models]]
- Organization: ByteDance

## Citation
> Fu et al., "Lance: Unified Multimodal Modeling by Multi-Task Synergy," arXiv:2605.18678, 2026.
