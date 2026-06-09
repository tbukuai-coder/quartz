---
type: source
arxiv_id: "2501.12948"
title: "DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning"
authors: ["DeepSeek-AI"]
date: 2025-01-20
org: "DeepSeek"
tags: [alignment, reasoning, rlhf, 2025]
upvotes: 448
---

# DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning

> Demonstrated that **pure reinforcement learning (without SFT)** can produce emergent chain-of-thought reasoning in LLMs, with DeepSeek-R1 matching OpenAI o1 on reasoning benchmarks.

## Key Contributions
- **DeepSeek-R1-Zero**: Trained with pure RL (no SFT warmup) — reasoning behaviors **emerge naturally** from RL alone
- Showed emergence of self-verification, reflection, and long chain-of-thought during RL training
- **DeepSeek-R1**: Multi-stage pipeline (cold-start SFT → RL → rejection sampling → SFT → RL) achieves performance **comparable to OpenAI o1-1217**
- Successful **distillation** of reasoning capabilities into smaller models (1.5B–70B) using Qwen and Llama bases
- Released all model weights openly, including distilled versions
- The most upvoted paper on HF Papers (448 upvotes)

## Method
### DeepSeek-R1-Zero (Pure RL)
- Start from DeepSeek-V3 base model (no SFT)
- Apply GRPO (from [[sources/deepseekmath]]) with rule-based rewards:
  - Accuracy reward: correct final answer
  - Format reward: proper `<think>` and `<answer>` tags
- Result: Model naturally develops chain-of-thought, self-verification, and "aha moments"
- Limitations: poor readability, language mixing, repetition

### DeepSeek-R1 (Full Pipeline)
1. **Cold-start SFT**: Small amount of high-quality long-CoT examples to bootstrap
2. **RL Phase 1**: GRPO on reasoning tasks (math, code, logic)
3. **Rejection sampling**: Use RL checkpoint to generate data, filter by correctness
4. **SFT Phase 2**: Fine-tune on rejection-sampled data + general instruction data
5. **RL Phase 2**: Final RL stage for helpfulness and safety

### Distillation
- Distill DeepSeek-R1 into Qwen-2.5 (1.5B, 7B, 14B, 32B) and Llama-3 (8B, 70B)
- Distilled models significantly outperform non-distilled counterparts

## Results
- **AIME 2024**: 79.8% (pass@1) — comparable to o1-1217
- **MATH-500**: 97.3%
- **Codeforces**: 96.3 percentile
- Distilled R1 (14B) outperforms QwQ-32B-Preview on many benchmarks

## Connections
- **Builds on**: [[sources/deepseekmath]] (GRPO method), DeepSeek-V3 (base model)
- **Key concepts**: [[concepts/grpo]], [[concepts/rlhf]], [[concepts/distillation]]
- **Models**: [[entities/models/deepseek]]
- **Organizations**: [[entities/orgs/deepseek]]
- **GitHub**: [deepseek-ai/deepseek-r1](https://github.com/deepseek-ai/deepseek-r1) (92K ⭐)

## Citation
> DeepSeek-AI, "DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning," arXiv:2501.12948, 2025.
> https://huggingface.co/papers/2501.12948
