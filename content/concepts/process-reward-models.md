---
type: concept
tags: [reward-modeling, alignment, reasoning, math]
---

# Process Reward Models (PRMs)

> Reward models that evaluate **each step** of a reasoning chain — providing fine-grained supervision that substantially outperforms outcome-only evaluation. The intellectual foundation for how modern reasoning models (o1, DeepSeek-R1) are trained and verified.

## Overview
When an LLM solves a multi-step math problem, there are two ways to evaluate the solution:
- **Outcome supervision (ORM)**: Just check if the final answer is correct
- **Process supervision (PRM)**: Check each intermediate step for correctness

Process supervision provides much more information — it tells the model *where* errors occur, enabling better credit assignment and more reliable reasoning. This distinction is fundamental to the training of modern reasoning models.

## How It Works

### Outcome Reward Models (ORMs)
- Train on (solution, correct/incorrect) labels
- Labels determined automatically by checking final answer
- **Problem**: Must implicitly learn where errors occur — difficult credit assignment
- **Advantage**: Cheap to label (automatic verification)

### Process Reward Models (PRMs)
- Train on (step, positive/negative/neutral) labels
- Each step scored independently given the solution prefix
- **Advantage**: Precise feedback on exactly where reasoning goes wrong
- **Challenge**: Requires step-level labels (expensive human annotation or synthetic generation)

### Evaluation: Best-of-N
1. Generate N candidate solutions from the LLM
2. Score each solution with the reward model
3. Select the highest-scoring solution
4. PRM consistently selects better solutions than ORM, especially at large N

## Key Results
From [[sources/lets-verify-step-by-step]]:
- **MATH (best-of-1860)**: PRM achieves 78.2% vs ORM at 72.4% — 5.8% absolute improvement
- PRM advantages persist across all difficulty levels
- Active learning reduces annotation cost by 2.6×
- PRM generalizes to out-of-distribution domains (AP Calculus, Chemistry, Physics)

## Role in Test-Time Compute Scaling
[[sources/scaling-test-time-compute|Snell et al. (2024)]] showed that PRMs are critical for **compute-optimal test-time scaling**:
- PRM beam search outperforms best-of-N at the same compute budget
- Product-of-step-scores is the best PRM aggregation strategy (not min, not last)
- PRMs significantly outperform ORMs for search-based test-time scaling
- Compute-optimal strategy with PRMs is **4× more efficient** than best-of-N baseline

## Relationship to Modern Reasoning Models
| Model | Reward Approach | Notes |
|---|---|---|
| OpenAI o1 | Reportedly PRM-guided | Not publicly documented |
| [[sources/deepseek-r1\|DeepSeek-R1]] | Rule-based process rewards | Format + accuracy rewards per step |
| [[sources/deepseekmath\|DeepSeekMath]] | Rule-based outcome rewards | GRPO with correctness verification |
| [[sources/kimi-k15\|Kimi k1.5]] | Outcome rewards only | Deliberately avoids PRMs, shows they're not necessary |
| [[sources/qwen3\|Qwen3]] | Rule-based verifiable rewards | In RL training stage |
| [[sources/open-reasoner-zero\|Open-Reasoner-Zero]] | Rule-based + learned critic | PPO's value function provides implicit process reward |
| [[sources/s1\|s1]] | No reward model (SFT) | Distillation approach — reasoning via imitation |
| [[sources/repro\|RePro]] | **Self-supervised process reward** | CoT-as-optimization: Magnitude + Stability scores |

**Key debate**: Kimi k1.5 achieves o1-level performance *without* process reward models, suggesting that sufficiently scaled RL with outcome rewards + long context may be enough. The optimal approach remains an active research question.

## RePro: Process Rewards Without Human Labels

[[sources/repro|RePro (2025)]] introduces a novel approach to process-level rewards that requires **no human annotation**:
- Frames CoT reasoning as a **gradient descent process** where each step implicitly optimizes toward the correct answer
- **Magnitude Score**: Measures how much each reasoning segment improves the probability of the ground truth answer
- **Stability Score**: Penalizes oscillatory reasoning patterns (up-down-up)
- **Plug-and-play**: Works with PPO, GRPO, REINFORCE++ — just add α·R_repro to the outcome reward
- **Reduces overthinking**: Produces shorter, more efficient chains while improving accuracy
- Achieves +2.5 AIME24 on Qwen3-1.7B with GRPO

This represents a practical middle ground: denser than outcome-only rewards, cheaper than human-labeled PRMs, and more principled than heuristic process rewards.

## Variants & Extensions
- **Math-Shepherd**: Automated PRM labeling via backward verification
- **Synthetic PRMs**: Use LLMs to generate step-level labels (cheaper than human annotation)
- **Rule-based process rewards**: Format compliance + step verification via code execution (DeepSeek-R1)
- **Verifiable rewards**: Mathematical/code correctness as a form of process supervision
- **Learned critics**: PPO's value function as an implicit process evaluator ([[sources/open-reasoner-zero|ORZ]])
- **Self-supervised process rewards**: [[sources/repro|RePro]]'s optimization-lens approach — derive process rewards from ground truth answers alone

## Key Papers
- [[sources/lets-verify-step-by-step]] — Foundational PRM paper (PRM800K)
- [[sources/scaling-test-time-compute]] — PRMs for compute-optimal test-time scaling
- [[sources/deepseek-r1]] — Rule-based process rewards for reasoning RL
- [[sources/deepseekmath]] — GRPO with outcome rewards
- [[sources/kimi-k15]] — Shows PRMs are not strictly necessary
- [[sources/repro]] — Self-supervised process rewards via optimization lens

## See Also
- [[concepts/rlhf]]
- [[concepts/grpo]]
- [[concepts/test-time-compute]]
- [[concepts/scaling-laws]]
- [[comparisons/rl-reasoning-methods]]
