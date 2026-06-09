---
type: source
arxiv_id: "2505.00949"
title: "Llama-Nemotron: Efficient Reasoning Models"
authors: ["NVIDIA"]
date: 2025-05-01
org: "NVIDIA"
tags: [reasoning, nas, distillation, reinforcement-learning, efficiency, 2025]
upvotes: 44
---

# Llama-Nemotron

> An open family of heterogeneous reasoning models (8B, 49B, 253B) with a dynamic reasoning toggle, delivering DeepSeek-R1-competitive performance with superior inference efficiency through neural architecture search.

## Key Contributions
- First open-source models to support a **dynamic reasoning toggle** — users can switch between standard chat ("detailed thinking off") and reasoning ("detailed thinking on") modes at inference time via system prompt
- Uses **Puzzle NAS framework** to produce inference-optimized architectures from Llama 3 models, achieving **5× throughput speedup** over Llama-3.3-70B at batch size 256 on a single H100
- LN-Ultra (253B) matches or outperforms DeepSeek-R1 on most benchmarks while being **significantly more efficient** to serve
- Open-sources weights, training data, and code under a permissive license

## Method
**Architecture (Puzzle NAS)**:
- LN-Super (49B): Optimized from Llama-3.1-70B to run on a single H100 at TP1 with 5× throughput gain
- LN-Ultra (253B): Derived from Llama-3.1-405B, optimized for 4×H100 at TP4
- Puzzle performs blockwise architecture search: selects transformer blocks from the teacher model using mixed-integer programming under hardware constraints
- Post-NAS: Knowledge distillation (40B tokens for Super, 30B tokens for Ultra) + continued pretraining on curated data

**Synthetic Data for Reasoning Toggle**:
- Reasoning-on data: Math (curated pipeline from Moshkov et al.), code (OpenCodeReasoning 70K problems), science (STEM competition problems), general (Arena-Hard-style queries)
- Reasoning-off data: Paired responses generated for the same prompts with non-reasoning system prompt
- This paired data teaches the model to respect the toggle instruction

**Post-training**:
1. *SFT*: Token-level cross-entropy loss on mixed reasoning/non-reasoning data with sequence packing at 32K
2. *RL for Reasoning*: GRPO on math/science with rule-based verification. 72 rollout prompts, 16 responses each, temperature 1.0
3. *RL for Instruction Following*: Short GRPO run on synthetic constraint-following prompts
4. *RLHF*: Reward model trained on human preferences for helpfulness/safety

**Infrastructure**: NeMo-Aligner for RL, vLLM for generation, Megatron for training.

## Results
- **LN-Ultra (253B)**: 72.6% AIME 24, 67.8% AIME 25, 72.7% GPQA, 79.1% LiveCodeBench (SOTA among open models at release)
- **LN-Super (49B)**: 65.0% AIME 24, 59.3% AIME 25, 66.8% GPQA, 69.7% LiveCodeBench — competitive with models 2× its size
- **LN-Nano (8B)**: Strong for its size class — 52.0% AIME 24 in reasoning mode
- **Reasoning toggle**: Models maintain full chat quality in reasoning-off mode (on par with Llama-3.3-70B for Super)
- **Arena Hard**: 88.3% for Super, surpassing Claude 3.5 Sonnet and GPT-4o

## Models Released
- **LN-Nano** — 8B, reasoning toggle
- **LN-Super** — 49B, single-H100 optimized
- **LN-Ultra** — 253B, 4×H100 optimized

## Connections
- Builds on: [[sources/llama-3|Llama 3]], [[sources/deepseek-r1|DeepSeek-R1]] (GRPO), [[sources/open-reasoner-zero|Open-Reasoner-Zero]]
- Related to: [[sources/nemotron-3-super|Nemotron 3 Super]], [[sources/nemotron-h|Nemotron-H]]
- Related concepts: [[concepts/grpo]], [[concepts/distillation]], [[concepts/llm-serving]], [[concepts/speculative-decoding]]
- From: [[entities/orgs/nvidia|NVIDIA]]

## Citation
> NVIDIA, "Llama-Nemotron: Efficient Reasoning Models," arXiv:2505.00949, 2025.
