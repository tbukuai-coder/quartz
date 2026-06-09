---
type: source
arxiv_id: "2605.15155"
title: "Self-Distilled Agentic Reinforcement Learning"
authors: ["Zhengxi Lu", "Zhiyuan Yao", "Zhuowen Han", "Zi-Han Wang", "Jinyang Wu", "Qi Gu", "Xunliang Cai", "Weiming Lu", "Jun Xiao", "Yueting Zhuang"]
date: 2026-05-15
org: "Zhejiang University / Meituan"
tags: [rl, agents, self-distillation, multi-turn, 2026]
upvotes: 111
---

# Self-Distilled Agentic Reinforcement Learning (SDAR)

> Enhances RL for multi-turn agent training by integrating on-policy self-distillation through a sigmoid gate that selectively strengthens positive token-level guidance while mitigating destabilizing negative teacher rejections.

## Key Contributions
- Identifies the problem of **compounding multi-turn instability** when transferring on-policy self-distillation (OPSD) to multi-turn agents
- Proposes **sigmoid-gated positive guidance**: selectively applies token-level distillation signal only at positive-gap positions where teacher outperforms student
- **Mitigates negative teacher rejections**: avoids pushing student away from tokens where the privileged-context teacher happens to be wrong (common in multi-turn settings)
- **Skill-conditioned guidance**: adapts distillation signal to the type of skill being executed in each turn
- Achieves 161 GitHub stars; consistently improves over GRPO and hybrid RL-OPSD baselines

## Method
SDAR runs a teacher branch with privileged context (e.g., future turns, gold tool outputs) alongside the standard RL training of a student. A sigmoid gate computes the gap between teacher and student token probabilities and applies guidance only where the teacher genuinely outperforms (positive gap). This prevents multi-turn compounding errors where the teacher is artificially confident due to privileged future context that doesn't help for the current turn. The gate is differentiable and trained end-to-end.

## Results
- Consistent improvements over GRPO and hybrid RL-OPSD baselines on multi-turn agent benchmarks
- Reduces format errors and tool-call failures in multi-step agentic tasks
- More stable training curves compared to naive OPSD transfer to multi-turn settings

## Connections
- Builds on: [[sources/agentic-rl-reasoning]], [[sources/multi-turn-agent-rl]], [[concepts/grpo]]
- Related: [[sources/anti-self-distillation]], [[sources/a2tgpo-agentic]], [[sources/skill1]]
- Related concepts: [[concepts/agents]], [[concepts/distillation]], [[comparisons/rl-reasoning-methods]]

## Citation
> Lu et al., "Self-Distilled Agentic Reinforcement Learning," arXiv:2605.15155, 2026.
