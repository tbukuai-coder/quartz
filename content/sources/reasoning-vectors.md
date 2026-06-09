---
type: source
arxiv_id: "2509.01363"
title: "Reasoning Vectors: Transferring Chain-of-Thought Capabilities via Task Arithmetic"
authors: ["Mohammad Zbeeb", "Hasan Abed Al Kader Hammoud", "Bernard Ghanem"]
date: 2025-09-02
org: "KAUST"
tags: [reasoning, model-merging, task-arithmetic, transfer, 2025]
upvotes: 62
---

# Reasoning Vectors

> Demonstrates that reasoning capability from RL can be extracted as a compact task vector and transferred to other models via task arithmetic — no retraining needed.

## Key Contributions
- **Reasoning as a transferable vector**: Extract the difference between SFT and GRPO-trained models as a "reasoning vector"
- **Zero-cost transfer**: Add the reasoning vector to any instruction-tuned model to improve reasoning — no additional training
- Works across **diverse benchmarks**: GSM8K, HumanEval, SciQ, BigBenchHard
- Robust under **adversarial conditions** — reasoning vectors are difficult to remove
- Connects **model merging** and **reasoning RL** — two previously separate research areas

## Method
1. Start with two Qwen2.5 checkpoints from the same base: one SFT-only, one GRPO-trained
2. Compute reasoning vector: V_reason = θ_GRPO − θ_SFT
3. Apply to any target model: θ_target_new = θ_target + α · V_reason
4. The scaling factor α controls reasoning intensity

Key insight: RL-trained reasoning capability is localized in weight space and can be arithmetically extracted and transplanted.

## Results
- **GSM8K**: +8-15% improvement on instruction-tuned models receiving the reasoning vector
- **HumanEval**: Improved code reasoning
- **SciQ, BBH**: Generalized improvement across reasoning types
- Works even when source and target models have different instruction tuning

## Connections
- **Builds on**: [[sources/ties-merging|TIES-Merging]], [[sources/dare|DARE]], [[concepts/model-merging|Model Merging]]
- **Source RL**: [[concepts/grpo|GRPO]], [[sources/deepseekmath|DeepSeekMath]]
- **Related**: [[sources/meta-abilities-alignment|Meta-Abilities Alignment]] (also uses merging for reasoning)
- **Concepts**: [[concepts/model-merging|Model Merging]], [[concepts/grpo|GRPO]]

## Citation
> Zbeeb et al., "Reasoning Vectors: Transferring Chain-of-Thought Capabilities via Task Arithmetic," arXiv:2509.01363, 2025.
