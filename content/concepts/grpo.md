---
type: concept
tags: [alignment, grpo, reinforcement-learning, ppo]
---

# GRPO (Group Relative Policy Optimization)

> A simplified variant of PPO that **eliminates the critic/value model** by computing advantages relative to a group of sampled outputs — halving memory requirements while maintaining RL-based alignment quality.

## Overview
GRPO, introduced in [[sources/deepseekmath|DeepSeekMath (2024)]], addresses a practical limitation of PPO: it requires a critic model (often as large as the policy) to estimate baselines. GRPO instead samples a group of outputs for each prompt and uses the group statistics as the baseline. This was the method that enabled [[sources/deepseek-r1|DeepSeek-R1]] to achieve reasoning capabilities matching OpenAI o1.

## How It Works

### Algorithm
For each prompt `x`:
1. Sample **G** outputs `{y_1, ..., y_G}` from the old policy `π_θ_old`
2. Score each output: `r_i = R(x, y_i)` (using reward model or rule-based verifier)
3. Compute **group-relative advantages**: `Â_i = (r_i - mean(r)) / std(r)`
4. Update policy with PPO-style clipped objective using these advantages

```
L_GRPO = -E_group[min(ρ_i · Â_i, clip(ρ_i, 1-ε, 1+ε) · Â_i)] + β · KL(π_θ || π_ref)
```

Where `ρ_i = π_θ(y_i|x) / π_θ_old(y_i|x)` is the importance ratio.

### Key Advantages Over PPO
| Aspect | PPO | GRPO |
|---|---|---|
| Value/Critic model | Required | **Not needed** |
| Memory | Policy + Critic + Ref + Reward = 4 models | Policy + Ref + Reward = 3 models |
| Advantage estimation | Learned value function (GAE) | Group statistics |
| Implementation complexity | High (value head, GAE, etc.) | Lower |

## GRPO vs PPO: The Open-Reasoner-Zero Debate

[[sources/open-reasoner-zero|Open-Reasoner-Zero (2025)]] challenged GRPO's dominance, showing that **PPO with GAE(λ=1, γ=1) outperforms GRPO** for reasoning-oriented RL:

| Finding | Implication |
|---|---|
| PPO's learned critic identifies repetitive patterns | More robust advantage estimation |
| GRPO suffers training instability (mid-training quality collapse) | PPO's clipping + critic is more stable |
| PPO achieves same results in **1/10 the training steps** | More compute-efficient |
| No KL regularization needed with PPO | Simpler to tune |

The debate remains active — GRPO is simpler and was used for DeepSeek-R1 and Qwen3, while PPO shows better stability and efficiency. The choice may depend on scale and engineering constraints.

## Recent Improvements: Training GRPO Better

Two recent papers from May 2026 identify and fix structural problems in GRPO training dynamics.

### LoPE: Solving the Zero-Advantage Problem

[[sources/nonsense-helps-lope|LoPE (2026)]] identifies a critical training pathology: when **all sampled rollouts for a query fail**, the group-relative advantage collapses to zero. The model receives no training signal for these queries, wasting data and compute.

**The fix**: Inject **Lorem Ipsum-style nonsense perturbations** into the prompt space during rollout generation. This creates artificial success/failure variance where none existed, restoring training signal. The perturbed outputs are filtered via perplexity scores and assembled stochastically.

Key insight: nonsense perturbations are surprisingly effective — they broaden exploration without degrading final model quality, because the model learns to ignore the noise while benefiting from the restored gradient signal.

### Balanced Aggregation: Sequence vs Token-Level Bias

[[sources/balanced-aggregation-grpo|Balanced Aggregation (2026)]] analyzes a key implementation choice: how token-level policy gradients are aggregated within each group.

| Aggregation | Bias | When it fails |
|---|---|---|
| **Sequence aggregation** (standard GRPO) | Averages over all tokens; underweights long sequences | Long reasoning chains get diluted gradients |
| **Token aggregation** (recent alternative) | Normalizes per-token; unstable early in training | Early training collapse, high variance |
| **Balanced aggregation** (proposed) | Interpolates based on group statistics | Stable across training phases and sequence lengths |

The balanced approach dynamically interpolates between sequence and token aggregation based on group statistics, improving training stability and final performance across reasoning and code benchmarks.

### ResRL: Decoupling Positive-Negative Gradient Interference

[[sources/resrl|ResRL (2026)]] addresses a deeper problem: when negative sample reinforcement (NSR) penalizes incorrect trajectories, it **inadvertently suppresses shared valid tokens** that also appear in correct trajectories. This gradient conflict limits both Pass@1 and Pass@k performance.

**The insight**: Penalties on negatives should be confined to gradient directions **orthogonal to the positive subspace**.

**Method**:
1. Construct positive subspace S from top-k principal directions of positive token representations (via SVD)
2. Compute orthogonal-complement energy: $e(x) = (1/d) \|(I - P_S)x\|^2$
3. Reweight negative sample advantages by e(x) — higher residual = more orthogonal = stronger penalty
4. Add length-scaled reward discount beyond 3500 tokens to curb verbosity exploitation

**Results**: +9.4% Avg@16 over NSR on Qwen3-4B math; +9.6% CodeForces rating; +10.4% ALFWorld over EMPG. Best at rank k=64 (protection-discrimination sweet spot).

## Where GRPO Shines
- **Mathematical reasoning**: Verifiable correctness → clean reward signal ([[sources/deepseekmath]])
- **Code generation**: Tests as reward signal
- **Reasoning tasks**: Where outcome-based rewards are natural
- **Pure RL training**: [[sources/deepseek-r1]] used GRPO to train reasoning from scratch

## Key Papers
- [[sources/deepseekmath]] — Introduced GRPO
- [[sources/deepseek-r1]] — Scaled GRPO for reasoning
- [[sources/open-reasoner-zero]] — PPO challenges GRPO for reasoning RL
- [[sources/nonsense-helps-lope]] — LoPE: Lorem Ipsum perturbation solves zero-advantage
- [[sources/balanced-aggregation-grpo]] — Balanced aggregation fixes sequence vs token bias
- [[sources/resrl]] — ResRL: Residual-based reweighting decouples positive-negative gradient interference

## See Also
- [[concepts/rlhf]]
- [[concepts/dpo]]
- [[concepts/test-time-compute]]
- [[entities/models/deepseek]]
