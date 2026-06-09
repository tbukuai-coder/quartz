---
type: source
arxiv_id: "2605.12500"
title: "SenseNova-U1: Unifying Multimodal Understanding and Generation with NEO-unify Architecture"
authors: ["Haiwen Diao", "Penghao Wu", "Hanming Deng", "Jiahao Wang", "Shihao Bai", "Silei Wu", "Weichen Fan", "Wenjie Ye", "Wenwen Tong", "Xiangyu Fan"]
date: 2026-05-13
org: "SenseTime"
tags: [multimodal, unified-model, vision-language, generation, understanding, 2026]
upvotes: 191
---

# SenseNova-U1: Unifying Multimodal Understanding and Generation with NEO-unify Architecture

> Native unified multimodal model bridging understanding and generation via NEO-unify architecture — covers vision-language perception, knowledge reasoning, agentic decision-making, spatial intelligence, any-to-image synthesis, text-rich infographics, VLA, and world modeling. 2,642 GitHub stars.

## Key Contributions
- **NEO-unify architecture**: native unified paradigm treating understanding and generation as integrated processes (not cascaded pipelines)
- **Dense + MoE variants**: both dense and mixture-of-experts configurations
- **Comprehensive capabilities**: VL perception, knowledge reasoning, agentic decision, spatial intelligence, any-to-image, text-rich generation, VLA, world modeling
- **2,642 GitHub stars** — massive community adoption
- Argues the understanding/generation divide is a structural limitation, not just engineering artifact

## Method
SenseNova-U1 builds on NEO-unify, a native unified paradigm that eliminates the traditional dichotomy between understanding (encoding) and generation (decoding). Rather than cascading separate encoders and generators, it shares representation spaces bidirectionally — the same representations that enable understanding also drive generation. Available in both dense and MoE variants for different compute budgets.

## Results
- Strong performance across multimodal understanding benchmarks
- High-quality image synthesis and text-rich infographic generation
- Demonstrates agentic decision-making and spatial intelligence
- Vision-language-action capabilities for embodied tasks

## Connections
- Builds on: [[sources/lance]], [[sources/qwen-image-2]], [[sources/minicpm-o-4-5]]
- Related: [[concepts/multimodal-models]], [[concepts/mixture-of-experts]], [[concepts/vision-language-models]]
- Organization: SenseTime

## Citation
> Diao et al., "SenseNova-U1: Unifying Multimodal Understanding and Generation with NEO-unify Architecture," arXiv:2605.12500, 2026.
