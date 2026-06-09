---
type: source
arxiv_id: "2604.27085"
title: "RoundPipe: Efficient Training on Multiple Consumer GPUs with Pipeline Parallelism"
authors: ["Yibin Luo", "Shiwei Gao", "Huichuan Zheng", "Youyou Lu", "Jiwu Shu"]
date: 2026-04-19
org: "Tsinghua University"
tags: [training-infrastructure, pipeline-parallelism, consumer-gpus, llm-training, efficiency, 2026]
upvotes: 35
---

# RoundPipe: Efficient Training on Multiple Consumer GPUs

> A novel pipeline scheduling approach that eliminates the "weight binding" constraint in LLM fine-tuning on consumer GPUs, achieving up to 2.16× higher throughput and 7.3× longer sequences on RTX 4090s.

## Key Contributions

- **Weight Binding Issue identification**: Existing pipeline schedules fix stage weights to specific GPUs, limiting throughput to the slowest stage
- **RoundPipe scheduling**: Treats GPUs as stateless execution workers with dynamic stage dispatch via round-robin assignment
- **Priority-aware transfer scheduling**: Packs parameter transfers into idle windows between critical-path activation transfers
- **Distributed event-based consistency protocol**: Fine-grained layer-level execution ordering without pipeline-stalling barriers
- **Automated stage-splitting algorithm**: O(L³) complexity for near-optimal load balancing across asymmetric stages

## Results

- On 8× RTX 4090: up to **2.16× higher throughput** and **7.3× longer sequences**
- On 8× A800: up to **1.47× speedups** and **5.6× longer sequences** for large models
- **Only system** capable of LoRA fine-tuning a **235B MoE model on 24GB GPUs**
- 4090 throughput reaches ≥76% of A800 solutions across all models

## Connections
- Builds on: [[sources/zero-deepspeed]], [[concepts/training-infrastructure]], [[sources/prima-cpp]]
- Related concepts: [[concepts/mixed-precision-training]], [[concepts/quantization]]
- Related comparisons: [[comparisons/inference-engines]]
- Cited by / Influenced: Democratizing LLM training on consumer hardware

## Citation
> Luo et al., "RoundPipe: Efficient Training on Multiple Consumer GPUs with Pipeline Parallelism," arXiv:2604.27085, 2026.
