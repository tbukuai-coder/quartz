---
type: source
arxiv_id: "2506.01413"
title: "Incentivizing Reasoning for Advanced Instruction-Following of Large Language Models"
authors: ["Yulei Qin", "Gang Li", "Zongyi Li", "Zihan Xu", "Yuchen Shi", "Zhekai Lin", "Xiao Cui", "Ke Li", "Xing Sun"]
date: 2025-06-03
org: "Tencent / Chinese Academy of Sciences"
tags: [reasoning, rl, instruction-following, grpo, complex-instructions, cot, 2025]
upvotes: 17
---

# Incentivizing Reasoning for Advanced Instruction-Following of Large Language Models

> A GRPO-based method that teaches LLMs deep reasoning for complex instructions with compositional constraints (And, Chain, Selection, Nested) — achieving superior performance on ComplexBench and demonstrating that vanilla CoT can actually hurt performance.

## Key Contributions
- **Identifies CoT harm**: Vanilla chain-of-thought (CoT) exerts a negative impact on complex instruction following because it produces superficial reasoning that simply paraphrases instructions
- **Deep reasoning via RL**: Uses GRPO with rule-centric reward signals to cultivate structured, sophisticated reasoning for complex instructions
- **Complex instruction dataset**: LLM-based instruction evolving with compositional rules and constraints (And, Chain, Selection, Nested)
- **Generalization**: RL paradigm teaches LLMs "how to think" rather than memorizing patterns — better OOD generalization than SFT
- **Small model gains**: 1.5B models achieve larger relative improvements than 7B models, showcasing small LLM potential via test-time scaling

## Method

### Problem Definition
Complex instructions consist of compositional structures:
- **And**: Multiple independent constraints (e.g., "respond in JSON AND include 3 sections")
- **Chain**: Sequential constraints (e.g., "first summarize, then critique")
- **Selection**: Choice among alternatives
- **Nested**: Hierarchical composition of the above

### Instruction Evolving Pipeline
1. **Seed selection**: Sample from WildChat and Alpaca datasets, tagged by topic/task
2. **Constraint instantiation**: Randomly sample constraint combinations from pool, with pre-defined validity checks to eliminate conflicts
3. **LLM evolution**: Few-shot in-breadth evolution with constraint templates
4. **Quality filtering**: Seven typical issues identified and filtered via LLM-as-judge
5. **Verification**: Code-based + LLM-as-judge evaluation for constraint satisfaction

### RL Training (GRPO)
- **Algorithm**: GRPO with group-level advantage normalization
- **Format reward**: Checks for `<think>`, `</think>`, `<answer>`, `</answer>` tags
- **Accuracy reward**: Extracts and evaluates answer contents against constraints
- **Rule-centric rewards**: Sample-wise contrast signals that distinguish reasoning from answer contents

### Two-Step Inference (SDC baseline comparison)
- **Step 1**: Generate reasoning
- **Step 2**: Generate answer based on reasoning
- Decouples reasoning from answering but still lacks deep reasoning quality

## Results

### ComplexBench (Qwen2.5-7B-Instruct)

| Method | Avg. | Chain | Selection | Selection & Chain |
|---|---|---|---|---|
| I/O (baseline) | 74.47 | 70.96 | 65.67 | 62.68 |
| CoT | 72.12 | 73.18 | 70.49 | 65.85 |
| SDC | 76.18 | 73.59 | 62.69 | 56.20 |
| SFT | 73.44 | 73.07 | 69.16 | 63.03 |
| **Ours (RAIF)** | **77.40** | **76.26** | **76.26** | **63.51** |

Key findings:
- **CoT hurts**: CoT actually degrades performance (-2.35% overall) due to superficial paraphrasing
- **Deep reasoning wins**: RAIF achieves +2.93% over I/O with only 299 additional reasoning tokens
- **SFT overfits**: SFT learns surface patterns; fails on OOD constraints
- **RL generalizes**: RL-trained models maintain performance on out-of-distribution constraint types
- **Small models benefit most**: 1.5B models show larger relative gains than 7B models
- **Keyword analysis**: Models increase use of structured reasoning tokens (first, second, next, finally) on challenging benchmarks after RL

### Ablation Study
- Superior CoT enforcement (SupCoT): +3.84% on ComplexBench
- Behavior cloning (BC): -3.46% — mimicking without understanding hurts
- Best config: SupCoT + BC + RL on both math and complex datasets: +5.16%

## Datasets Used
- **ComplexBench** — Complex instruction following benchmark
- **IFEval** — Instruction format evaluation
- **CELLO** — Constraint evaluation
- **CF Bench** — Constraint following
- **FB Bench** — Format benchmark
- **Follow Bench** — Following instructions
- **Info Bench** — Information benchmark
- **DeepScaleR** — Math reasoning dataset
- **WildChat / Alpaca** — Seed instruction sources

## Models Used
- Qwen2.5-1.5B-Instruct, Qwen2.5-7B-Instruct
- DeepSeek-distilled variants
- Ministral-8B (shows inferior capacity to Qwen)

## Connections
- Builds on: [[sources/deepseek-r1|DeepSeek-R1]] (GRPO algorithm), [[sources/self-instruct|Self-Instruct]] (instruction evolving), [[sources/grpo|GRPO]] (reward model-free RL)
- Cited by / Influenced: Addresses a critical gap — RL for instruction following (not just math/code)
- Related concepts: [[concepts/chain-of-thought|Chain-of-Thought]], [[concepts/grpo|GRPO]], [[concepts/instruction-tuning|Instruction Tuning]]
- Related papers: [[sources/agentic-rl-reasoning|Agentic RL]] (RL for agents), [[sources/general-reasoner|General-Reasoner]] (cross-domain RL), [[sources/tricks-or-traps-rl|Tricks or Traps]] (RL best practices)
- GitHub: [yuleiqin/RAIF](https://github.com/yuleiqin/RAIF) (32 ⭐)

## Citation
> Qin et al., "Incentivizing Reasoning for Advanced Instruction-Following of Large Language Models," arXiv:2506.01413, 2025.
