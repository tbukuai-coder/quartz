---
type: source
arxiv_id: "2605.25604"
title: "DVAO: Dynamic Variance-adaptive Advantage Optimization for Multi-reward Reinforcement Learning"
authors: ["Guochao Jiang", "Jingyi Song", "Guofeng Quan", "Chuzhan Hao", "Guohua Liu", "Yuewei Zhang"]
date: 2026-05-26
org: "Multi-institution"
tags: [rl, multi-reward, grpo, training-stability, 2026]
upvotes: 132
---

# DVAO: Dynamic Variance-adaptive Advantage Optimization for Multi-reward Reinforcement Learning

> Addresses training instability in multi-reward GRPO by dynamically weighting objectives based on empirical reward variance — maintains bounded advantage magnitudes and achieves Pareto-optimal multi-objective performance.

## Key Contributions
- **Dynamic variance-adaptive weighting**: automatically adjusts objective weights based on empirical reward variance per objective
- **Bounded advantage magnitudes**: prevents any single reward from dominating the gradient signal
- **Multi-objective Pareto frontier**: achieves better Pareto-optimal tradeoffs than static Reward Combination or Advantage Combination
- **Fixes seesaw effect**: eliminates the common problem where improving one metric degrades another
- Addresses fundamental limitation of GRPO in real-world multi-reward settings

## Method
Standard multi-reward GRPO approaches use either Reward Combination (RC: sum rewards before computing advantages) or Advantage Combination (AC: compute advantages per reward, then combine). RC generates advantages with unbounded variance across objectives; AC suffers from scale mismatches. DVAO dynamically estimates per-objective reward variance and reweights advantages to maintain bounded magnitudes, preventing any single objective from dominating the policy gradient while achieving Pareto-optimal multi-objective performance.

## Results
- Superior multi-objective performance over RC and AC baselines
- Maintains training stability across diverse reward scales
- Achieves better Pareto frontiers on multi-reward LLM alignment

## Connections
- Builds on: [[sources/deepseek-r1]], [[concepts/grpo]], [[sources/marble]]
- Related: [[sources/delta-token-credit]], [[sources/resrl]], [[comparisons/rl-reasoning-methods]]
- Extends: GRPO to practical multi-reward production settings

## Citation
> Jiang et al., "DVAO: Dynamic Variance-adaptive Advantage Optimization for Multi-reward Reinforcement Learning," arXiv:2605.25604, 2026.
