---
type: source
arxiv_id: "2605.05922"
title: "Think, then Score: Decoupled Reasoning and Scoring for Video Reward Modeling"
authors: ["Yuan Wang", "Ouxiang Li", "Yulong Xu", "Borui Liao", "Jiajun Liang", "Jinghan Li", "Meng Wang", "Xintao Wang", "Pengfei Wang", "Kuien Liu"]
venue: "arXiv preprint"
year: 2026
date: "2026-05"
org: null
upvotes: 1
tags: [video-generation, reward-modeling, chain-of-thought, evaluation, reinforcement-learning]
github: null
---

# DeScore: Think, then Score — Decoupled Reasoning and Scoring for Video Reward Modeling

> A decoupled "think-then-score" video reward model where an MLLM first generates Chain-of-Thought reasoning, then a dedicated **learnable query token + regression head** predicts the final reward — combining the generalization of CoT reasoning with the training stability of discriminative scoring.

## Key Contributions

1. **Decoupled paradigm**: Separates CoT reasoning (generative, interpretable) from final reward scoring (discriminative, stable) — avoids the optimization bottleneck of coupling both in one autoregressive chain
2. **Two-stage training**: (1) Discriminative cold start with random mask mechanism for robust scoring; (2) Dual-objective RL stage independently refining CoT quality and calibrating rewards
3. **Random mask mechanism**: Randomly masks portions of CoT during training so the scoring module learns to attend to multimodal inputs directly, not over-rely on generated reasoning
4. **SOTA on video reward benchmarks**: Superior generalization on both in-domain and OOD benchmarks, outperforming discriminative and generative baselines
5. **Effective for post-training**: Improves video generation quality when used as reward model for GRPO and Flow-DPO on Wan-2.1

## Method

### Architecture
- **Backbone**: Qwen3-VL-8B (multimodal LLM)
- **Stage 1**: Generate explicit CoT analyzing video quality
- **Stage 2**: Learnable [Reward] query token appended after CoT → regression head → scalar reward
- **Random masking**: During training, randomly mask CoT tokens with probability p — forces scoring module to also attend directly to video/text tokens

### Training Pipeline
1. **Discriminative Cold Start**: LoRA fine-tuning (rank 64) with random masking + BT loss on preference pairs
2. **Dual-Objective RL**: Independently optimize CoT quality (via outcome reward) and scoring calibration (via auxiliary BT loss) — prevents CoT degradation during reward learning

### Why Decoupling Matters
| Paradigm | Reasoning | Scoring | Problem |
|---|---|---|---|
| Discriminative RM | None | Direct regression | Shortcut learning, poor OOD |
| Generative RM | CoT → token score | Autoregressive | Coupled optimization, gradient variance ∝ T |
| **DeScore** | CoT → reasoning | Separate regression head | **Stable + generalizable** |

## Results

### Video Preference Accuracy
- SOTA on both in-domain and OOD benchmarks
- Superior generalization: maintains accuracy on unseen video generators and quality dimensions
- Outperforms VideoScore, VideoAlign, and generative RM baselines

### Post-Training Application
- Improves Wan-2.1 video generation quality under both Longcat-GRPO and Flow-DPO
- Better reward signal than VideoAlign and pure discriminative baselines

## Connections

- [[sources/stream-t1|Stream-T1]] — Video generation with test-time scaling; DeScore provides the reward model for such systems
- [[sources/marble|MARBLE]] — Multi-reward for diffusion; DeScore provides per-video quality assessment
- [[concepts/reward-modeling|Reward Modeling]] — Extends reward modeling to video domain with decoupled CoT
- [[concepts/video-generation|Video Generation]] — Critical evaluation infrastructure for video gen post-training
- [[sources/repro|RePro]] — Both address reward model design; RePro for process rewards in reasoning, DeScore for video quality
