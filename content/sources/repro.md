---
type: source
arxiv_id: "2512.01925"
title: "Rectifying LLM Thought from Lens of Optimization"
authors: ["Junnan Liu", "Hongwei Liu", "Songyang Zhang", "Kai Chen"]
date: 2025-12-03
org: "OpenCompass / Shanghai AI Laboratory"
tags: [reasoning, process-reward, rl, chain-of-thought, overthinking, 2025]
upvotes: 25
---

# RePro: Rectifying LLM Thought

> Reframes chain-of-thought reasoning as a **gradient descent process** and introduces **RePro** (Rectifying Process-level Reward) — a dual scoring mechanism that combines Magnitude (optimization intensity) and Stability (trajectory smoothness) scores to create a plug-and-play process-level reward for any RLVR pipeline. Reduces overthinking while improving accuracy across PPO, REINFORCE++, and GRPO.

## Key Contributions
- **Optimization lens on CoT**: Frames each reasoning step as an implicit gradient update toward the correct answer — with log-probability of ground truth answer as proxy objective J̃
- **Dual scoring mechanism**: Magnitude Score (net improvement in J̃, measuring optimization intensity) + Stability Score (penalizes oscillatory reasoning patterns)
- **Plug-and-play process reward**: Composite RePro reward integrates into any RLVR pipeline (PPO, GRPO, REINFORCE++) with a single weight coefficient α
- **Reduces overthinking**: RePro produces shorter, more efficient reasoning chains while improving accuracy — directly addressing the wasteful "overthinking" problem in long CoT models
- **Self-supervised**: Unlike step-level PRMs that require human labeling, RePro derives process-level rewards from ground truth answers alone

## Method
Given reasoning trajectory τ = [τ_thinking; τ_conclusion]:
1. **Proxy objective**: J̃(π_θ, q, τ_≤t, a) = (1/|a|) Σ log π_θ(a_i | q, τ_≤t) — tracks how well intermediate CoT steps "set up" the model to answer correctly
2. **Segment trajectory** into k=10–30 sub-segments
3. **Magnitude Score**: S_magn = tanh(Δ(J̃) / J̄_b + 1) + 1 — normalized improvement relative to no-context baseline
4. **Stability Score**: S_stab penalizes oscillatory (up-down-up) patterns in J̃
5. **Combined reward**: R_total = R_outcome + α · R_repro, where R_repro = w·S_magn + (1-w)·S_stab
6. High-signal segments selected for backpropagation

Key insight: Good reasoning should steadily increase the probability of the correct answer (high magnitude, low oscillation). Bad reasoning oscillates or stagnates. This signal is free to compute from existing rollouts.

## Results
### DeepSeek-R1-Distill-Qwen-1.5B
| Method | AIME24 | MATH500 | GPQA-D | MBPP |
|---|---|---|---|---|
| PPO baseline | 34.8 | 86.9 | — | — |
| PPO + RePro | **36.3** | **87.7** | — | — |
| GRPO baseline | 32.9 | — | 34.5 | 62.5 |
| GRPO + RePro | **36.0** | — | **37.0** | **65.4** |

### Qwen3-1.7B
| Method | AIME24 | MATH500 |
|---|---|---|
| GRPO baseline | 47.3 | 93.4 |
| GRPO + RePro | **49.8** | **94.1** |

- Consistent gains across PPO, REINFORCE++, GRPO
- Generalizes out-of-domain (GPQA-Diamond, MBPP, LiveCodeBench)
- Reduces average reasoning token count (shorter, more efficient chains)

## Connections
- **Builds on**: [[sources/deepseek-r1|DeepSeek-R1]], [[sources/deepseekmath|DeepSeekMath/GRPO]]
- **Related**: [[sources/deepconf|DeepConf]] (also addresses overthinking), [[sources/lets-verify-step-by-step|Let's Verify Step by Step]] (process reward motivation)
- **Concepts**: [[concepts/process-reward-models|Process Reward Models]], [[concepts/grpo|GRPO]], [[concepts/chain-of-thought|Chain-of-Thought]]
- **Comparison**: [[comparisons/rl-reasoning-methods|RL Reasoning Methods]]
- **GitHub**: https://github.com/open-compass/RePro

## Citation
> Liu et al., "Rectifying LLM Thought from Lens of Optimization," arXiv:2512.01925, 2025.
