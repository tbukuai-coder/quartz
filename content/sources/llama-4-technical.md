---
type: source
arxiv_id: "2601.11659"
title: "The Llama 4 Herd: Architecture, Training, Evaluation, and Deployment Notes"
authors: ["Meta AI"]
date: 2026-01-20
org: "Meta"
tags: [open-model, moe, multimodal, architecture, 2026]
upvotes: 0
---

# Llama 4 Technical Details

> Comprehensive technical report on Meta's Llama 4 model family — Scout (17B active/109B total) and Maverick (17B active/400B total) with early-fusion multimodality, iRoPE, and Behemoth teacher model.

## Key Contributions
- Detailed technical architecture for **Llama 4 Scout** (109B total, 17B active, 10M context) and **Maverick** (400B total, 17B active)
- **Early-fusion multimodal**: Vision/text integrated from the start of pre-training (not bolted on after)
- **iRoPE**: Interleaved RoPE — novel positional encoding enabling 10M+ token context in Scout
- **Routed/shared expert MoE**: Hybrid expert structure with both routed and always-active shared experts
- **Behemoth teacher** (2T+ params): Previewed as the largest model used for distillation
- **Multi-stage training**: Pre-training → mid-training → lightweight SFT → online RL → lightweight DPO

## Method
Architecture innovations:
1. **Early-fusion multimodality**: Text and image tokens processed together from layer 1 — deeper cross-modal understanding than late-fusion
2. **iRoPE (Interleaved RoPE)**: Alternates between RoPE and NoPE (no positional encoding) layers — enables extreme context extension to 10M tokens
3. **MoE structure**: Combines routed experts (top-k per token) with shared experts (always active) — ensures consistent base capability
4. **Length generalization**: Training on 10M tokens without proportional memory increase

Training pipeline:
- Pre-training on massive multilingual + multimodal corpus
- Mid-training with domain-specific data upsampling
- Lightweight SFT + online RL + lightweight DPO for alignment

## Results
- **Scout**: 10M token context — longest among open models
- **Maverick**: Strong general reasoning, competitive with Qwen3-235B
- **Multimodal**: Native image understanding without separate vision encoder fine-tuning
- **Behemoth**: Previewed as teacher model for distillation into smaller variants

## Models Released
- Llama 4 Scout (109B, 17B active) — open weights
- Llama 4 Maverick (400B, 17B active) — open weights

## Connections
- **Builds on**: [[sources/llama-3|Llama 3]], [[sources/llama-4|Llama 4 announcement]]
- **Part of**: [[entities/models/llama|Llama]] family, [[entities/orgs/meta|Meta]]
- **Related concepts**: [[concepts/mixture-of-experts|MoE]], [[concepts/positional-encodings|Positional Encodings]] (iRoPE), [[concepts/long-context|Long Context]], [[concepts/multimodal-models|Multimodal Models]]
- **Comparison**: [[comparisons/open-model-families|Open Model Families]]
- **Historic**: First open model with 10M token context

## Citation
> Meta AI, "The Llama 4 Herd: Architecture, Training, Evaluation, and Deployment Notes," arXiv:2601.11659, 2026.
