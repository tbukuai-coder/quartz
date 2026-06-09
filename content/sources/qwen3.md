---
type: source
arxiv_id: "2505.09388"
title: "Qwen3 Technical Report"
authors: ["Qwen Team", "Alibaba Group"]
date: 2025-05-14
org: "Alibaba"
tags: [open-models, reasoning, moe, alignment, 2025]
upvotes: 339
---

# Qwen3 Technical Report

> The **most upvoted model paper on HF** (339 upvotes). Introduces unified **thinking/non-thinking modes** in a single model family spanning 0.6B–235B parameters (dense + MoE), with a thinking budget mechanism for adaptive inference-time compute allocation.

## Key Contributions
- **Unified thinking modes**: Single model supports both "thinking" (step-by-step reasoning with `<think>` blocks) and "non-thinking" (fast direct response) — no need for separate chat and reasoning models
- **Thinking budget mechanism**: Users can control how many tokens the model spends "thinking," balancing latency vs. accuracy per query
- **8 models**: 6 dense (0.6B–32B) + 2 MoE (30B-A3B, 235B-A22B)
- **State-of-the-art** across coding, math, reasoning, and agent tasks
- **119 languages** (up from 29 in Qwen2.5)
- All models released under Apache 2.0
- The flagship Qwen3-235B-A22B achieves #1 on AIME 2025, LiveCodeBench, and BFCL agent benchmarks

## Method
### Architecture
- Dense models: standard decoder-only Transformer with GQA, RoPE, SwiGLU, RMSNorm, QKV bias
- MoE models: Qwen3-235B-A22B has 128 experts with top-8 routing (22B active), grouped routing with 8 groups
- Qwen3-30B-A3B: 128 experts, top-8 routing (3B active)
- All models support 32K native context (extensible to 128K+ via YaRN)

### Pre-training (3 stages)
1. **General Stage (S1)**: 30T+ tokens at 4K sequence length — broad language understanding
2. **Reasoning Stage (S2)**: Upweight math, code, STEM, reasoning data at 4K sequence length
3. **Long Context Stage (S3)**: Extend to 32K with progressive sequence length increase + YaRN

### Post-training (4 stages)
1. **Long-CoT Cold Start**: Curate dataset with verified chain-of-thought solutions, train initial thinking capability
2. **Reasoning RL**: GRPO on challenging math/code/logic problems with rule-based verifiable rewards
3. **Thinking Mode Fusion**: Merge thinking and non-thinking capabilities into a single model via mixed SFT on both modes + RL with a "thinking budget" reward
4. **General RL**: Final RL stage for helpfulness, instruction following, safety, and agent capabilities

### Thinking Mode Fusion (key innovation)
- Train a model that responds to `/think` and `/no_think` control tokens
- Mixed SFT: combine long-CoT reasoning data and standard chat data
- RL with thinking budget: reward model that penalizes excessive thinking tokens, encouraging efficient reasoning
- Result: single model deployment instead of separate chat + reasoning endpoints

## Results
| Benchmark | Qwen3-235B-A22B | DeepSeek-R1 | GPT-4o | Claude 3.5 |
|---|---|---|---|---|
| AIME 2025 | **81.5** | 70.0 | 68.5 | — |
| LiveCodeBench | **70.7** | 64.3 | 60.0 | — |
| MATH-500 | **98.2** | 97.3 | 76.6 | — |
| BFCL | **70.8** | — | 62.8 | — |
| MMLU | 86.7 | — | 88.1 | — |

- Qwen3-30B-A3B (3B active params) **matches DeepSeek-R1 (671B total)** on many reasoning benchmarks
- Qwen3-4B outperforms Qwen2.5-72B-Instruct on math benchmarks with thinking mode
- 119 languages with strong cross-lingual transfer

## Models Released
| Model | Params | Active | Architecture |
|---|---|---|---|
| Qwen3-0.6B | 0.6B | 0.6B | Dense |
| Qwen3-1.7B | 1.7B | 1.7B | Dense |
| Qwen3-4B | 4B | 4B | Dense |
| Qwen3-8B | 8B | 8B | Dense |
| Qwen3-14B | 14B | 14B | Dense |
| Qwen3-32B | 32B | 32B | Dense |
| Qwen3-30B-A3B | 30B | 3B | MoE (128 experts) |
| Qwen3-235B-A22B | 235B | 22B | MoE (128 experts) |

## Connections
- **Builds on**: [[sources/qwen25]] (Qwen2.5), [[sources/deepseekmath]] ([[concepts/grpo|GRPO]] for RL), [[sources/deepseek-r1]] (thinking/reasoning paradigm)
- **Key concepts**: [[concepts/grpo]], [[concepts/mixture-of-experts]], [[concepts/rlhf]], [[concepts/scaling-laws]]
- **Models**: [[entities/models/qwen]]
- **Organizations**: [[entities/orgs/alibaba]]

## Citation
> Qwen Team, "Qwen3 Technical Report," arXiv:2505.09388, 2025.
> https://huggingface.co/papers/2505.09388
