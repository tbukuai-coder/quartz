---
type: source
arxiv_id: "2605.13301"
title: "Achieving Gold-Medal-Level Olympiad Reasoning via Simple and Unified Scaling"
authors: ["Yafu Li", "Runzhe Zhan", "Haoran Zhang", "Shunkai Zhang", "Yizhuo Li", "Zhilin Wang", "Jiacheng Chen", "Futing Wang", "Xuyang Hu", "Yuchen Fan"]
date: 2026-05-15
org: "Simplified Reasoning"
tags: [reasoning, rl, olympiad, math, physics, scaling, 2026]
upvotes: 159
---

# Achieving Gold-Medal-Level Olympiad Reasoning via Simple and Unified Scaling (SU-01)

> A simple unified recipe converts post-trained reasoning backbones into gold-medal-level olympiad solvers through reverse-perplexity curriculum SFT, two-stage RL, and test-time scaling — achieving IMO and IPhO gold-medal performance.

## Key Contributions
- **Reverse-perplexity curriculum for SFT**: orders training data by decreasing perplexity to instill rigorous proof-writing and self-checking behaviors before RL
- **Two-stage reinforcement learning**: (1) proof-search RL with verifiable rewards for exploration, (2) proof-level RL for refinement and self-correction
- **Test-time scaling**: trajectory-level and token-level budget allocation during inference
- Achieves **gold-medal performance** on International Mathematical Olympiad (IMO) and International Physics Olympiad (IPhO) problems
- Simple and unified — the same recipe works for both math and physics without domain-specific modifications

## Method
Starting from a post-trained reasoning model, the pipeline applies: (1) Reverse-perplexity curriculum SFT — harder examples first by model perplexity, teaching structured proof writing; (2) Stage-1 RL — proof-search with verifiable rewards to expand solution coverage; (3) Stage-2 RL — proof-level refinement with self-checking rewards to improve rigor; (4) Test-time scaling — adaptive compute allocation at inference time. The recipe is intentionally minimal — no domain-specific engineering, reward hacking mitigations, or specialized architectures.

## Results
- Gold-medal-level on IMO 2024/2025 problems
- Gold-medal-level on IPhO problems
- Competitive with specialized systems while using a unified approach
- 89 GitHub stars for the SU-01 system

## Connections
- Builds on: [[sources/deepseek-r1]], [[sources/deepseek-prover-v2]], [[concepts/grpo]], [[sources/scaling-test-time-compute]]
- Related: [[sources/scalelogic]], [[sources/klear-reasoner]], [[sources/prorl]]
- Related concepts: [[concepts/test-time-compute]], [[concepts/chain-of-thought]], [[comparisons/reasoning-models]]

## Citation
> Li et al., "Achieving Gold-Medal-Level Olympiad Reasoning via Simple and Unified Scaling," arXiv:2605.13301, 2026.
