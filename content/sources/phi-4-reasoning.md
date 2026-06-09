---
type: source
arxiv_id: "2504.21318"
title: "Phi-4-reasoning Technical Report"
authors: ["Marah Abdin", "Sahaj Agarwal", "Ahmed Awadallah"]
date: 2025-04-30
org: "Microsoft"
tags: [reasoning, small-model, sft, rl, 2025]
upvotes: 55
---

# Phi-4-reasoning

> A 14B reasoning model that outperforms DeepSeek-R1-Distill-Llama-70B and approaches o3-mini, trained via SFT on "teachable" prompts with reasoning demonstrations from o3-mini.

## Key Contributions
- **Phi-4-reasoning (14B)** outperforms models 5× its size on complex reasoning tasks
- Introduced concept of **"teachable" prompts** — carefully curated for the right level of complexity and diversity for SFT
- **Phi-4-reasoning-plus**: Enhanced variant using outcome-based RL on top of SFT, further improving performance
- Demonstrated that **data curation for reasoning SFT** is as important as the RL stage
- Strong results across math, science, coding, algorithmic problem-solving, planning, and spatial understanding

## Method
1. **Teachable prompt selection**: Curate prompts that are complex enough to require extended reasoning but not so hard they produce noisy demonstrations
2. **Reasoning demonstration generation**: Use o3-mini to generate high-quality reasoning chains for selected prompts
3. **SFT**: Fine-tune Phi-4 (14B) on these curated reasoning demonstrations
4. **Outcome-based RL** (for Phi-4-reasoning-plus): Further refine with RL using correctness as reward

Key insight: The quality and diversity of SFT data matters enormously. Careful prompt curation outperforms naive scaling of reasoning data.

## Results
- **AIME 2024**: 75.3% (Phi-4-reasoning-plus) — competitive with much larger models
- **MATH-500**: 97.2% (Phi-4-reasoning-plus)
- **GPQA Diamond**: 72.5%
- **Outperforms**: DeepSeek-R1-Distill-Llama-70B on most reasoning benchmarks
- **Approaches**: o3-mini performance at 14B scale

## Models Released
- Phi-4-reasoning (14B) — open weights
- Phi-4-reasoning-plus (14B) — open weights

## Connections
- **Builds on**: [[sources/phi-4|Phi-4]], [[entities/models/phi|Phi family]]
- **Distills from**: o3-mini (OpenAI)
- **Org**: [[entities/orgs/microsoft|Microsoft]]
- **Related**: [[sources/deepseek-r1|DeepSeek-R1]], [[sources/s1|s1]] (both: small model + good data = strong reasoning)
- **Related concepts**: [[concepts/distillation|Distillation]], [[concepts/chain-of-thought|Chain-of-Thought]]
- **Comparison**: [[comparisons/reasoning-models|Reasoning Models]]

## Citation
> Abdin et al., "Phi-4-reasoning Technical Report," arXiv:2504.21318, 2025.
