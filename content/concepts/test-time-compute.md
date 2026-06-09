---
type: concept
tags: [reasoning, inference, scaling-laws, test-time, 2024, 2025]
---

# Test-Time Compute Scaling

> Using additional computation at inference time (longer reasoning chains, multiple samples, verification) to improve model performance — the paradigm behind o1, DeepSeek-R1, and s1.

## Overview
Test-time compute scaling is the idea that instead of only scaling models at training time (more parameters, more data), you can also scale at inference time by giving the model more computation per query. This is the core insight behind OpenAI's o1, DeepSeek's R1, and the broader "reasoning models" paradigm. The theoretical foundations were laid by [[sources/scaling-test-time-compute|Snell et al. (2024)]], who showed a small model with optimal test-time compute can outperform a 14× larger model.

## How It Works

### Two Mechanisms

**1. Parallel scaling** — Generate multiple independent solutions, select the best:
- **Best-of-N**: Sample N responses, pick the one scored highest by a verifier
- **Majority voting**: Sample N, take the most common answer
- Scales with √N — diminishing returns quickly

**2. Sequential scaling** — Generate longer, deeper reasoning chains:
- **Chain-of-thought**: Model "thinks step by step" — more tokens = deeper reasoning
- **Budget forcing**: Suppress end-of-thinking token, append "Wait" to force continued reasoning ([[sources/s1|s1]])
- **Self-revision**: Model critiques and revises its own answers iteratively
- Scales more efficiently — each step can build on previous reasoning

### Compute-Optimal Strategy
[[sources/scaling-test-time-compute|Snell et al.]] showed the optimal strategy depends on prompt difficulty:
| Difficulty | Best Strategy | Why |
|---|---|---|
| Easy | Best-of-N (small N) | Model already knows the answer; more compute is wasted |
| Medium | Beam search with PRM | Verification catches errors; search finds good paths |
| Hard | Sequential revision | Needs deep reasoning; each revision builds understanding |

### Training Methods for Reasoning
Three approaches to create models that can use test-time compute effectively:

1. **RL from scratch** (no SFT): [[sources/deepseek-r1|DeepSeek-R1]], [[sources/open-reasoner-zero|Open-Reasoner-Zero]]
   - Apply RL (GRPO or PPO) directly to base model with rule-based rewards
   - Emergent chain-of-thought, self-correction, backtracking
   
2. **SFT on reasoning traces** (distillation): [[sources/s1|s1]]
   - Fine-tune on curated reasoning examples (as few as 1K)
   - Budget forcing at inference extends thinking
   
3. **RL after SFT warm-up**: [[sources/kimi-k15|Kimi k1.5]], [[sources/qwen3|Qwen3]]
   - SFT first for basic reasoning, then RL to scale further
   - Often the strongest practical approach

## Key Results
| Model | Method | AIME24 | Key Finding |
|---|---|---|---|
| s1-32B | SFT + budget forcing | 57% | 1K examples sufficient |
| DeepSeek-R1 | Pure RL (GRPO) | 79.8% | Emergent reasoning from RL alone |
| ORZ-32B | Pure RL (PPO) | 53.3% | PPO > GRPO, 10× more efficient |
| Kimi k1.5 | SFT + RL | 77.5% | Long context RL scales reasoning |

## Key Papers
- [[sources/scaling-test-time-compute|Scaling Test-Time Compute]] (2024) — theoretical framework
- [[sources/lets-verify-step-by-step|Let's Verify Step by Step]] (2023) — process reward models
- [[sources/deepseek-r1|DeepSeek-R1]] (2025) — pure RL reasoning
- [[sources/s1|s1]] (2025) — SFT distillation + budget forcing
- [[sources/open-reasoner-zero|Open-Reasoner-Zero]] (2025) — PPO > GRPO for reasoning RL
- [[sources/kimi-k15|Kimi k1.5]] (2025) — scaling RL with long context

## See Also
- [[concepts/process-reward-models|Process Reward Models]]
- [[concepts/scaling-laws|Scaling Laws]]
- [[concepts/grpo|GRPO]]
- [[concepts/rlhf|RLHF]]
- [[comparisons/reasoning-models|Reasoning Models Comparison]]
