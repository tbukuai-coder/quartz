---
type: source
arxiv_id: "2605.06638"
title: "Can RL Teach Long-Horizon Reasoning to LLMs? Expressiveness Is Key"
authors: ["Tianle Wang", "Zhaoyang Wang", "Guangchen Lan", "Xinpeng Wei", "Sipeng Zhang", "Guanwen Qiu", "Abulhair Saparov"]
venue: "arXiv preprint"
year: 2026
date: "2026-05"
org: null
upvotes: 8
tags: [reinforcement-learning, reasoning, scaling-laws, long-horizon, logic, curriculum]
github: null
---

# Can RL Teach Long-Horizon Reasoning? Expressiveness Is Key (ScaleLogic)

> RL training compute scales as a **power law with reasoning depth** (T ∝ D^γ, R² > 0.99), and the scaling exponent **γ increases monotonically with logical expressiveness** from 1.04 to 2.60 — demonstrating that *what* a model is trained on, not just *how much*, determines downstream transfer efficiency.

## Key Contributions

1. **ScaleLogic framework**: Synthetic logical reasoning environment with independent control over reasoning depth (horizon) and logical expressiveness (5 levels from implication-only to first-order quantification)
2. **Power-law scaling discovery**: Training compute T follows T ∝ D^γ (R² > 0.99); scaling exponent γ increases monotonically with expressiveness: 1.04 → 1.22 → 1.47 → 1.71 → 2.60
3. **Expressiveness determines transfer**: More expressive training yields both larger downstream gains (+10.66 points) and more compute-efficient transfer — what matters is training content, not just volume
4. **Cross-algorithm robustness**: Power-law holds across DAPO, GRPO, and REINFORCE++ — it's a property of the task, not the algorithm
5. **Curriculum substantially improves efficiency**: Threshold-triggered curriculum reduces training compute by ~3× compared to fixed-depth training

## Method

### ScaleLogic: Five Levels of Logical Expressiveness
| Level | Logical Features | γ (scaling exponent) |
|---|---|---|
| Implication-only | If A then B | 1.04 |
| + Conjunction | If A and B then C | 1.22 |
| + Negation | If A and not B then C | 1.47 |
| + Disjunction | If A then B or C | 1.71 |
| + Quantification | For all X, if P(X) then Q(X) | 2.60 |

### Key Insight: Why Expressiveness Matters
Each expressiveness level introduces qualitatively different reasoning demands:
- **Conjunction**: Track multiple supporting literals simultaneously
- **Negation**: Maintain polarity throughout proof
- **Disjunction**: Handle branching proof paths (case analysis)
- **Quantification**: Ground universal rules to specific entities

### Training Setup
- Model: Qwen3-4B (non-thinking), replicated on Qwen3-8B
- RL algorithm: DAPO (extension of GRPO)
- Training: 8× B200 180G GPUs
- Reward: Binary correctness on multiple-choice logical reasoning

## Results

### Power-Law Scaling (T ∝ D^γ)
- All fits achieve R² > 0.99
- γ increases monotonically: 1.04, 1.22, 1.47, 1.71, 2.60
- Implication: training cost for complex logical reasoning grows **super-linearly** with depth

### Downstream Transfer (Qwen3-4B)
| Training Setting | Avg Downstream Gain | Steps to +5% |
|---|---|---|
| Implication-only | +4.93 | — (never) |
| + Conjunction | +6.86 | ~900 |
| + Negation | +7.51 | ~700 |
| + Disjunction | +8.99 | ~500 |
| + Quantification | **+10.66** | ~400 |

More expressive training → larger gains AND faster convergence on downstream benchmarks (MATH, GSM8K, ARC, LogiQA).

### Cross-Algorithm Robustness
| Algorithm | γ (+ Conjunction) |
|---|---|
| DAPO | 1.22 |
| GRPO | 1.24 |
| REINFORCE++ | 1.26 |

Near-identical scaling exponents → power law is a task property, not algorithm-specific.

### Curriculum Training
- Threshold-triggered curriculum (start depth 1, advance when accuracy > threshold)
- ~3× more compute-efficient than training at fixed maximum depth
- Same final accuracy reached with substantially fewer steps

## Connections

- [[sources/deepseek-r1|DeepSeek-R1]] — GRPO-based reasoning; ScaleLogic studies how RL scales with reasoning complexity
- [[concepts/grpo|GRPO]] — Core algorithm; ScaleLogic shows power-law scaling is algorithm-agnostic
- [[concepts/scaling-laws|Scaling Laws]] — New scaling dimension: reasoning depth as fundamental complexity axis
- [[comparisons/rl-reasoning-methods|RL Reasoning Methods]] — Adds expressiveness as key variable in RL reasoning training
- [[sources/tricks-or-traps-rl|Tricks or Traps]] — Practical RL recipes; ScaleLogic provides theoretical grounding
- [[sources/scaling-implicit-deductive-reasoning|Implicit Deductive Reasoning]] — Both study how reasoning depth affects model capability
