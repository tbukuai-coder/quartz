---
type: source
arxiv_id: "2605.04077"
title: "Balanced Aggregation: Understanding and Fixing Aggregation Bias in GRPO"
authors: ["Zhiyuan Zeng", "Jiameng Huang", "Zhangyue Yin", "Jiashuo Liu", "Ziniu Li", "Bingrui Li", "Yuhao Wu", "Yining Zheng", "Ge Zhang", "Wenhao Huang"]
date: 2026-05
tags: [rlhf, grpo, reinforcement-learning, policy-gradient, optimization, reasoning]
upvotes: 1
---

# Balanced Aggregation: Understanding and Fixing Aggregation Bias in GRPO

> Analyzes how token-level policy gradient terms are aggregated within each sampled group in GRPO, showing that neither sequence aggregation nor token aggregation is universally optimal, and proposes balanced aggregation for better training stability and performance.

## Key Contributions
- Systematically analyzes the aggregation bias in GRPO-style reinforcement learning with verifiable rewards (RLVR)
- Compares sequence aggregation (standard GRPO) vs token aggregation (recent alternative)
- Shows that the choice between sequence and token aggregation creates an optimization bias that affects training stability and final performance
- Proposes balanced aggregation that interpolates between the two approaches based on group statistics

## Method
The paper investigates a key design choice in GRPO: how to aggregate token-level policy gradients within a group of sampled rollouts.
- **Sequence aggregation**: Averages the gradient over all tokens in a sequence, then normalizes by group reward statistics. Standard in original GRPO.
- **Token aggregation**: Normalizes each token's gradient individually using group statistics at that token position. Recently proposed as superior.
- **Balanced aggregation**: The paper shows both have biases. Sequence aggregation underweights long sequences; token aggregation can be unstable early in training. A balanced interpolation achieves better stability and final reward.

## Results
- Balanced aggregation improves training stability compared to pure sequence or token aggregation
- Better final performance on reasoning and code generation benchmarks using RLVR
- The analysis provides principled guidance for GRPO implementation choices

## Datasets Used
- Reasoning and code generation benchmarks

## Models Released
- None explicitly mentioned

## Connections
- Builds on: [[sources/deepseek-r1]], [[sources/tricks-or-traps-rl]], [[concepts/grpo]]
- Related: [[sources/nonsense-helps-lope]] — another GRPO training improvement
- Related: [[sources/open-reasoner-zero]] — PPO vs GRPO analysis
- Related concept: [[concepts/grpo]]

## Citation
> Zeng et al., "Balanced Aggregation: Understanding and Fixing Aggregation Bias in GRPO," arXiv:2605.04077, 2026.
