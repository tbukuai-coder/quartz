---
type: source
arxiv_id: "2407.10671"
title: "Qwen2 Technical Report"
authors: ["Qwen Team", "An Yang", "Baosong Yang"]
date: 2024-07-16
org: "Alibaba / Qwen"
tags: [pre-training, open-model, multilingual, moe, 2024]
upvotes: 171
---

# Qwen2

> The Qwen2 series (0.5B–72B, plus MoE variant 57B-A14B) trained on 7T tokens, surpassing prior open models on MMLU, GPQA, HumanEval, GSM8K, and multilingual benchmarks.

## Key Contributions
- Released **Qwen2 dense models** (0.5B, 1.5B, 7B, 57B-A14B MoE, 72B) covering the full scale range
- Trained on **7T tokens** (up from 3T in Qwen1.5), with improved quality filtering and diverse data mix
- Qwen2-72B surpasses **LLaMA-3-70B** on most benchmarks (MMLU 84.2 vs 79.5)
- Extended multilingual coverage to **27 languages** with dedicated evaluation
- Introduced **GQA** across all model sizes for efficient inference
- First Qwen generation with **MoE variant** (57B total, 14B active)

## Method
Standard decoder-only Transformer with GQA, SwiGLU, RMSNorm, and RoPE. Training uses multi-stage pretraining with careful domain balancing across web, code, math, academic, and multilingual data. Post-training includes SFT on high-quality instruction data followed by DPO for alignment.

The MoE variant (Qwen2-57B-A14B) uses 8 experts per layer with top-2 routing, giving it the quality of a ~70B model at the inference cost of ~14B.

## Results
- **MMLU**: 84.2 (72B) — surpasses Llama-3-70B (79.5) and Mixtral-8x22B (77.8)
- **GPQA**: 37.9 (72B) — competitive with frontier models
- **HumanEval**: 86.0 (72B) — strong code generation
- **GSM8K**: 89.5 (72B) — strong math reasoning
- **Multilingual**: SOTA on M3Exam across 27 languages
- **MoE variant**: Matches Qwen2-72B on many tasks at ~40% inference cost

## Models Released
- Qwen2-0.5B, 1.5B, 7B, 57B-A14B, 72B (Base + Instruct variants)

## Connections
- **Builds on**: Qwen1.5 series
- **Foundation for**: [[sources/qwen25|Qwen2.5]], [[sources/qwen3|Qwen3]], [[sources/qwen2-vl|Qwen2-VL]], [[sources/qwen2-audio|Qwen2-Audio]]
- **Part of**: [[entities/models/qwen|Qwen]] family, [[entities/orgs/alibaba|Alibaba/Qwen]]
- **Related concepts**: [[concepts/mixture-of-experts|MoE]], [[concepts/pre-training|Pre-training]], [[concepts/dpo|DPO]]

## Citation
> Qwen Team, "Qwen2 Technical Report," arXiv:2407.10671, 2024.
