---
type: source
arxiv_id: "2605.06139"
title: "Listwise Policy Optimization: Group-based RLVR as Target-Projection on the LLM Response Simplex"
authors: ["Yun Qu", "Qi Wang", "Yixiu Mao", "Heming Zou", "Yuhang Jiang", "Yingyue Li", "Wutong Xu", "Lizhou Cai", "Weijie Liu", "Clive Bai"]
date: 2026-05-11
org: "Multi-institution"
tags: [rl, reasoning, grpo, theory, policy-optimization, 2026]
upvotes: 69
---

# Listwise Policy Optimization: Group-based RLVR as Target-Projection on the LLM Response Simplex

> Reveals common geometric structure of group-based RLVR methods (GRPO, DAPO, etc.) — each defines a target distribution on the response simplex — and proposes LPO that explicitly minimizes divergence to optimal targets with monotonic improvement guarantees.

## Key Contributions
- **Geometric unification**: shows GRPO, DAPO, and other group-based methods all implicitly define target distributions on the response simplex and perform approximate projection toward them
- **Response simplex framework**: treats the space of response probabilities as a probability simplex where policy optimization is target projection
- **Listwise Policy Optimization (LPO)**: explicitly constructs optimal target distributions and minimizes divergence via proper f-divergences
- **Monotonic improvement guarantee**: formal proof that LPO improves policy in each step
- **First-order approximation analysis**: shows how existing methods arise as special cases of target projection

## Method
The paper reveals that group-based policy gradient methods in RLVR share a geometric structure: given a group of responses per prompt, each method implicitly defines a target distribution on the response simplex (the space of probability assignments to the group). GRPO uses advantage-weighted softmax; DAPO uses clipped advantages; etc. LPO makes this explicit: it constructs the optimal target distribution from verified rewards and then minimizes the f-divergence between the current policy's response distribution and this target, with formal monotonic improvement guarantees.

## Results
- Consistent improvement over GRPO and DAPO on math reasoning benchmarks
- More stable training with monotonic improvement guarantees
- Provides principled framework for designing new RLVR objectives

## Connections
- Builds on: [[sources/deepseek-r1]], [[concepts/grpo]], [[sources/delta-token-credit]]
- Related: [[sources/dvao]], [[sources/resrl]], [[sources/balanced-aggregation-grpo]], [[comparisons/rl-reasoning-methods]]
- Provides: theoretical foundation for understanding all group-based RLVR methods

## Citation
> Qu et al., "Listwise Policy Optimization: Group-based RLVR as Target-Projection on the LLM Response Simplex," arXiv:2605.06139, 2026.
