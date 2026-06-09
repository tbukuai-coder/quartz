---
type: source
arxiv_id: "2507.07451"
title: "RLEP: Reinforcement Learning with Experience Replay for LLM Reasoning"
authors: ["Hongzhi Zhang", "Jia Fu", "Jingyuan Zhang", "Kai Fu", "Qi Wang", "Fuzheng Zhang", "Guorui Zhou"]
date: 2025-07-07
org: "Kwai (Kuaishou)"
tags: [reinforcement-learning, reasoning, experience-replay, grpo, 2025]
upvotes: 6
---

# RLEP

> A two-phase RL framework that collects verified reasoning trajectories and replays them during training, achieving faster convergence and better final performance than standard GRPO.

## Key Contributions
- Introduces **experience replay for LLM reasoning** — a two-phase framework that first collects verified successful trajectories, then replays them during subsequent RL training
- Shows that blending **newly generated rollouts with replayed successes** at every update step stabilizes training and prevents policy drift from pre-trained weights
- Achieves **faster convergence** and **higher final accuracy** than standard GRPO on mathematical reasoning benchmarks
- Simple to implement on top of existing GRPO pipelines with minimal overhead

## Method
**Phase 1 — Trajectory Collection**:
- Run the base model on training problems to generate multiple candidate solutions
- Verify solutions using rule-based reward (correct/incorrect)
- Store verified successful trajectories in an experience replay buffer

**Phase 2 — Replay-Enhanced Training**:
- At each training step, sample mini-batches that blend:
  - Newly generated rollouts from the current policy (standard GRPO)
  - Replayed successful trajectories from the buffer
- The replay trajectories serve as an anchor, preventing the policy from drifting too far from known-good reasoning patterns
- Optimizes using the standard GRPO objective on the blended batches

**Key insight**: RL for LLM reasoning is energy-intensive and unstable. The policy can gradually drift away from pre-trained weights, losing capabilities. Experience replay provides a stabilizing signal by reminding the model of successful reasoning strategies discovered earlier in training.

## Results
Based on Qwen2.5-Math-7B:
- **AIME 2024**: Improved over standard GRPO baseline
- **AIME 2025**: Improved over standard GRPO baseline
- **AMC 2023**: Consistent gains
- **Faster convergence**: Reaches target accuracy in fewer training steps
- **More stable training**: Reduced variance in training reward curves

## Connections
- Builds on: [[sources/deepseek-r1|DeepSeek-R1]] (GRPO), [[concepts/grpo|GRPO]]
- Related to: [[sources/prorl|ProRL]] (prolonged RL), [[sources/tricks-or-traps-rl|Tricks or Traps]] (RL recipes)
- Extends: [[sources/klear-reasoner|Klear-Reasoner]] (GPPO), [[sources/open-reasoner-zero|Open-Reasoner-Zero]] (PPO vs GRPO)
- Related concepts: [[concepts/rlhf]], [[concepts/grpo]], [[concepts/chain-of-thought]]

## Citation
> Zhang et al., "RLEP: Reinforcement Learning with Experience Replay for LLM Reasoning," arXiv:2507.07451, 2025.
