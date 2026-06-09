---
type: source
arxiv_id: "2605.06222"
title: "When to Trust Imagination: Adaptive Action Execution for World Action Models"
authors: ["Rui Wang", "Yue Zhang", "Jiehong Lin", "Kuncheng Luo", "Jianan Wang", "Zhongrui Wang", "Xiaojuan Qi"]
date: 2026-05
tags: [robotics, world-action-models, reinforcement-learning, visual-observation, embodied-ai]
upvotes: 28
---

# When to Trust Imagination: Adaptive Action Execution for World Action Models

> World Action Models (WAMs) jointly predict future visual observations and actions, but current methods execute a fixed number of predicted actions blindly. This paper formulates adaptive WAM execution as a future-reality verification problem.

## Key Contributions
- Introduces adaptive action execution for World Action Models (WAMs) in robotic manipulation
- Formulates the problem as future-reality verification: the robot should only execute predicted actions as long as the imagined future remains consistent with physical reality
- Proposes a verification mechanism to determine when to stop executing imagined actions and re-query the WAM

## Method
The core idea is to treat WAM-generated action sequences skeptically. Instead of executing all predicted actions, the robot:
1. Predicts a sequence of future observations and actions using the WAM
2. Monitors the physical rollout against the predicted observations
3. Stops executing when divergence exceeds a threshold
4. Re-queries the WAM with updated state information

This adaptive execution prevents compounding errors from executing actions based on outdated or divergent world predictions.

## Results
The approach improves robotic manipulation reliability by preventing error accumulation from blindly following WAM predictions.

## Datasets Used
- Standard robotic manipulation benchmarks for World Action Models

## Models Released
- None explicitly mentioned

## Connections
- Related to: [[sources/exoactor]] — exocentric video generation for humanoid control
- Related concepts: [[concepts/agents]], [[concepts/test-time-compute]]
- Builds on: World Action Models paradigm in robotics

## Citation
> Wang et al., "When to Trust Imagination: Adaptive Action Execution for World Action Models," arXiv:2605.06222, 2026.
