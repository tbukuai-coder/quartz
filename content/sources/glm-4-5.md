---
type: source
arxiv_id: "2508.06471"
title: "GLM-4.5: Agentic, Reasoning, and Coding (ARC) Foundation Models"
authors: ["GLM-4.5 Team", "Aohan Zeng", "Xin Lv", "et al."]
date: 2025-08-06
org: "Zhipu AI"
tags: [moe, reasoning, agents, coding, reinforcement-learning, 2025]
upvotes: 211
---

# GLM-4.5

> A 355B-parameter (32B active) MoE model optimized for Agentic, Reasoning, and Coding (ARC) tasks, ranking 3rd overall and 2nd on agentic benchmarks among all evaluated models.

## Key Contributions
- Introduces a **deeper-is-better MoE architecture** — uses 89 MoE layers (vs. DeepSeek-V3's 58) with narrower width, finding that deeper models exhibit better reasoning capacity
- First major model to use the **Muon optimizer** for MoE pre-training, showing it accelerates convergence and tolerates larger batch sizes
- Proposes **Expert Model Iteration** for post-training — trains separate expert models for Reasoning, Agent, and General chat, then unifies them via self-distillation
- Achieves **70.1% on TAU-Bench** (agentic), **91.0% on AIME 24** (reasoning), and **64.2% on SWE-bench Verified** (coding) with fewer parameters than competitors
- Includes an MoE-based **Multi-Token Prediction (MTP)** layer for native speculative decoding during inference

## Method
**Architecture**: 355B total / 32B active parameters. 89 MoE layers + 3 dense layers + 1 MTP layer. Uses 160 routed experts with 8 active per token + 1 shared expert. Loss-free balance routing with sigmoid gates. GQA with 96 attention heads (2.5× more than typical), which counterintuitively doesn't improve training loss but consistently improves reasoning benchmarks. QK-Norm for attention stability.

**Pre-training**: 23T tokens in two stages. Stage 1: general webpages. Stage 2: upsampled code, math, science. Uses Muon optimizer (lr 2.5e-4 → 2.5e-5 cosine decay). Batch size warmup from 16M to 128M tokens. Cosine schedule outperformed WSD (warmup-stable-decay) on general benchmarks.

**Mid-training**: Three specialized stages after pre-training:
1. Repo-level code training (cross-file dependencies, GitHub PRs/commits) — extends to 32K
2. Synthetic reasoning data (math, science, coding competitions)
3. Long-context + agent training — extends to 128K with synthetic agent trajectories

**Post-training (Expert Model Iteration)**:
- *Stage 1*: Three expert models trained independently — Reasoning (math/code RL), Agent (real-world tool use RL), General (RLHF)
- *Stage 2*: Unified model via self-distillation from all experts, followed by final RL passes
- Uses **Slime** RL infrastructure with Megatron training + SGLang rollout engine

## Results
- **Overall rank**: 3rd among all evaluated models (open + closed), 2nd on agentic benchmarks
- **Reasoning**: 91.0% AIME 24, 85.4% MATH-500, 68.0% GPQA
- **Agents**: 70.1% TAU-Bench (complex agent interactions), 91.1% BFCL V3 (function calling)
- **Coding**: 64.2% SWE-bench Verified, 73.9% LCB (LiveCodeBench)
- **GLM-4.5-Air** (106B / 12B active): competitive compact variant

## Models Released
- **GLM-4.5** — 355B (32B active) MoE, open-source
- **GLM-4.5-Air** — 106B (12B active) MoE, compact variant

## Connections
- Builds on: [[sources/deepseek-v3|DeepSeek-V3]] (MoE design), [[sources/mixtral|Mixtral]] (MoE), [[sources/sglang|SGLang]] (inference)
- Competes with: [[sources/deepseek-v3|DeepSeek-V3]], [[sources/qwen3|Qwen3]]
- Related concepts: [[concepts/mixture-of-experts]], [[concepts/grpo]], [[concepts/multi-token-prediction]], [[concepts/llm-serving]]
- Same family: [[sources/glm-4.1v-thinking|GLM-4.1V-Thinking]]

## Citation
> GLM-4.5 Team, "GLM-4.5: Agentic, Reasoning, and Coding (ARC) Foundation Models," arXiv:2508.06471, 2025.
