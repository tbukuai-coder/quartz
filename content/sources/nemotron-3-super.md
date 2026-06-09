---
type: source
arxiv_id: "2604.12374"
title: "Nemotron 3 Super: Open, Efficient Mixture-of-Experts Hybrid Mamba-Transformer Model for Agentic Reasoning"
authors: ["NVIDIA"]
date: 2025-04-12
org: "NVIDIA"
tags: [moe, mamba, hybrid, fp4, agents, reasoning, 2025]
upvotes: 36
---

# Nemotron 3 Super

> A 120B (12B active) hybrid Mamba-Attention MoE model — the first to combine NVFP4 pre-training, LatentMoE architecture, and MTP layers for native speculative decoding, achieving 2.2× higher throughput than GPT-OSS-120B.

## Key Contributions
- First model to be **pre-trained natively in NVFP4** (4-bit floating point), demonstrating that FP4 pre-training at 25T tokens is stable and competitive
- Introduces **LatentMoE** — a new MoE variant that projects expert inputs to a latent space before routing, optimizing both accuracy per FLOP and accuracy per parameter
- Includes **MTP (Multi-Token Prediction) layers** for native speculative decoding, enabling inference acceleration without separate draft models
- Hybrid **Mamba-Attention** architecture — alternates between Mamba-2 SSM layers and attention layers for efficiency with long contexts up to 1M tokens
- Achieves **2.2× throughput over GPT-OSS-120B** and **7.5× over Qwen3.5-122B** at comparable accuracy
- All datasets, base model, post-trained, and quantized checkpoints are open-sourced

## Method
**Architecture**: 120B total / 12B active. Hybrid layer pattern alternating Mamba-2 (state space model) layers and attention layers. Uses LatentMoE instead of standard MoE — expert inputs are projected to a lower-dimensional latent space before the router, reducing routing overhead. 1 MTP layer appended for speculative decoding.

**NVFP4 Pre-training**:
- All linear layers in NVFP4 except: final 15% of network in BF16 (stability), latent projections in BF16, MTP layers in BF16
- Uses Warmup-Stable-Decay (WSD) learning rate schedule over 25T tokens
- **Tracking Merge Evaluation**: During the stable phase, averages checkpoints in weight space (model soups) to smooth noisy benchmark performance

**Pre-training data**: 25T tokens including web, code, math, science, multilingual. Releases new specialized datasets: synthetic code concepts, synthetic code competitions, and math competition CoT.

**Post-training**:
1. **SFT**: Scaled up agentic datasets; added "low effort reasoning mode" for latency-sensitive scenarios
2. **RLVR**: Multi-environment RL across 5 simultaneous gym environments (math, code, science, instruction following, agentic tasks)
3. **SWE-RL**: Specialized RL for software engineering using GitHub issue/PR data
4. **RLHF**: Final stage for helpfulness, chat quality, and safety
5. **MTP healing**: Brief training phase to recover MTP layer quality after RL

**Long-context**: Extended to 1M context via continual pretraining phase with progressive sequence length increase.

## Results
- **AIME 25**: 90.2% (no tools), competitive with Qwen3.5-122B (90.4%)
- **HMMT Feb25**: 93.7% (no tools), 94.7% (with tools) — outperforms Qwen3.5-122B
- **SWE-bench Verified**: 63.8% — competitive with frontier models
- **TAU-Bench**: 78.3% (agentic) — strong real-world agent performance
- **Inference**: 2.2× throughput vs. GPT-OSS-120B, 7.5× vs. Qwen3.5-122B
- **FP8/FP4 quantized checkpoints** provided for deployment on Hopper/Blackwell GPUs

## Models Released
- **Nemotron 3 Super 120B-A12B Base** — open-source base model
- **Nemotron 3 Super 120B-A12B Instruct** — post-trained
- **FP8 and NVFP4 quantized checkpoints** — for efficient deployment

## Connections
- Builds on: [[sources/nemotron-h|Nemotron-H]] (hybrid Mamba-Transformer), [[sources/mamba|Mamba]], [[sources/mamba-2|Mamba 2]]
- Uses: [[sources/quartet|Quartet]]-related NVFP4 training, [[sources/deepseek-r1|DeepSeek-R1]] (GRPO for RL)
- Competes with: [[sources/glm-4-5|GLM-4.5]], [[sources/qwen3|Qwen3]], [[sources/gpt-oss|GPT-OSS]]
- Related concepts: [[concepts/mixture-of-experts]], [[concepts/state-space-models]], [[concepts/multi-token-prediction]], [[concepts/quantization]]
- From: [[entities/orgs/nvidia|NVIDIA]]

## Citation
> NVIDIA, "Nemotron 3 Super: Open, Efficient Mixture-of-Experts Hybrid Mamba-Transformer Model for Agentic Reasoning," arXiv:2604.12374, 2025.
